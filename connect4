// clang++-7 -pthread -std=c++17 -o main main.cpp
#include <iostream>
#include <vector>
#include <string> 
using namespace std; 

//declare new data types, typedef allows more efficient way to initialize variables with vector types, especially matrices
typedef vector< string > stringvector;
typedef vector< stringvector > stringmatrix;

//display matrix
//requires stringmatrix and does not need to return anything
auto DisplayMatrix(stringmatrix printpls) -> void {
  //ranged for loop
  for (auto vector : printpls){
    for (auto num : vector){
      //prints every number in row, separated by a tab
      cout << num << "\t";
    }
    //after done all numbers in the row, goes to next line
    cout << "\n";
  }
}
//place token in desired spot
//requires playerMove, stringmatrix and whichPlayer from main method
//returns updated stringmatrix
auto placeToken(string playerMove, stringmatrix matrix, bool whichPlayer) -> stringmatrix {
    int row = static_cast<int> (matrix.size());
    int col = static_cast<int> (matrix[0].size());
    for (int i =0; i < row; i++){
      for (int j = 0; j < col; j++){
        //first player changes matrix index to X
        //determines to which token to change to by using the whichPlayer bool variable
        //since there are only 2 players, a bool variable is sufficient
        if (matrix[i][j] == playerMove && whichPlayer){
          matrix[i][j] = "X";
        }
        //second player changes matrix index to O
        else if (matrix[i][j] == playerMove && !whichPlayer){
          matrix[i][j] = "O";
        }
      }
    }
    return matrix;
}

// check input 
//requires stringmatrix and where the player wants to go
//returns whether the player can place their chip there
//checking whether or not the chip that the player inputted is floating in space
//the game is played perpendicular to a table, a chip must be sitting below where a player wants to place it
//if a player wanted to place a chip without anything supporting it, it would fall to the index below it, developed a function to ensure that the chip was either to be placed in the bottom row, or there was a chip below the desired index to support it 
//This proved to be difficult because once a function has returned something, it does not progress through any more of the code within it
//As a result, we had to implement a nested loop to ensure that every condition has a corresponding return statement that does not produce an endless loop
auto checkInput(stringmatrix matrix, string playerMove ) -> bool {
  for (int i = 0; i < static_cast<int> (matrix.size()); i++){
    for (int j =0; j < static_cast<int> (matrix[0].size()); j++){
      // if it's already taken i.e. X or O; entry can't be X or O, 
      // conditions to ensure player's desired placement is valid
      //cannot already have a token in index and cannot be an element not already set in the matrix
        if (matrix[i][j] != "X" && matrix[i][j] != "O" && matrix[i][j]== playerMove){
          //check if input is floating in space, can only place chip if there is a chip below it to support
          // feature was improvement that was added on in later stages -- added constraints for the user better reflects game of connect4 (rather than tictactoe)
          if(i !=4 && matrix[i+1][j] !="X" && matrix[i+1][j] != "O"){
            cout << "You cannot place a chip here as there is nothing below to support it. Please try again." << endl;
            return false;
          }
  
        return true;
      }
    }
  }
  cout << "You cannot place a chip here as there is either already someone else's or your desired index is out of bounds. Please try again." << endl;
  return false; 
}
 
//requires bool to determine if game is done, stringmatrix and which player is playing (to determine who won)
//returns whether someone won
//another challenge was identifying the winner of the game since there are different ways of winning a game
// a person can win by having four of their chips in a row, column, or diagonal
//had to include different conditional statements that would check for consecutive horizontal, vertical and diagonal indices
//We handled these challenges by using variable traces and print statements before and after different loops and conditional statements to determine if our code was successfully progressing
auto checkWinner(bool continueplaying, stringmatrix matrix, bool whichPlayer) -> bool {
  string tile; 
  if (whichPlayer){
    tile = "X";
  }
  else{
    tile="O";
  }
  auto board_height= static_cast<int> (matrix.size());
  auto board_width = static_cast<int> (matrix[0].size());
  for (int row = 0; row < board_height; row++){
    for (int col = 0; col < static_cast<int> (matrix[0].size());col++){
      // if statement 1; checks horizontal
      if (col <= board_width - 4 && tile == matrix[row][col] && tile == matrix[row][col+1] && tile == matrix[row][col+2] && tile == matrix[row][col+3]){
        continueplaying = false; 
      }
      // if statement 2; checks vertical
      if (row <= board_height - 4 && tile == matrix[row][col] && tile == matrix[row+1][col] && tile == matrix[row+2][col] && tile == matrix[row+3][col]){
        continueplaying = false; 
      }
      // if statement 3, checks diagonal to bottom right
      if( row <= board_height-4 && col <= board_width-4 ){
        if( tile == matrix[row][col] && tile == matrix[row+1][col+1] && tile == matrix[row+2][col+2] && tile == matrix[row+3][col+3] ){
          continueplaying = false;
        }
      }
      // if statement 4, checks diagonal to bottom left
      if( row <= board_height-4 && col >= board_width-4 ){
        if( tile == matrix[row][col] && tile == matrix[row+1][col-1] && tile == matrix[row+2][col-2] && tile == matrix[row+3][col-3] ){
          continueplaying = false; 
        }
      }
    }
  }
  // this function originally had nested for-loops for every if statement, but was later changed to only have 1 set of nested for-loops and some nested if-statements to improve run-time 
  return continueplaying;
}
//requires stringmatrix
//if there are strings left in the matrix that are not chips, the matrix is not full and will return that it is not a tie yet
auto checkTie(stringmatrix matrix) -> bool {
  for (int i = 0; i < static_cast<int> (matrix.size()); i++){
    for (int j = 0; j < static_cast<int> (matrix[0].size()); j++){
      if (matrix[i][j] != "X" && matrix[i][j] != "O"){
        return false; 
      }
    }
  }
  return true; 
}// function was added on later to improve user experience; even though the users will probably be aware of a tie in the event that it happens, having the program accounce it feels more official 

