# Peg-Game
// This program simulates a peg game, where the objective is to jump pegs over adjacent pegs into empty spots, removing the jumped over pegs. 'T' represents a peg and '.' represents an empty space. Players are prompted to input a move in three characters and the program checks if the move is valid before executing it. The game ends when one peg remains, and the player is congratulated for winning.
#include <iostream>
using namespace std;

int row(char peg);
int col(char peg);

// intializes the pegs
char pegA = '.';
char pegB = 'T';
char pegC = 'T';
char pegD = 'T';
char pegE = 'T';
char pegF = 'T';
char pegG = 'T';
char pegH = 'T';
char pegI = 'T';
char pegJ = 'T';
char pegK = 'T';
char pegL = 'T';
char pegM = 'T';
char pegN = 'T';
char pegO = 'T';

// function to display the game board
void displayBoard() {
	cout << "    " << pegA << "            A" << endl;
	cout << "   " << pegB << " " << pegC << "          B C" << endl;
	cout << "  " << pegD << " " << pegE << " " << pegF << "        D E F" << endl;
	cout << " " << pegG << " " << pegH << " " << pegI << " " << pegJ << "      G H I J" << endl;
	cout << pegK << " " << pegL << " " << pegM << " " << pegN << " " << pegO << "    K L M N O" << endl;
}

// Function to get a reference to a specific peg based on its character
char& getPeg(char peg) {
	// return the reference to the peg based on the character inputted
	switch (toupper(peg)) {
		case 'A': return pegA;
		case 'B': return pegB;
		case 'C': return pegC;
		case 'D': return pegD;
		case 'E': return pegE;
		case 'F': return pegF;
		case 'G': return pegG;
		case 'H': return pegH;
		case 'I': return pegI;
		case 'J': return pegJ;
		case 'K': return pegK;
		case 'L': return pegL;
		case 'M': return pegM;
		case 'N': return pegN;
		case 'O': return pegO;
		default: return pegA;
	}
}

// Function to check if move is valid
bool isValidMove(char from, char over, char to) {
	// checks if all characters are valid, between 'A' - 'O'
	if (from < 'A' || from > 'O' || over < 'A' || over > 'O' || to < 'A' || to > 'O') {
		return false;
	}
	
	if (getPeg(from) != 'T' || getPeg(over) != 'T' || getPeg(to) != '.') {
		return false;
	}
	return true;
	
	// Determines the row and column for the peg in the move
	int rowFrom = row(from), colFrom = col(from);
	int rowOver = row(over), colOver = col(over);
	int rowTo = row(to), colTo = col(to);

	// checks if the movid is a valid jump
	if ((rowFrom == rowOver && rowOver == rowTo && abs(colFrom - colOver) == 1 && abs(colOver - colTo) == 1) || (colFrom == colOver && colOver == colTo && abs(rowFrom - rowOver) == 1 && abs(rowOver - rowTo) == 1)) {
		return true;
	}
	return false; // invalid move
}

// function to update the peg after a move is made
void makeMove(char from, char over, char to) {
	getPeg(from) = '.';
	getPeg(over) = '.';
	getPeg(to) = 'T';
}

// function to check if the game has been won
bool checkWin() {
	int count = 0;
	for (char peg = 'A'; peg <= 'O'; peg++) {
		if (getPeg(peg) == 'T') {
			count++;
		}
	}
	return count == 1;
}

// main game loop
int main() {
	string move; // variable to store the players input move
	while (true) {
		displayBoard(); //displays the board
		cout << "Enter move (for example FCA) or Q to quit: " << endl;
		cin >> move; // get the move from the player
		cout << endl;

		if (move == "Q" || move == "q") {
			break; // quit the game if 'Q' or 'q' is entered
		}

		// checks if the move is a valid length
		if (move.length() != 3 || !isValidMove(move[0], move[1], move[2])) {
			cout << "Move is not valid. Try again." << endl;
			continue;
		}

		// makes the valid move
		makeMove(move[0], move[1], move[2]);

		// checks if the game has been won
		if (checkWin()) {
			cout << "You win! Congratulations!" << endl;
			break; // exists the game loop if the game has been won
		}
	}
	return 0;
}

// row returns the row of the given peg location
// Parameter peg is a character, with the letter of the peg (A-O)
// Letter should be upper case, between A and O
// Returns the row (1 through 5). 
// Row 1 is the top row (with one peg), row 5 is the bottom (with 5 pegs)
int row(char peg) {
	if (peg >= 'K') {
		return 5;
	}
	else if (peg >= 'G') {
		return 4;
	}
	else if (peg >= 'D') {
		return 3;
	}
	else if (peg >= 'B') {
		return 2;
	}
	else if (peg == 'A') {
		return 1;
	}
	else {
		cout << "Error - row: Invalid peg: " << peg << endl;
		return -1;
	}
}

// col returns the column of the given peg location
// Parameter peg is a character, with the letter of the peg (A-O)
// Letter should be upper case, between A and O
// Returns the column (1 through 5). 
// At each level, the first letter is column 1, the second letter is column 2, etc.
int col(char peg) {
	if (peg >= 'K') {
		return peg - 'K' + 1;
	}
	else if (peg >= 'G') {
		return peg - 'G' + 1;
	}
	else if (peg >= 'D') {
		return peg - 'D' + 1;
	}
	else if (peg >= 'B') {
		return peg - 'B' + 1;
	}
	else if (peg == 'A') {
		return 1;
	}
	else {
		cout << "Error - col: Invalid peg: " << peg << endl;
		return -1;
	}
}
