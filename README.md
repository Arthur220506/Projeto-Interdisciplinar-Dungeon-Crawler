#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define RED "\x1b[31m"
#define RESET "\x1b[0m"

// Variáveis Globais
const char PLAYER_CHAR = '&';
const char KEY_CHAR = '@';
const char MONSTER_CHAR = 'X';
const char MONSTER2_CHAR = 'V';
const char CLOSED_DOOR = 'D';
const char OPENED_DOOR = '=';
const char SPIKE_CHAR = '#';
const char BUTTON_CHAR = 'O';

char key_pressed;
int playerX = 1, playerY = 1;
int monsterX, monsterY;
int tem_chave;
int keyX, keyY;
int tela = 0;
int coord_X, coord_Y;
int vidas;
int button_pressed;

// Funções do Jogo
void playerMovement(char key_pressed, int limit)
{
    if (key_pressed == 'q')
    {
        tela = 0;
        main();
    }
    if (key_pressed == 'w' && playerX - 1 != 0 && playerX - 1 != limit)
    {
        playerX--;
    }
    if (key_pressed == 's' && playerX + 1 != 0 && playerX + 1 != limit)
    {
        playerX++;
    }
    if (key_pressed == 'a' && playerY - 1 != 0 && playerY - 1 != limit)
    {
        playerY--;
    }
    if (key_pressed == 'd' && playerY + 1 != 0 && playerY + 1 != limit)
    {
        playerY++;
    }
}
void levelWalls(int xLimit, int yLimit, char level[xLimit][yLimit])
{
    for (int x = 0; x < xLimit; x++)
    {
        for (int y = 0; y < yLimit; y++)
        {
            if (x == 0 || x == xLimit - 1 || y == 0 || y == yLimit - 1)
            {
                level[x][y] = '*';
            }
            else
            {
                level[x][y] = ' ';
            }
        }
    }
}
void print_level(int xLimit, int yLimit, char level[xLimit][yLimit])
{
    for (coord_X = 0; coord_X < xLimit; coord_X++)
    {
        for (coord_Y = 0; coord_Y < yLimit; coord_Y++)
        {
            printf(" %c", level[coord_X][coord_Y]);
        }
        printf("\n");
    }
}
void gameOver(char level[20][20]) 
{
    if (level[playerX][playerY] == SPIKE_CHAR || playerX == monsterX && playerY == monsterY) {
        system("cls");
        playerY = 1;
        playerX = 1;
        tem_chave = 0;
        vidas--;

        if (vidas == 0) {
            printf(
                "voce foi pego 3 vezez tentando fugir e agora esta na solitaria \n"
                "talvez em outro momento voce consiga fugir \n"
                "\n"
            );
            system("pause");
            tela = 0;
            main();
        }
        printf("voce foi pego |tentativas restantes: %d\n\n", vidas);

        system("pause");
    }
}
int main()
{
    vidas = 3;
    srand(time(NULL));

    // Declaração de variavéis

    int choice;

    int monstermov;

    // Inicializando matrizes
    char level1[10][10];

    char level2[20][20];
    // char level3[40][40];
    levelWalls(10, 10, level1);
    levelWalls(20, 20, level2);

    // Loop do Menu
    while (tela == 0)
    {
        system("cls");
        printf("%s        ****  *****      **     *     *  *    *  *******   *******  *******  *    *%s \n", RED, RESET);
	    printf("%s        *   * *   *      * *    *     *  * *  *  *         *        *     *  * *  *%s \n", RED, RESET);
		printf("%s        ****  *****      *   *  *     *  *  * *  *  ****   *******  *     *  *  * *%s \n", RED, RESET);
		printf("%s        *   * *  *       * *    *     *  *   **  *     *   *        *     *  *   **%s \n", RED, RESET);
		printf("%s        ****  *   *      **     *******  *    *  *******   *******  *******  *    *%s \n\n\n\n", RED, RESET);
	    printf("   1-jogar\n\n\n   2-tutorial\n\n\n   3-sair\n\n\n");
        choice = getch();

        if (choice == '1')
        {
            system("cls");

            // Todo: Adicionar introdução da história aqui
            printf("em uma madrugada silenciosa, o ze do crime tentou escapar de carandiru\n\n\n");

            system("pause");
            tela = 1;
            system("cls");
        }
        else if (choice == '2')
        {
            system("cls");
            printf(
                "Certo, aqui estao algumas instrucoes:\n\n"
                "Passe por tres setores do presidio coletando 3 chaves e evitando os guardas para conseguir sua liberdade.\n\n"
                "em cada nivel, o jogador precisa se mover para coletar uma chave e abrir uma porta fechada.\n\n"
                "para completar a missao use os seguntes comandos:\n\n\n"
                "W: se mova uma unidade para cima\n\n"
                "A: se mova uma unidade para esquerda\n\n"
                "S: se mova uma unidade para baixo\n\n"
                "D: se mova uma unidade para direita\n\n"
                "I: interage com um objeto\n\n"
				"@: chave da porta\n\n"
				"X: guarda noturno\n\n"
				"&: Ze do crime\n\n");
            system("pause");
        }
        else if (choice == '3')
        {
            system("cls");
            printf("voce nao tem a coragem necessaria para fugir ne?.");
            return 0;
        }
        else
        {
            printf("coloque uma opcao valida!\n");
            system("pause");
        }
    }

    // Level 1 loop
    while (tela == 1)
    {
        monsterX = 6;
        monsterY = 6;
        keyX = 5;
        keyY = 5;

        monstermov = rand() % 4;
        if (monstermov == 0 && monsterX - 1 != 0 && monsterX - 1 != 9)
        {
            monsterX--;
        }
        if (monstermov == 1 && monsterX + 1 != 0 && monsterX + 1 != 9)
        {
            monsterX++;
        }
        if (monstermov == 2 && monsterY - 1 != 0 && monsterY - 1 != 9)
        {
            monsterY--;
        }
        if (monstermov == 3 && monsterY + 1 != 0 && monsterY + 1 != 9)
        {
            monsterY++;
        }

        level1[monsterX][monsterY] = MONSTER_CHAR;
        if (tem_chave == 0)
        {
            level1[9][5] = CLOSED_DOOR;
            level1[keyX][keyY] = KEY_CHAR;
        }
        if (tem_chave == 1)
        {
            level1[9][5] = OPENED_DOOR;
            level1[keyX][keyY] = ' ';
        }

        level1[playerX][playerY] = PLAYER_CHAR;
        print_level(10, 10, level1);

        level1[playerX][playerY] = ' ';
        level1[monsterX][monsterY] = ' ';

        key_pressed = getch();
        playerMovement(key_pressed, 9);

        if (playerX == keyX && playerY == keyY && key_pressed == 'i')
        {
            tem_chave = 1;
        }

        gameOver(level1);

        // Checando posição do player, se ele estiver em cima da porta aberta e apertar 's', avança
        if (playerX == 8 && playerY == 5 && tem_chave == 1 && key_pressed == 's')
        {
            tela = 2;
            system("cls");
            printf(
                "ze do crime conseguiu sair de dentro de sua sela\n"
                "agora ele tem que sair do patio de carandiru\n"
                "porem vai precisar liberar a chave que esta cheia de espinhos\n"
                "\n"
                "\n"
            );
            system("pause");
            playerX = 1, playerY = 1;
            tem_chave = 0;
        }
        system("cls");
    }

    // Loop da Fase 2
    while (tela == 2)
    {   
        // Declarando posições iniciais dos objetos

        monsterX = 10;
        monsterY = 17;
        keyX = 2;
        keyY = 8;
        
        // Lógica do botão, ele tenha sido pressionado, os espinhos envolta da chave sumirão
        if (button_pressed == 0)
        {
            level2[keyX-1][keyY] = SPIKE_CHAR;
            level2[keyX+1][keyY] = SPIKE_CHAR;
            level2[keyX][keyY-1] = SPIKE_CHAR;
            level2[keyX][keyY+1] = SPIKE_CHAR;
            level2[12][12] = BUTTON_CHAR;
        }
        else
        {
            level2[keyX-1][keyY] = ' ';
            level2[keyX+1][keyY] = ' ';
            level2[keyX][keyY-1] = ' ';
            level2[keyX][keyY+1] = ' ';
        }
        if (tem_chave == 0)
        {
            level2[19][5] = CLOSED_DOOR;
            level2[keyX][keyY] = KEY_CHAR;
        }
        else
        {
            level2[19][5] = OPENED_DOOR;
        }


        monstermov = rand() % 2;    
        if (monstermov == 0) 
        {
            if (playerY < monsterY && monsterY - 1 != 0) {
                monsterY--;
            } else if (playerY > monsterY && monsterY + 1 != 19) {
                monsterY++;
            }
        } 
        else 
        {
            if (playerX < monsterX && monsterX - 1 != 0) {
                monsterX--;
            } else if (playerX > monsterX && monsterX + 1 != 19) {
                monsterX++;
            }
        }

        // Colocando o player e monstro
        level2[playerX][playerY] = PLAYER_CHAR;
        level2[monsterX][monsterY] = MONSTER2_CHAR;

        print_level(20, 20, level2);

        if (playerX == 12 && playerY == 12)
        {
            button_pressed = 1;
            printf("a chave esta segura para ser coletada!\n");
        }

        level2[playerX][playerY] = ' ';
        level2[monsterX][monsterY] = ' ';
        key_pressed = getch();

        if (playerX == keyX && playerY == keyY && key_pressed == 'i')
        {
            tem_chave = 1;
            level2[19][5] = OPENED_DOOR;
        }
        if (playerX == 18 && playerY == 5 && tem_chave == 1 && key_pressed == 's'){
            system("cls");
            tela = 3;
            printf("em producao\n");
            system("pause");
        }
        playerMovement(key_pressed, 19);
        gameOver(level2);
        system("cls");

    }

    return 0;
}
