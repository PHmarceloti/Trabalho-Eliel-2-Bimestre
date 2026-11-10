# Trabalho-Eliel-2-Bimestre
#include <stdio.h>


#ifdef _WIN32
#include <windows.h>
#endif

int main(void) {
    int senha, senhaDigitada, opcao;
    float saldo = 500.00f;  
    float maiorDeposito = 0.0f;
    float valor;

#ifdef _WIN32
    SetConsoleOutputCP(65001);
#endif

    do {
        printf("Crie uma senha numérica de 4 dígitos: ");
        scanf("%d", &senha);

        if (senha < 1000 || senha > 9999) {
            printf("A senha deve ter exatamente 4 dígitos!\n");
        }
    } while (senha < 1000 || senha > 9999);

    do {
        printf("\nOpções do Menu:\n");
        printf("1. Depositar\n");
        printf("2. Sacar\n");
        printf("3. Consultar Saldo e Estatísticas\n");
        printf("4. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1: // Depositar
                printf("Valor do depósito (ex: 50.75): R$ ");
                scanf("%f", &valor);

                if (valor <= 0) {
                    printf("Valor inválido!\n");
                } else {
                    saldo += valor;
                    if (valor > maiorDeposito) {
                        maiorDeposito = valor;
                    }
                    printf("Depósito realizado com sucesso!\n");
                }
                break;

            case 2: // Sacar
                printf("Digite sua senha de 4 dígitos: ");
                scanf("%d", &senhaDigitada);

                if (senhaDigitada != senha) {
                    printf("Senha Incorreta! Operação cancelada.\n");
                } else {
                    printf("Valor do saque: R$ ");
                    scanf("%f", &valor);

                    if (valor <= 0) {
                        printf("Valor inválido!\n");
                    } else if (valor > saldo) {
                        printf("Saldo Insuficiente!\n");
                    } else {
                        saldo -= valor;
                        printf("Saque realizado com sucesso!\n");
                    }
                }
                break;

            case 3: // Consultar saldo e estatísticas
                printf("Saldo atual: R$ %.2f\n", saldo);
                printf("Maior depósito realizado: R$ %.2f\n", maiorDeposito);
                break;

            case 4: // Sair
                printf("Obrigado por usar nosso banco!\n");
                break;

            default:
                printf("Opção inválida!\n");
        }
    } while (opcao != 4);

    return 0;
}
