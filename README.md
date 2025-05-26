# GitHubCopilot-Debugando-

Depurando com o GitHub Copilot
2 / 3 - Debugando um Verificador de Número Primo
XP 6720/7750
NÍVEL 10
5/5
 Básico
 Matemática
Desafio
Em um sistema de verificação matemática online, foi solicitado que você desenvolvesse uma função capaz de identificar se um número é primo ou não. Um número primo é aquele que só é divisível por 1 e por ele mesmo, e é maior que 1.

No entanto, o código fornecido pela equipe contém um erro lógico que compromete o resultado final. Seu objetivo é analisar, identificar e corrigir o erro para que o programa funcione corretamente.

Uma opção para te ajudar durante o processo de depuração é o uso do GitHub Copilot, que pode explicar e sugerir correções de código.

Entrada
Um único número inteiro N (N ≥ 0) representando o número a ser verificado.

Saída
Caso o número seja primo, o programa deverá exibir: N é um número primo!
Caso o número não seja primo, deverá exibir: N não é um número primo.
Substituindo N pelo número fornecido na entrada.

Exemplos
A tabela abaixo apresenta exemplos com alguns dados de entrada e suas respectivas saídas esperadas. Certifique-se de testar seu programa com esses exemplos e com outros casos possíveis.

Entrada	Saída
7	7 é um número primo!
10	10 não é um número primo.
2	2 é um número primo!

antes:

number = int(input())

def is_prime(n):
    if n <= 4:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

if is_prime(number):
    print(f"{number} é um número primo!")
else:
    print(f"{number} não é um número primo.")

    depois 

    # Entrada do número a ser verificado
number = int(input())

# Função para verificar se um número é primo
def is_prime(n):
    if n < 2:  # Números menores que 2 não são primos
        return False
    for i in range(2, int(n**0.5) + 1):  # Verifica divisores até a raiz quadrada de n
        if n % i == 0:
            return False
    return True

# Verifica se o número é primo e imprime o resultado
if is_prime(number):
    print(f"{number} é um número primo!")
else:
    print(f"{number} não é um número primo.")