// next steps: include graphics (e.g. animations of chips getting dropped in particular spots), algorithm that allows player to play against computer (with customizable levels of difficulty)
auto main() -> int {
  //make a starting matrix
    //ask players their names and welcome them -- feature that was added on later to improve user experience  
  string player1Name;
  string player2Name;
  cout << "Welcome to ConnectFour! Player 1 will go first and their token will be an X. Player 2 will go second and their token will be an O" << "\n" << "Player 1, please enter your name" << endl;
  cin >> player1Name; 
  cout<< "Player 2, please enter your name" << endl;
  cin >> player2Name;

  //initialize stringmatrix, empty board with no chips
  stringvector vector; 
  stringmatrix matrix;
  for (int i = 1; i <= 30; i++){
    vector.push_back(to_string(i));
    if (i %6 == 0){
      matrix.push_back(vector);
      vector.clear();
      // dividing by 6 ensures that each row will contain only 6 elements, no less/more
    }
  }
  DisplayMatrix(matrix);

  auto continueplaying = true; 
  auto whichPlayer = true;
  string playerMove;



  //change do while loop to only be written once, regardless of which player is playing
  while (continueplaying){
    //get player1 input, make sure its valid 
    //use do while loop because want to loop to run at least once before breaking
    do {
      cout << player1Name <<", where do you want to place your chip" << endl;
      cin >> playerMove; 
      whichPlayer = true; 
    } while (!checkInput (matrix, playerMove));
    // originally repeated the code inside the 'do' section twice (once before a while loop and another time inside it) -- we then used a do-while loop to reduce the number of lines in our code and increase our level of abstraction
    // place player1's token where desired 
    matrix = placeToken(playerMove, matrix, whichPlayer);
    DisplayMatrix(matrix);


  bool winnerStatement = checkWinner(continueplaying, matrix, whichPlayer);
  //since after player 1 places a chip that the game is over, we know player 1 won the game
  if (!winnerStatement){
    cout << "Congrats " << player1Name <<"! You won!" << endl;
  }

    // place player1's token in right place using placeToken()
    if (winnerStatement){
      do {
      cout << player2Name <<", where do you want to place your chip" << endl;
      cin >> playerMove; 
      whichPlayer = false; 
    } while (!checkInput (matrix, playerMove));
    //if input does not meet conditions, will continue to ask for a chip that follows the rules of the game
      matrix = placeToken(playerMove, matrix, whichPlayer);
      DisplayMatrix(matrix);
    
      winnerStatement = checkWinner(continueplaying, matrix, whichPlayer);
      //since returns continueplaying variable, it is false, meaning someone has won
      //since after player 2 places a chip that the game is over, we know player 2 won the game
      if (!winnerStatement){
      cout << "Congrats " << player2Name <<"! You won!" << endl;
      } 
    }
    // checks if the entire gameboard is filled without a winner - then it will result in a tie
    continueplaying = winnerStatement;
    if (checkTie(matrix)){
        cout << "There is a tie, the game is over." << endl;
        continueplaying = false; 
      }
  }
} 
//future improvements:
// show how the winner won(highlight the row/column/diagonal they won with)
// different colours for different players, would be easier to differentiate who is playing where
//if placed a chip with nothing to support it, should drop to the nearest index in that column
