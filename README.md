# projeto-1-programacao
Código do projeto jogo
#include <iostream>
#include "header.h"
#include <stdlib.h>

using namespace std;

void desenharMapa()
{
    int i, j;
    for (i = 0; i < tamanhoAtual; i++)
    {
        for (j = 0; j < tamanhoAtual; j++)
        {
            // Primeira Linha
            if (i == 0)
            {
                mapa[i][j] = '*';
            }
            // Ultima Linha
            else if (i == tamanhoAtual - 1)
            {
                mapa[i][j] = '*';
            }
            // Primeira Coluna
            else if (j == 0)
            {
                mapa[i][j] = '*';
            }
            // Ultima Coluna
            else if (j == tamanhoAtual - 1)
            {
                mapa[i][j] = '*';
            }
            // Posicao Intermediaria
            else
            {
                mapa[i][j] = ' ';
            }
        }
    }

    // Colocar Jogador
    mapa[1][1] = '&';
    mapa[4][7 ] = '#';
    // Colocar Chave
    mapa[tamanhoAtual / 2][tamanhoAtual - 2] = '@';
    // Colocar Porta
    mapa[tamanhoAtual - 2][tamanhoAtual - 1] = 'D';
}

void imprimirMapa()
{
    int i, j;
    for (i = 0; i < tamanhoAtual; i++)
    {
        for (j = 0; j < tamanhoAtual; j++)
        {
            cout << mapa[i][j];
        }
        cout << endl;
    }
}

void movimentarJogador()
{
    char direcao;
    cout << "Direcao: ";
    cin >> direcao;

    switch (direcao)
    {
    case 'w':
        if (mapa[posicaoXjogador - 1][posicaoYjogador] == ' ')
        {
            mapa[posicaoXjogador][posicaoYjogador] = ' ';
            posicaoXjogador--;
            mapa[posicaoXjogador][posicaoYjogador] = '&';
        }
        break;
    case 'a':
        if (mapa[posicaoXjogador][posicaoYjogador - 1] == ' ')
        {
            mapa[posicaoXjogador][posicaoYjogador] = ' ';
            posicaoYjogador--;
            mapa[posicaoXjogador][posicaoYjogador] = '&';
        }
        break;
    case 's':
        if (mapa[posicaoXjogador + 1][posicaoYjogador] == ' ')
        {

            mapa[posicaoXjogador][posicaoYjogador] = ' ';
            posicaoXjogador++;
            mapa[posicaoXjogador][posicaoYjogador] = '&';
        }
        break;

    case 'd':
        if (mapa[posicaoXjogador][posicaoYjogador + 1] == ' ' || mapa[posicaoXjogador][posicaoYjogador + 1] == '=')
        {
            mapa[posicaoXjogador][posicaoYjogador] = ' ';
            posicaoYjogador++;
            mapa[posicaoXjogador][posicaoYjogador] = '&';
        }
        break;

    case 'i':
        if (mapa[posicaoXjogador - 1][posicaoYjogador] == '@' ||
            mapa[posicaoXjogador][posicaoYjogador - 1] == '@' ||
            mapa[posicaoXjogador + 1][posicaoYjogador] == '@' ||
            mapa[posicaoXjogador][posicaoYjogador + 1] == '@')
        {
            mapa[posicaoXPorta][posicaoYPorta] = '=';
            mapa[posicaoXChave][posicaoYChave] = ' ';
        }
        break;

    default:
        break;
    }
}

int main()
{
	
    desenharMapa();
    while (true)
    {

        imprimirMapa();
        movimentarJogador();
        if(posicaoXjogador == posicaoXPorta && posicaoYjogador == posicaoYPorta) {
            cout << "Proxima Fase!";
            break;
        }
    }

    return 0;
}
  
  char mapa[75][75];
int tamanhoAtual = 25;

int posicaoXjogador = 1;
int posicaoYjogador = 1;

int posicaoXChave = tamanhoAtual / 2;
int posicaoYChave = tamanhoAtual - 2;

int posicaoXPorta = tamanhoAtual - 2;
int posicaoYPorta = tamanhoAtual - 1;

void desenharMapa();
void imprimirMapa();
void movimentarJogador();
