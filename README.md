# tic-tac-toe
a code that allows one to play an engaging game of tic tac toe with the computer

#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>
#include <time.h>

char board[3][3];
const char PLAYER ='X';
const char COMP = 'O';

void reset_board();
void print_board();
int check_free_spaces();
void player_move();
void comp_move();
char check_winner();
void print_winner(char);

int main ()
{
    char winner = ' ';
    char response;

    do
    {
        winner = ' ';
        response = ' ';
        reset_board();

    while(winner == ' ' && check_free_spaces() != 0)
    {
        print_board();
        player_move();
        winner = check_winner();
        if(winner != ' ' || check_free_spaces() == 0)
        {
            break;
        }
        comp_move();
        winner = check_winner();
        if(winner != ' ' || check_free_spaces() == 0)
        {
            break;
        }
    }

    print_board();
    print_winner(winner);
    printf("would you like to play again! (Y/N):\n ");
    scanf("%c");
    scanf("%c", &response);
    response = toupper(response);
       
    } while (response == 'Y');

printf("/n thanks for playing!");
    return 0;
}

void reset_board()
{
    for(int i = 0; i < 3; i++)
    {
        for(int j = 0; j < 3; j++)
        {
            board[i][j] = ' ';
        }
    }

}
void print_board()
{
    printf(" %c | %c | %c",board[0][0],board[0][1],board[0][2]);
    printf("\n***|***|***\n");
    printf(" %c | %c | %c",board[1][0],board[1][1],board[1][2]);
    printf("\n***|***|***\n");
    printf(" %c | %c | %c",board[2][0],board[2][1],board[2][2]);
    printf("\n");

}
int check_free_spaces()
{
    int free_spaces = 9;

    for(int i = 0; i < 3; i++)
    {
        for(int j = 0; j < 3; j++)

        {
            if(board[i][j] != ' ')
            {
            free_spaces--;
            }
        }
            
    }
    return free_spaces;
}
        
void player_move()
{
    int x;
    int y;

    do
    {
        printf("enter row number 1-3: ");
        scanf("%d", &x);
        x--;

        printf("enter column number 1-3: ");
        scanf("%d", &y);
        y--;

        if(board[x][y] != ' ')
        {
            printf("invalid move!\n");
        }
        else
        {
            board[x][y] = PLAYER;
            break;
        }
    }while (board[x][y] != ' ');

}
void comp_move()
{
    // creat a seed based on current time
    srand(time(0));
    int x;
    int y;

    if(check_free_spaces()>0)
    {
        do
        {
            x = rand() % 3;
            y = rand() % 3;
        } while (board[x][y] != ' ');

        board[x][y] = COMP;        
    }
    else
    {
        print_winner(' ');
    }
}
char check_winner()
{
    // checks rows
    for(int i = 0; i<3; i++)
    {
        if(board[i][0] == board[i][1] && board[i][0] == board[i][2])
        {
            return board[i][0];
        }
    }
// check columns
for(int i = 0; i<3; i++)
    {
        if(board[0][i] == board[1][i] && board[0][i] == board[2][i])
        {
            return board[0][1];
        }
    }
// check diagonals
if(board[0][0] == board[1][1] && board[0][0] == board[2][2])
    {
        return board[0][0];
    }
if(board[0][2] == board[1][1] && board[0][0] == board[2][0])
    {
        return board[0][2];
    }

return ' ';

}
void print_winner(char winner)
{
    if(winner == PLAYER)
    {
        printf("YOU WIN!");
    }
    else if(winner == COMP)
    {
        printf("COMPUTER WINS!");
    }
    else
    {
        printf("ITS A TIE!");
    }

}


