/*
    PROJECT TITANIC BY:
        214/CO/15 - ADITYA NAND
        218/CO/15 - AKHILESH NAIDU
        220/CO/15 - AKSHAYE SINGHI
*/
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <time.h>
#include <ctype.h>

void delay(int mseconds)
{
    clock_t goal = mseconds + clock();
    while (goal > clock());
}
void disp1(int j)
{
    static int k=0;
    if(k<=100)
        printf("\n\n\n\n\n\n\n\t\t\t\tLoading Application   %d%c",j,37);
    else
        printf("\n\n\n\n\n\n\n\t\t\tPreparing your Battle Ground   %d%c",j,37);
    k++;
}
void load_place_ship()
{
    int i;
    printf("\n\n\n\n\n\n\n\t\t\t\tPlacing your ship");
    for(i=0;i<4;i++)
    {
        delay(500);
        printf("\t%c",46);
    }
    system("cls");
}
void load_app()
{
    int i,j=0,t=150;
    for(j=0;j<=100;j++)
    {
        if(j==0)
        {
            disp1(j);
            delay(1500);
            system("cls");
        }
        else if(j<26)
        {
            disp1(j);
            delay(t);
            t=t-10;
            system("cls");
        }
        else if(j<100)
        {
            disp1(j);
            delay(t);
            system("cls");
        }
        else if(j==100)
        {
            disp1(j);
            delay(1000);
            system("cls");
        }
    }
}

int mat1[11][11], mat2[11][11], mat3[11][11], mat4[11][11];
//generate_coordinates(a,direction,x1,y1,5);

void display_grid(int e[][11]){    // Display of the grid while placing the ship
    int i, j;
    for(i=0; i<11; i++){
        printf("\t\t\t    ");
        for(j=0; j<11; j++){
            if(i==0 && j==0)
                printf("  ");
            else
            if(i==0 || j==0)
                if(i==0)
                    printf("%d ",j-1);
                else
                    printf("%d ",i-1);
            else
                printf("%d ",e[i][j]);
        }
        printf("\n");
    }
}
void display_grid1(int d[][11]){        // Display while playing the game
    int i, j;
    for(i=0; i<11; i++){
        printf("\t\t\t    ");
        for(j=0; j<11; j++){
            if(i==0 && j==0)
                printf("  ");
            else
            if(i==0 || j==0)
                if(i==0)
                    printf("%d ",j-1);
                else
                    printf("%d ",i-1);
            else{
                if(d[i][j])
                    printf("%c ",d[i][j]);
                else
                    printf("- ");
            }
        }
        printf("\n");
    }
}
void place_ship(int c[][11], int p, int q, int r, int s){  // Aircraft carrier and Submarine.
    int i;
    if(p==q){
        if(r<s)
            for(i=r; i<=s; i++)
                c[p][i]++;
        else
            for(i=s; i<=r; i++)
                c[p][i]++;
    }
    else{
        if(p<q)
            for(i=p; i<=q; i++)
                c[i][r]++;
        else
            for(i=q; i<=p; i++)
            c[i][r]++;
    }
    system("cls");   // To clear the screen; It's getting interesting code by code..!!!!!!!
    load_place_ship();
    printf("\n\n\n");
    display_grid(c);
    printf("\t\n\nPlace your ship in the grid. Make sure your ENEMY can't see it..!! \n");
    printf("\tShips will be placed as following:- \n");
    printf("\t1. Aircraft Carrier (5 blocks). \n");
    printf("\t2. Battleship (4 blocks). \n");
    printf("\t3. Destroyer (4 blocks). \n");
    printf("\t4. Submarine (3 blocks). \n");
    printf("\t5. Tug Boat (2 blocks). \n\n\n");
}

