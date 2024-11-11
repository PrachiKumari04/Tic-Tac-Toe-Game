


# Tic Tac Toe Game

A simple and user-friendly Tic Tac Toe game implemented in JavaScript, HTML, and CSS. The game features two modes: playing against a friend and playing against a smart computer opponent.

## Features

- Two modes: 
  - **2 Players**: Play with a friend.
  - **Vs Computer**: Play against a computer with an unbeatable AI.
- User-friendly interface.
- Colored X and O symbols:
  - X is displayed in red.
  - O is displayed in black.
- Handles user clicks, tracks game state, and checks for winning conditions.
- Restart game functionality.

## How to Play

1. Open `index.html` in a web browser.
2. Choose the game mode: 
   - Click `2 Players` to play with a friend.
   - Click `Vs Computer` to play against the computer.
3. Click on any cell in the game board to make your move.
4. The game will announce the winner or if it ends in a draw.
5. Click `Restart` to start a new game.

## Files

- `index.html`: The HTML structure of the game.
- `style.css`: The CSS styling for the game.
- `script.js`: The JavaScript logic for handling game functionality.

## Minimax Algorithm

The Minimax algorithm is used to make the computer opponent unbeatable. It evaluates the game board recursively to determine the best possible move for the computer, ensuring it plays optimally.

### Minimax Function

The `minimax` function takes the current board state and the player (`X` or `O`). It generates all possible moves, evaluates them recursively, and returns the move with the best score. The computer (O) tries to maximize the score, while the player (X) tries to minimize it.

```javascript
function minimax(newBoard, player) {
    const availSpots = newBoard.map((cell, index) => cell === null ? index : null).filter(v => v !== null);

    if (checkWin(newBoard, 'X')) {
        return { score: -10 };
    } else if (checkWin(newBoard, 'O')) {
        return { score: 10 };
    } else if (availSpots.length === 0) {
        return { score: 0 };
    }

    const moves = [];
    for (let i = 0; i < availSpots.length; i++) {
        const move = {};
        move.index = availSpots[i];
        newBoard[availSpots[i]] = player;

        if (player === 'O') {
            const result = minimax(newBoard, 'X');
            move.score = result.score;
        } else {
            const result = minimax(newBoard, 'O');
            move.score = result.score;
        }

        newBoard[availSpots[i]] = null;
        moves.push(move);
    }

    let bestMove;
    if (player === 'O') {
        let bestScore = -10000;
        for (let i = 0; i < moves.length; i++) {
            if (moves[i].score > bestScore) {
                bestScore = moves[i].score;
                bestMove = i;
            }
        }
    } else {
        let bestScore = 10000;
        for (let i = 0; i < moves.length; i++) {
            if (moves[i].score < bestScore) {
                bestScore = moves[i].score;
                bestMove = i;
            }
        }
    }

    return moves[bestMove];
}




https://github.com/user-attachments/assets/abf7f8d0-8fcc-49bc-bf79-0267e816b828



