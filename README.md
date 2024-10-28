import chess
import chess.engine

# Initialize the chess board and Stockfish
board = chess.Board()
engine_path = "path/to/stockfish"  # Replace with your Stockfish path
engine = chess.engine.SimpleEngine.popen_uci(engine_path)

def get_bot_move(board):
    """Gets the bot's next move from Stockfish."""
    result = engine.play(board, chess.engine.Limit(time=0.1))
    return result.move

# Main game loop
while not board.is_game_over():
    print(board)
    if board.turn == chess.WHITE:
        move = get_bot_move(board)  # Bot plays as white
        print(f"Bot move: {move}")
    else:
        move = input("Enter your move (e.g., e2e4): ")
        try:
            board.push(chess.Move.from_uci(move))
        except ValueError:
            print("Invalid move! Try again.")
            continue
    board.push(move)

engine.quit()
print("Game over!")
