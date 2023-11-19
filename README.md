# Codsoft_Second-Project
tic_tac_toe game



CODE -----


#include<bits/stdc++.h>
using namespace std;


// tic_tac_toe in c++


char gameBoard[9] = { ' ',' ',' ',' ',' ',' ',' ',' ',' ' };
int playerMove;

void displayBoard();
void playerMoveX();
void playerMoveO();
void computerMove();
void resetBoard();
char checkGameState();
void playAgainstComputer();
void playAgainstPlayer();

int main() {
    while (true) {
        int gameMode;
        cout << "Welcome to Tic-Tac-Toe!" << endl;
        cout << "1. Player vs Computer" << endl;
        cout << "2. Player X vs Player O" << endl;
        cout << "Choose the game mode: ";
        cin >> gameMode;

        switch (gameMode) {
            case 1: playAgainstComputer(); break;
            case 2: playAgainstPlayer(); break;
            default: cout << "Invalid Mode" << endl; break;
        }
    }
    return 0;
}

void resetBoard() {
    for (int i = 0; i < 9; i++) {
        gameBoard[i] = ' ';
    }
}

void playerMoveX() {
    while (true) {
        cin >> playerMove;
        playerMove--;
        if (playerMove < 0 || playerMove > 8 || gameBoard[playerMove] != ' ') {
            cout << "Invalid position. Try again: ";
        } else {
            gameBoard[playerMove] = 'X';
            break;
        }
    }
}

void playerMoveO() {
    while (true) {
        cin >> playerMove;
        playerMove--;
        if (playerMove < 0 || playerMove > 8 || gameBoard[playerMove] != ' ') {
            cout << "Invalid position. Try again: ";
        } else {
            gameBoard[playerMove] = 'O';
            break;
        }
    }
}

void computerMove() {
    srand(time(0));
    do {
        playerMove = rand() % 9;
    } while (gameBoard[playerMove] != ' ');
    gameBoard[playerMove] = 'O';
}

void displayBoard() {
    cout << "   " << gameBoard[0] << " | " << gameBoard[1] << " | " << gameBoard[2] << endl;
    cout << "   ---------" << endl;
    cout << "   " << gameBoard[3] << " | " << gameBoard[4] << " | " << gameBoard[5] << endl;
    cout << "   ---------" << endl;
    cout << "   " << gameBoard[6] << " | " << gameBoard[7] << " | " << gameBoard[8] << endl;
}

char checkGameState() {
    for (int i = 0; i < 9; i += 3) {
        if (gameBoard[i] == gameBoard[i + 1] && gameBoard[i + 1] == gameBoard[i + 2] && gameBoard[i] != ' ') {
            if (gameBoard[i] == 'X') {
                return 'X';
            } else {
                return 'O';
            }
        }
    }

    for (int i = 0; i < 3; i++) {
        if (gameBoard[i] == gameBoard[i + 3] && gameBoard[i + 3] == gameBoard[i + 6] && gameBoard[i] != ' ') {
            if (gameBoard[i] == 'X') {
                return 'X';
            } else {
                return 'O';
            }
        }
    }

    if ((gameBoard[0] == gameBoard[4] && gameBoard[4] == gameBoard[8] && gameBoard[0] != ' ') ||
        (gameBoard[2] == gameBoard[4] && gameBoard[4] == gameBoard[6] && gameBoard[2] != ' ')) {
        if (gameBoard[4] == 'X') {
            return 'X';
        } else {
            return 'O';
        }
    }

    bool isDraw = true;
    for (int i = 0; i < 9; i++) {
        if (gameBoard[i] == ' ') {
            isDraw = false;
            break;
        }
    }
    if (isDraw) {
        return 'D';
    }

    return 'C';
}

void playAgainstComputer() {
    resetBoard();
    while (true) {
        displayBoard();
        playerMoveX();
        char gameState = checkGameState();
        if (gameState == 'X') {
            displayBoard();
            cout << "Player X wins!" << endl;
            break;
        } else if (gameState == 'D') {
            displayBoard();
            cout << "It's a draw!" << endl;
            break;
        }
        computerMove();
        if (gameState == 'O') {
            displayBoard();
            cout << "Computer wins!" << endl;
            break;
        }
    }
}

void playAgainstPlayer() {
    resetBoard();
    while (true) {
        displayBoard();
        playerMoveX();
        char gameState = checkGameState();
        if (gameState == 'X') {
            displayBoard();
            cout << "Player X wins!" << endl;
            break;
        } else if (gameState == 'D') {
            displayBoard();
            cout << "It's a draw!" << endl;
            break;
        }
        playerMoveO();
        if (gameState == 'O') {
            displayBoard();
            cout << "Player O wins!" << endl;
            break;
        }
    }
}
