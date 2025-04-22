# Super-Trunfo-duelo-de-Pa-ses
Trabalho Estacio

#include <stdio.h>

// Estrutura para representar uma carta de pais
typedef struct {
    char nome[50];
    int populacao;
    float area;
    float pib;
    int pontosTuristicos;
    float densidadeDemografica;
} Carta;

// Funcao para mostrar o nome do atributo baseado no numero
const char* nomeDoAtributo(int opcao) {
    switch (opcao) {
        case 1: return "Populacao";
        case 2: return "Area";
        case 3: return "PIB";
        case 4: return "Pontos Turisticos";
        case 5: return "Densidade Demografica";
        default: return "Desconhecido";
    }
}

// Funcao para obter o valor do atributo baseado na escolha
float obterValor(Carta c, int atributo) {
    switch (atributo) {
        case 1: return (float)c.populacao;
        case 2: return c.area;
        case 3: return c.pib;
        case 4: return (float)c.pontosTuristicos;
        case 5: return c.densidadeDemografica;
        default: return 0.0;
    }
}

int main() {
    // Cartas pre-definidas
    Carta carta1 = {"Estados Unidos", 331786478, 9834000.0, 23000.0, 25, 331786478 / 9834000.0};
    Carta carta2 = {"China", 1449457891, 9597000.0, 17000.0, 40, 1449457891 / 9597000.0};

    int atributo1, atributo2;
    int i;

    printf("=== SUPER TRUNFO DE PAISES ===\n");
    printf("Carta 1: %s\n", carta1.nome);
    printf("Carta 2: %s\n\n", carta2.nome);

    // Menu para o primeiro atributo
    printf("Escolha o primeiro atributo:\n");
    printf("1. Populacao\n");
    printf("2. Area\n");
    printf("3. PIB\n");
    printf("4. Pontos Turisticos\n");
    printf("5. Densidade Demografica\n");
    printf("Opcao: ");
    scanf("%d", &atributo1);

    // Validacao do primeiro atributo
    if (atributo1 < 1 || atributo1 > 5) {
        printf("Opcao invalida!\n");
        return 1;
    }

    // Menu para o segundo atributo (sem repetir o primeiro)
    printf("\nEscolha o segundo atributo (diferente do primeiro):\n");
    for (i = 1; i <= 5; i++) {
        if (i != atributo1)
            printf("%d. %s\n", i, nomeDoAtributo(i));
    }
    printf("Opcao: ");
    scanf("%d", &atributo2);

    if (atributo2 < 1 || atributo2 > 5 || atributo2 == atributo1) {
        printf("Opcao invalida!\n");
        return 1;
    }

    // Comparacao dos dois atributos
    float valor1A = obterValor(carta1, atributo1);
    float valor2A = obterValor(carta2, atributo1);
    float valor1B = obterValor(carta1, atributo2);
    float valor2B = obterValor(carta2, atributo2);

    // Mostrar comparacao
    printf("\nComparacao dos atributos:\n");

    printf("%s:\n", nomeDoAtributo(atributo1));
    printf("%s: %.2f\n", carta1.nome, valor1A);
    printf("%s: %.2f\n", carta2.nome, valor2A);

    printf("%s:\n", nomeDoAtributo(atributo2));
    printf("%s: %.2f\n", carta1.nome, valor1B);
    printf("%s: %.2f\n", carta2.nome, valor2B);

    // Verificacao de vitoria por atributo
    int pontos1 = 0, pontos2 = 0;

    // Atributo 1
    if (atributo1 == 5) { // densidade demografica
        if (valor1A < valor2A) pontos1++; 
        else if (valor2A < valor1A) pontos2++;
    } else {
        if (valor1A > valor2A) pontos1++;
        else if (valor2A > valor1A) pontos2++;
    }

    // Atributo 2
    if (atributo2 == 5) {
        if (valor1B < valor2B) pontos1++; 
        else if (valor2B < valor1B) pontos2++;
    } else {
        if (valor1B > valor2B) pontos1++;
        else if (valor2B > valor1B) pontos2++;
    }

    // Soma total dos atributos
    float soma1 = valor1A + valor1B;
    float soma2 = valor2A + valor2B;

    printf("\nSoma total dos atributos:\n");
    printf("%s: %.2f\n", carta1.nome, soma1);
    printf("%s: %.2f\n", carta2.nome, soma2);

    // Resultado final
    printf("\nResultado:\n");
    if (soma1 > soma2)
        printf("%s venceu!\n", carta1.nome);
    else if (soma2 > soma1)
        printf("%s venceu!\n", carta2.nome);
    else
        printf("Empate!\n");

    return 0;
}