void place_ship1(int b[][11], int p, int q, int r, int s){  // All the other ships
    int found=1; char direct;
    static int count; count=0;
    do{
        int i;
        if(found==0){
           printf("\tEnter the starting vertical co-ordinate: ");
           scanf("%d",&p);
           printf("\tEnter the starting horizontal co-ordinate: ");
           scanf("%d",&q);
           printf("\tEnter direction 'w', 'a', 's', 'd': ");
           direct=getch();
           p++;q++;
           found=1;
           if(count<2){
                int found, size; found=1; size=4;
                tolower(direct);
                do{
                    if(found==0){
                        printf("\tEnter the starting vertical co-ordinate: ");
                        scanf("%d",&p);
                        printf("\tEnter the starting horizontal co-ordinate: ");
                        scanf("%d",&r);
                        printf("\tEnter direction 'w' 'a' 's' 'd': ");
                        direct=getch();
                        p++;r++;
                        tolower(direct);
                        found=1;
                    }
                    if((p<1 || p>10) || (r<1 || r>10))
                        found=0;
                    else{
                        switch(direct){
                            case 'w':
                                q=p-size+1;
                                if(q<1)
                                    found=0;
                                s=r;break;
                            case 'a':
                                s=r-size+1;
                                if(s<1)
                                    found=0;
                                q=p;break;
                            case 's':
                                q=p+size-1;
                                if(q>10)
                                    found=0;
                                s=r;break;
                            case 'd':
                                s=r+size-1;
                                if(s>10)
                                    found=0;
                                q=p;break;
                        }
                    }
                    if(found==0){
                        printf("\n\n\tInvalid input in generation");
                        printf("\n\tPlease enter co-ordinates again! \a\n\n\n");
                    }
                }while(found==0);
           }
           else{
                int found, size; found=1; size=2;
                tolower(direct);
                do{
                    if(found==0){
                        printf("\tEnter the starting vertical co-ordinate: ");
                        scanf("%d",&p);
                        printf("\tEnter the starting horizontal co-ordinate: ");
                        scanf("%d",&r);
                        printf("\tEnter direction 'w' 'a' 's' 'd': ");
                        direct=getch();
                        p++;r++;
                        tolower(direct);
                        found=1;
                    }
                    if((p<1 || p>10) || (r<1 || r>10))
                        found=0;
                    else{
                        switch(direct){
                            case 'w':
                                q=p-size+1;
                                if(q<1)
                                    found=0;
                                s=r;break;
                            case 'a':
                                s=r-size+1;
                                if(s<1)
                                    found=0;
                                q=p;break;
                            case 's':
                                q=p+size-1;
                                if(q>10)
                                    found=0;
                                s=r;break;
                            case 'd':
                                s=r+size-1;
                                if(s>10)
                                    found=0;
                                q=p;break;
                        }
                    }
                    if(found==0){
                        printf("\n\n\tInvalid input in generation");
                        printf("\n\tPlease enter co-ordinates again! \a\n\n\n");
                    }
                }while(found==0);
           }
        }
        if(p==q){
                if(r<s){
                    for(i=r; i<=s; i++){
                        b[p][i]++;
                        if(b[p][i]>1){
                            while((i-r)>=0)
                               b[p][i--]--;
                            found=0;
                            break;
                        }
                    }
                }
                else{
                    for(i=s; i<=r; i++){
                        b[p][i]++;
                        if(b[p][i]>1){
                            while((i-s)>=0)
                               b[p][i--]--;
                            found=0;
                            break;
                        }
                    }
                }
                if(found==0){
                    printf("\n\n\tInvalid input ");
                    printf("\n\tPlease enter co-ordinates again! \a\n\n\n");
                }
        }
        else
        if(r==s){
            if(p<q){
                for(i=p; i<=q; i++){
                    b[i][r]++;
                    if(b[i][s]>1){
                        while((i-p)>=0)
                            b[i--][s]--;
                        found=0;
                        break;}
                }
            }
            else{
                for(i=q; i<=p; i++){
                    b[i][r]++;
                    if(b[i][s]>1){
                        while((i-q)>=0)
                            b[i--][s]--;
                        found=0;
                        break;
                    }
                }
            }
            if(found==0){
                printf("\n\n\tInvalid input ");
                printf("\n\tPlease enter co-ordinates again! \a\n\n\n");
            }
        }
    }while(found==0);
    system("cls");   // To clear the screen; It's getting interesting code by code..!!!!!!!
    load_place_ship();
    count++;
    printf("\n\n\n");
    display_grid(b);
    printf("\t\n\n Place your ship in the grid. Make sure your ENEMY can't see it..!! \n");
    printf("\tShips will be placed as following:- \n");
    printf("\t1. Aircraft Carrier (5 blocks). \n");
    printf("\t2. Battleship (4 blocks). \n");
    printf("\t3. Destroyer (4 blocks). \n");
    printf("\t4. Submarine (3 blocks). \n");
    printf("\t5. Tug Boat (2 blocks). \n\n\n");
}
void generate_coordinates(int a[][11], char d, int r1, int c1, int size){
    int r2, c2, found; found=1;
    tolower(d);
    do{
        if(found==0){
            printf("\tEnter the starting vertical co-ordinate: ");
            scanf("%d",&r1);
            printf("\tEnter the starting horizontal co-ordinate: ");
            scanf("%d",&c1);
            printf("\tEnter direction 'w' 'a' 's' 'd': ");
            d=getch();
            r1++;c1++;
            tolower(d);
            found=1;
        }
        if((r1<1 || r1>10) || (c1<1 || c1>10))
            found=0;
        else{
            switch(d){
                case 'w':
                    r2=r1-size+1;
                    if(r2<1)
                        found=0;
                    c2=c1;break;
                case 'a':
                    c2=c1-size+1;
                    if(c2<1)
                        found=0;
                    r2=r1;break;
                case 's':
                    r2=r1+size-1;
                    if(r2>10)
                        found=0;
                    c2=c1;break;
                case 'd':
                    c2=c1+size-1;
                    if(c2>10)
                        found=0;
                    r2=r1;break;
            }
        }
        if(found==0){
            printf("\n\n\tInvalid input in generation");
            printf("\n\tPlease enter co-ordinates again! \a\n\n\n");
        }
    }while(found==0);
    if(size==5 || size==3)
        place_ship(a,r1,r2,c1,c2);
    else
        place_ship1(a,r1,r2,c1,c2);
}
void play_game(){   // Playing of the game, unknown to user.
    system("cls");
    int r1, r2, x, y;
    r1=0; r2=0;
    char p1[9]="PLAYER 1";
    char p2[9]="PLAYER 2";
    while(1){
        int re_chance; re_chance=0;
        printf("\n\nPress any key...!!!\n\n");
        getch();
        do{
            system("cls");
            delay(1250);
            printf("\n\n\n");
            printf("%43s",p1);
            printf("\n\n\n");
            display_grid1(mat3);
            printf("\n\n");
            do{
                printf("\t ENTER THE VERTICAL CO-ORDINATE OF THE TARGET BLOCK: ");
                scanf("%d",&x);
                printf("\t ENTER THE HORIZONTAL CO-ORDINATE OF THE TARGET BLOCK: ");
                scanf("%d",&y);
                printf("\n\n");
            }while((x<0 && x>9) && (y<0 && y>9));
            re_chance=0;
            if(mat2[x+1][y+1]){
                mat2[x+1][y+1]--;
                mat3[x+1][y+1]=88;
                r1++;
                printf("\a");
                re_chance=1;
            }
            else{
                if(mat2[x+1][y+1]!='X'){
                    printf("\n\n\t\t\t MISSED \n\n");
                    mat3[x+1][y+1]=111;
                }
            }
        }while((re_chance!=0) && (r1!=18));
        if(r1==18)
            break;
        printf("\n\nPress any key...!!!\n\n");
        getch();
        do{
            system("cls");
            delay(1250);
            printf("\n\n\n");
            printf("%43s",p2);
            printf("\n\n\n");
            display_grid1(mat4);
            printf("\n\n");
            do{
                printf("\t ENTER THE VERTICAL CO-ORDINATE OF THE TARGET BLOCK: ");
                scanf("%d",&x);
                printf("\t ENTER THE HORIZONTAL CO-ORDINATE OF THE TARGET BLOCK: ");
                scanf("%d",&y);
            }while((x<0 && x>9) && (y<0 && y>9));
            re_chance=0;
            if(mat1[x+1][y+1]){
                mat1[x+1][y+1]--;
                mat4[x+1][y+1]=88;
                r2++;
                printf("\a");
                re_chance=1;
            }
            else{
                if(mat1[x+1][y+1]!='X'){
                    printf("\n\n\t\t\t MISSED \n\n");
                    mat4[x+1][y+1]=111;
                }
            }
        }while((re_chance!=0) && (r2!=18));
        if(r2==18)
            break;
    }
    if(r1==18)
        printf("\n\n\t\t\t   PLAYER 1 WINS\n");
    else
        printf("\n\n\t\t\t   PLAYER 2 WINS\n");
}
void enter_ship(int a[][11]){  // Entering of ships
    int x1, y1;
    char direction;
    int ch=1;
    do{
        printf("\tPlace your ship in the grid. Make sure your ENEMY can't view it..!! \n");
        printf("\tShips will be placed as following:- \n");
        printf("\t1. Aircraft Carrier (5 blocks). \n");
        printf("\t2. Battleship (4 blocks). \n");
        printf("\t3. Destroyer (4 blocks). \n");
        printf("\t4. Submarine (3 blocks). \n");
        printf("\t5. Tug Boat (2 blocks). \n\n\n");
        switch(ch){
            case 1:
                printf("\tPlace your Aircraft Carrier\n");
                printf("\tEnter the starting vertical co-ordinate: ");
                scanf("%d",&x1);
                printf("\tEnter the starting horizontal co-ordinate: ");
                scanf("%d",&y1);
                printf("\tEnter direction 'w', 'a', 's', 'd': ");
                direction=getch();
                x1++;y1++;
                generate_coordinates(a,direction,x1,y1,5);
                ch++;
            case 2:

                printf("\tPlace your Battleship\n");
                printf("\tEnter the starting vertical co-ordinate: ");
                scanf("%d",&x1);
                printf("\tEnter the starting horizontal co-ordinate: ");
                scanf("%d",&y1);
                printf("\tEnter direction 'w' 'a' 's' 'd': ");
                direction=getch();
                x1++;y1++;
                generate_coordinates(a,direction,x1,y1,4);
                ch++;
            case 3:

                printf("\tPlace your Destroyer\n");
                printf("\tEnter the starting vertical co-ordinate: ");
                scanf("%d",&x1);
                printf("\tEnter the starting horizontal co-ordinate: ");
                scanf("%d",&y1);
                printf("\tEnter direction 'w' 'a' 's' 'd': ");
                direction=getch();
                x1++;y1++;
                generate_coordinates(a,direction,x1,y1,4);
                ch++;
            case 4:

                printf("\tPlace your Submarine\n");
                printf("\tEnter the starting vertical co-ordinate: ");
                scanf("%d",&x1);
                printf("\tEnter the starting horizontal co-ordinate: ");
                scanf("%d",&y1);
                printf("\tEnter direction 'w' 'a' 's' 'd': ");
                direction=getch();
                x1++;y1++;
                generate_coordinates(a,direction,x1,y1,3);
                ch++;
            case 5:

                printf("\tPlace your Tug Boat\n");
                printf("\tEnter the starting vertical co-ordinate: ");
                scanf("%d",&x1);
                printf("\tEnter the starting horizontal co-ordinate: ");
                scanf("%d",&y1);
                printf("\tEnter direction 'w' 'a' 's' 'd': ");
                direction=getch();
                x1++;y1++;
                generate_coordinates(a,direction,x1,y1,2);
                ch++;
        }

    }while(ch!=6);
}
void play(){  // User display of the game play
    printf("\n\n\n");
    char p1[9]="PLAYER 1";
    char p2[9]="PLAYER 2";
    printf("%43s",p1);
    printf("\n\n\n");
    display_grid(mat1);
    printf("\n");
    enter_ship(mat1);
    system("cls");  // Player 2 starts placing his ships...!!!
    printf("\n\n\n");
    display_grid(mat1);
    printf("\n\nPress any key to continue...!!!\n\n");
    getch();
    system("cls");
    printf("Now handover the laptop to player 2\n\n");
    delay(3500);
    load_app();
    printf("%43s",p2);
    printf("\n\n\n");
    display_grid(mat2);
    printf("\n");
    enter_ship(mat2);
    system("cls");
    display_grid(mat1);
    printf("\n\nPress any key to continue...!!!\n\n");
    getch();
    system("cls");
    // preparing the board
    play_game();
    getch();
}
void instructions(){
    printf("\n\n\n");
    printf("\t\t\t        INSTRUCTIONS\n\n\n");
    printf("\n\n In this game, there will be 2 players. Each will have their own set of ships to place.\n\t The following are the ships that you can use : \n\t 1.Aircraft Carrier <5 blocks>\n\t 2.Battleship <4 blocks>\n\t 3.Destroyer <4 blocks>\n\t 4.Submarine <3 blocks>\n\t 5.Tug Boat <2 blocks>");
    printf("\n\n Players have to first place the ships in their respective grids. \n\n After placing the ships, each player must now target the opponent ships by     guessing its location and entering the co-ordinates.\n");
    printf("\n\n If it is a hit then the player gets another chance unless he misses the target upon which the opponent player gets his chance. \n\n The player that sinks all the ships first wins!\n");
    printf("\n\n\n\n The following is the grid, where each ' - ' or  '0' is the block :   \n\n");
    display_grid1(mat3);
    printf("\n\n\n\n Look at the following example to enter co-ordinates for aircraft carrier. \n\n Eg:Enter the starting vertical co-ordinate: 2 \n    Enter the starting horizontal co-ordinate: 3 \n    Enter direction 'w' 'a' 's' 'd': s");
    printf("\n\n\n    0 1 2 3 4 5 6 7 8 9            \n  0 - - - - - - - - - -           \n  1 - - - - - - - - - -           \n  2 - - - 1 - - - - - -           \n  3 - - - 1 - - - - - -           \n  4 - - - 1 - - - - - -           \n  5 - - - 1 - - - - - -           \n  6 - - - 1 - - - - - -           \n  7 - - - - - - - - - -           \n  8 - - - - - - - - - -           \n  9 - - - - - - - - - - ");
    printf("\n      One small twist though, submarine can be placed below another ship unlike others...!!! \n\n BEST OF LUCK! ");
    getch();
    load_app();
    play();
}
int main(){

    char title[11]="BATTLESHIP";
    int ch;
    load_app();
    do{
        system("cls");
        printf("\n\n\n");
        printf("%46s",title);
        printf("\n Enter your choice\n  1.Play\n  2.Instructions\n  3.Exit\n\n");
        scanf("%d",&ch);
        switch(ch){
        case 1:
            system("cls");
            load_app();
            play();break;
        case 2:
            system("cls");
            instructions();break;
        case 3:
            system("cls");
            printf("\n\n\n\n\n\n\n\n\n\n\t\t\t\t    THANK YOU\n\n\n\n\n\n\n\n\a\n\n\n\n\n\n\n\n\n\n");
            getch();
            exit(0);
        }
    }while(ch!=3);

    return 0;
}
/*
2 3, 2 7
3 3, 3 6
4 3, 4 6
2 3, 2 5
8 9, 9 9
*/
