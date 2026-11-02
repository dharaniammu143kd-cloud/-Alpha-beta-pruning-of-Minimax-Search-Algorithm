<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name:       </h3>
<h3>Register Number/Staff Id:           </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance
<hr>
<h2>Sample Input and Output:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)

# program:
```
# Experiment No: 7
# Implement Alpha-Beta Pruning of Minimax Search Algorithm
# for a Simple Tic-Tac-Toe Game

import math

# Initialize the board
board = [" " for _ in range(9)]

# Display the board
def display_board(board):
    for i in range(0, 9, 3):
        print(" | ".join(board[i:i+3]))
        if i < 6:
            print("---------")

# Check winner
def check_winner(board, player):
    win_positions = [
        [0, 1, 2], [3, 4, 5],
        [6, 7, 8], [0, 3, 6],
        [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6]
    ]

    for pos in win_positions:
        if all(board[i] == player for i in pos):
            return True

    return False

# Check whether board is full
def is_full(board):
    return " " not in board

# Alpha-Beta Pruning with Minimax
def minimax(board, depth, alpha, beta, is_maximizing):

    if check_winner(board, "O"):
        return 10 - depth

    if check_winner(board, "X"):
        return depth - 10

    if is_full(board):
        return 0

    if is_maximizing:
        best_score = -math.inf

        for i in range(9):
            if board[i] == " ":
                board[i] = "O"

                score = minimax(
                    board, depth + 1,
                    alpha, beta, False
                )

                board[i] = " "
                best_score = max(best_score, score)
                alpha = max(alpha, best_score)

                if beta <= alpha:
                    break

        return best_score

    else:
        best_score = math.inf

        for i in range(9):
            if board[i] == " ":
                board[i] = "X"

                score = minimax(
                    board, depth + 1,
                    alpha, beta, True
                )

                board[i] = " "
                best_score = min(best_score, score)
                beta = min(beta, best_score)

                if beta <= alpha:
                    break

        return best_score

# Find the best move for computer
def best_move(board):
    best_score = -math.inf
    move = None

    for i in range(9):
        if board[i] == " ":
            board[i] = "O"

            score = minimax(
                board, 0,
                -math.inf, math.inf, False
            )

            board[i] = " "

            if score > best_score:
                best_score = score
                move = i

    return move

# Main game
print("TIC-TAC-TOE USING ALPHA-BETA PRUNING")
print("You are X and Computer is O")

while True:

    display_board(board)

    # Player's turn
    while True:
        try:
            move = int(input("Enter position (1-9): ")) - 1

            if 0 <= move < 9 and board[move] == " ":
                break

            print("Invalid position! Try again.")

        except ValueError:
            print("Please enter a number between 1 and 9.")

    board[move] = "X"

    if check_winner(board, "X"):
        display_board(board)
        print("You win!")
        break

    if is_full(board):
        display_board(board)
        print("Game Draw!")
        break

    # Computer's turn
    print("Computer is thinking...")

    move = best_move(board)
    board[move] = "O"

    if check_winner(board, "O"):
        display_board(board)
        print("Computer wins!")
        break

    if is_full(board):
        display_board(board)
        print("Game Draw!")
        break
```
# output:

<img width="437" height="627" alt="image" src="https://github.com/user-attachments/assets/76ff0a09-b17b-4b87-b284-d7db4dad0d64" />

