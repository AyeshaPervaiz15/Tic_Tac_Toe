//C Program to Play the Tic Tac Toe Game

#include <stdio.h>
#include <stdbool.h>
// 2D-array Declared
char board[3][3];
  
// Function-> initialize the game board
void initializeBoard()
{int count = 1;
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            board[i][j] = ' ';
            printf("%d", count++);
            if (j < 2)
            {
                printf("  |  ");
            }
            
        }
        if (i < 2)
        printf("\n_____+_____+_____\n  ");
    }
   
    printf("\n\n\n");
    
}
// Function ->update the game board after every turn
int updateBoard(int box, char playerSign)
{
    int row = (box - 1) / 3;
    int col = (box- 1) % 3;
    bool isValid = true;           
    if (board[row][col] != ' ')
    {
        printf("\nInvalid: cell is filled\n");
        isValid = false;
    }
    else
    {
        board[row][col] = playerSign;
    }
    showBoard(row, col);
 
    return isValid;
}
 

 
// Function ->shows the game board after every turn
void showBoard(int x, int y)
{
    printf("\n");
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            printf("%c", board[i][j]);
            if (j < 2)
            {
                printf("  |  ");
            }
        }
        if (i < 2)
        printf("\n_____+_____+_____\n ");
    }
    printf("\n\n\n");
}
 

// Function-> check the winner of the game
int checkWinner(char w)
{
    // check all rows
    if (board[0][0] == w && board[0][1] == w && board[0][2] == w ||
      board[1][0] == w && board[1][1] == w && board[1][2] == w ||
      board[2][0] == w && board[2][1] == w && board[2][2] == w)
    {
        return 1;
      }
      // check all columns
    else if (board[0][0] == w && board[1][0] == w && board[2][0] == w ||
           board[0][1] == w && board[1][1] == w && board[2][1] == w ||
           board[0][2] == w && board[1][2] == w && board[2][2] == w)
    {
        return 1;
    }
    // check both diagonals
    else if (board[0][0] == w && board[1][1] == w && board[2][2] == w ||
           board[0][2] == w && board[1][1] == w && board[2][0] == w)
    {
        return 1;
    }
 
    //  no winner
    return 0;
}
 
// Start game 
void TicTacToe()
{
    int gameResult = 0;
    int box = 0;
    int playCount = 0;
    int updationResult = 1;
    char playerSign = ' ';
 
    // start playing the game
    while (!gameResult && playCount < 9)
    {
        if (playCount % 2 == 0)
        {
            // player 1
            printf("\nPlayer 1 [ X ] : ");
            playerSign = 'X';
        }
        else
        {
            // player 2
            printf("\nPlayer 2 [ O ] : ");
            playerSign = 'O';
        }
        scanf("%d", &box);
        if (box > 0 && box < 10)
        {
            updationResult = updateBoard(box, playerSign);
            // if updation is possible
            if (updationResult)
            {
                gameResult = checkWinner(playerSign);
                // print the winner of the game
                if (gameResult)
                {
                    printf("Player %d Won\n", playerSign == 'X' ? 1 : 2);
                }
                playCount++;
            }
        }
        else if (box == -1)
        {
            printf("\nGame Terminated\n");
            return;
        }
        else
        {
            printf("\nPlease Enter a valid box value\n");
        }
    }
 
    // no one won 
    if (!gameResult && playCount == 9)
    {
        printf("\n Game Draw \n");
    }
    printf("\n Game Over \n");
}
 
int main()
{
    printf("Tic Tac Toe\n");
    printf("Instructions: \n");
    printf("\tPlayer 1 sign = X\n");
    printf("\tPlayer 2 sign = O");
    printf("\n\tTo exit from game, Enter -1\n");
 
    printf("\nNumbers on Board\n\n");
    initializeBoard();
 
    char start = ' ';
    printf("Press Enter to start\n");
    scanf("%c", &start);
 
    if (start)
    {
        int userChoice = 1;
        // To restart the game
        while (userChoice!=0)
        {
            TicTacToe();
            printf("\nPress 1 to Restart");
            printf("\nPress 0 for Exit");
            
            printf("\n\tChoice: ");
            scanf("%d", &userChoice);
            if (userChoice)
            {
                initializeBoard();
            }
            printf("\n");
        }
    }
   
    return 0;
}