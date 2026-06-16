#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main()
{
    char choice[] = {'x', 'o'};
    int prows, pcols, crows, ccols, turns = 0;
    int rows = 3;
    int cols = 3;
    char grid[rows][cols];
    bool gameover = false;
    char userchoice, compchoice, option;
    char computer, player;

    for (int i = 0; i < rows; ++i)
    {
        for (int j = 0; j < cols; ++j)
        {
            grid[i][j] = '-';
        }
    }
    srand(time(0));

    cout << "Type 'M' if you want the first chance or 'C' if you want the computer to have the first chance: \n";
    cin >> option;

    cout << "Do you choose X or O?\n";
    cin >> userchoice;
    compchoice = (userchoice == 'X') ? 'O' : 'X';
    player = userchoice;
    computer = compchoice;

    while (turns < 9 && !gameover)
    {
        if (option == 'M')
        {
            do
            {
                cout << "Enter the row and coloumn where you want your chosen symbol\n";
                cin >> prows >> pcols;

            } while (grid[prows][pcols] != '-');

            grid[prows][pcols] = userchoice;
            turns++;
            option = 'C';
        }

        else if (option == 'C')

        {
            if (grid[0][0] == player || grid[2][2] == player || grid[2][0] == player || grid[0][2] == player)
            {
                if (grid[crows][ccols] != '-')
                {
                    cout << "Computer chose: 1st row and 1st coloumn";
                    grid[1][1] = computer;
                }

                turns++;
                option = 'M';
            }

            else if (userchoice == grid[1][1])
            {
                if (grid[crows][ccols] != '-')
                {
                    cout << "Computer chooses: " << crows << ccols;
                    grid[2][2] = computer || grid[2][0] = computer || grid[0][2] = computer;
                }
                turns++;
                option = 'M';
            }

            else
            {
                do
                {
                    crows = rand() % 3;
                    ccols = rand() % 3;
                } while (grid[crows][ccols] != '-');

                cout << "Computer chose: " << crows << ", " << ccols;
                grid[crows][ccols] = compchoice;
                turns++;
                option = 'M';
            }
        }
        cout << "\nCurrent grid:\n";
        for (int i = 0; i < rows; ++i)
        {
            for (int j = 0; j < cols; ++j)
            {
                cout << grid[i][j] << " ";
            }

            cout << endl;
        }

        for (int j = 0; j < cols; ++j)
        {
            char first = grid[0][j];
            if (first == '-')
                continue;

            bool same = true;
            for (int i = 1; i < rows; ++i)
            {

                if (grid[i][j] != first)
                {
                    same = false;
                    break;
                }
            }

            if (same)
            {
                cout << "coloumn" << j << " is full" << "-Player" << ((first == player) ? player : computer);
                gameover = true;
                break;
            }
        }

        for (int i = 0; i < rows; ++i)
        {
            char first = grid[i][0];
            if (first == '-')
                continue;

            bool same = true;
            for (int j = 1; j < cols; ++j)
            {

                if (grid[i][j] != first)
                {
                    same = false;
                    break;
                }
            }

            if (same)
            {
                cout << "Row" << i << " is full" << "-Player" << ((first == userchoice) ? userchoice : compchoice);
                gameover = true;
                break;
            }
        }

        char maindiag = grid[0][0];
        if (maindiag != '-' && maindiag == grid[1][1] && maindiag == grid[2][2])
        {
            cout << "Maindiagonal is full of" << maindiag << "-Player" << ((maindiag == userchoice) ? userchoice : compchoice);
            gameover = true;
        }

        char antidiag = grid[0][2];
        if (antidiag != '-' && antidiag == grid[1][1] && antidiag == grid[2][0])
        {
            cout << "Antidiagonal is full of" << antidiag << "-Player" << ((antidiag == userchoice) ? userchoice : compchoice);
            gameover = true;
        }

        if (userchoice == grid[1][1])
        {
            compchoice = grid[2][2];
            cout << "Computer chose " << grid[2][2];
        }
        while (grid[2][2] == '-')
            ;
    }

    return 0;
}
