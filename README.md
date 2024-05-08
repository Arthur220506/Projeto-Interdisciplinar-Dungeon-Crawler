#include <stdio.h>
#include <stdlib.h>

#define RED "\x1b[31m"
#define RESET "\x1b[0m"


/* run this program using the console pauser or add your own getch, system("pause") or input loop */

int main() {
    // Variaveis 
    int i;
    int j;
    int tela = 0;
    int escolha;

    char level1[10][10];
    char level2[20][20];
    char level3[40][40];

    int move;
    int cord_X = 1, cord_Y = 1;

    int tem_chave = 0;
    char Porta_Fechada = 'D';
    char Porta_Aberta = '=';

    char Jogador = '&';
    char Chave = '@';
    char Monstro = 'X';

    // Matrizes 
    for (i = 0; i < 10; i++) {
        for (j = 0; j < 10; j++) {
            if (i == 0 || i == 9 || j == 0 || j == 9) {
                level1[i][j] = '*';
            } else {
                level1[i][j] = ' ';
            }
        }
    }

    // Menu
    while (tela == 0) {
        system("cls");
        printf("%s        ****  *****      **     *     *  *    *  *******   *******  *******  *    *%s \n", RED, RESET);
	    printf("%s        *   * *   *      * *    *     *  * *  *  *         *        *     *  * *  *%s \n", RED, RESET);
		printf("%s        ****  *****      *   *  *     *  *  * *  *  ****   *******  *     *  *  * *%s \n", RED, RESET);
		printf("%s        *   * *  *       * *    *     *  *   **  *     *   *        *     *  *   **%s \n", RED, RESET);
		printf("%s        ****  *   *      **     *******  *    *  *******   *******  *******  *    *%s \n\n\n\n", RED, RESET);
	    printf("   1-jogar\n\n\n   2-tutorial\n\n\n   3-sair\n\n\n");

        escolha = getch();

        if (escolha == '1') {
            system("cls");
            printf("em uma madrugada silenciosa, o ze do crime tentou escapar de carandiru\n\n\n");
            system("pause");
            tela = 1;
            system("cls");
        } else if (escolha == '2') {
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
        } else if (escolha == '3') {
            system("cls");
            printf("voce nao tem a coragem necessaria para fugir ne?.");
            return 0;
        } else {
            printf("coloque uma opcao valida!\n");
            system("pause");
        }
    }

    // Level 1 
    while (tela == 1) {
        level1[7][5] = Monstro;

        if (tem_chave == 0) {
            level1[9][5] = Porta_Fechada;
        } else {
            level1[9][5] = Porta_Aberta;
        }

        if (tem_chave == 0) {
            level1[4][5] = Chave;
        }

        for (i = 0; i < 10; i++) {
            for (j = 0; j < 10; j++) {
                if (i == cord_Y && j == cord_X) {
                    level1[i][j] = Jogador;
                }
                printf("     %c", level1[i][j]);
            }
            printf("\n\n");
        }

        level1[cord_Y][cord_X] = ' ';

        move = getch();

        if (move == 'w' && cord_Y - 1 != 0 && cord_Y - 1 != 9) {
            cord_Y--;
        }
        if (move == 's' && cord_Y + 1 != 0 && cord_Y + 1 != 9) {
            cord_Y++;
        }
        if (move == 'a' && cord_X - 1 != 0 && cord_X - 1 != 9) {
            cord_X--;
        }
        if (move == 'd' && cord_X + 1 != 0 && cord_X + 1 != 9) {
            cord_X++;
        }
        if (move == 'i' && cord_X == 5 && cord_Y == 5) {
            tem_chave  = 1;
            level1[4][5] = ' ';

        }
        if (cord_X == 5 && cord_Y == 7) {
            system("cls");
            printf("Ze do crime foi pego na fulga. Mas ele pode tentar em outra noite.\n\n");
            system("pause");
            cord_X = 1;
            cord_Y = 1;
            tem_chave = 0;
        }
        if(tem_chave == 1 && move == 'i' && cord_X == 5 && cord_Y == 8){
        	tela = 2;
        	system("cls");
		}
        system("cls");
    }
    //Level 2
    while(tela == 2){
    	
	}

    return 0;
}
