# **Debugando um Verificador de Número Primo com GitHub Copilot**  

## **Desafio:**  
Em um sistema de verificação matemática online, foi solicitado que você desenvolvesse uma função capaz de identificar **se um número é primo ou não**.  

### **O que é um número primo?**  
Um número primo é aquele que:  
✅ Só é divisível por **1 e por ele mesmo**.  
✅ É **maior que 1**.  

No entanto, o código fornecido pela equipe contém um **erro lógico**, e sua missão é **corrigir** esse problema para que a verificação funcione corretamente.  

💡 **Dica:** O GitHub Copilot pode ajudar no processo de depuração, explicando e sugerindo correções no código.  

---

## 📥 **Entrada:**
📌 Um único número inteiro `N` (**N ≥ 0**) representando o número a ser verificado.  

## 📤 **Saída:**
O programa deverá exibir:  
✅ Caso o número seja primo:  
   ```
   N é um número primo!
   ```  
✅ Caso **não seja primo**:  
   ```
   N não é um número primo.
   ```  
_(Substituindo `N` pelo número fornecido na entrada.)_  

---

## **Exemplos:**
A tabela abaixo apresenta exemplos de entrada e saída esperada:

| Entrada | Saída |
|---------|------|
| **7**   | 7 é um número primo! |
| **10**  | 10 não é um número primo. |
| **2**   | 2 é um número primo! |

---

## ❌ **Código antes da correção:**
```python
number = int(input())

def is_prime(n):
    if n <= 4:  # ❌ Problema: Isso classifica erroneamente alguns primos
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

if is_prime(number):
    print(f"{number} é um número primo!")
else:
    print(f"{number} não é um número primo.")
```
### 🚨 **Problema no código**
- **Erro:** A condição `if n <= 4` está incorreta! Isso faz com que alguns números primos pequenos, como `2` e `3`, sejam classificados **erroneamente como não primos**.  

---

## ✅ **Código corrigido e otimizado:**
```python
# Entrada do número a ser verificado
number = input("Digite um número inteiro: ")

# Tratamento de erros para entrada inválida
if not number.isdigit():
    print("Erro: Por favor, insira um número inteiro válido.")
else:
    number = int(number)

    # Função para verificar se um número é primo
    def is_prime(n):
        if n < 2:  # ✅ Números menores que 2 não são primos
            return False
        if n in (2, 3):  # ✅ 2 e 3 são primos
            return True
        if n % 2 == 0 or n % 3 == 0:  # ✅ Eliminamos múltiplos de 2 e 3
            return False
        for i in range(5, int(n**0.5) + 1, 6):  # ✅ Melhor otimização com passo de 6k ± 1
            if n % i == 0 or n % (i + 2) == 0:
                return False
        return True

    # Verifica se o número é primo e imprime o resultado
    if is_prime(number):
        print(f"{number} é um número primo!")
    else:
        print(f"{number} não é um número primo.")
```
### **Otimizações Aplicadas**
✔️ **Correção do erro lógico** – Agora `2` e `3` são corretamente identificados como primos.  
✔️ **Tratamento de entrada inválida** – Evitamos falhas ao lidar com valores não numéricos.  
✔️ **Melhoria na eficiência** – Aplicamos a técnica **6k ± 1**, que reduz verificações desnecessárias.  

---

## **Por que verificamos até a raiz quadrada (`√N`)?**
Ao invés de testar todos os números menores que `N`, testamos até `√N`, pois **qualquer fator maior que `√N` terá um fator correspondente menor que `√N`**. Isso reduz drasticamente o número de verificações! 💡  

---

## **Código de Testes (`test_prime.py`)**
Para validar nossa implementação, adicionamos testes automatizados:

```python
import pytest
from main import is_prime

def test_numeros_primos():
    assert is_prime(2) == True
    assert is_prime(3) == True
    assert is_prime(7) == True
    assert is_prime(11) == True
    assert is_prime(97) == True

def test_numeros_nao_primos():
    assert is_prime(1) == False
    assert is_prime(4) == False
    assert is_prime(10) == False
    assert is_prime(12) == False
    assert is_prime(100) == False

pytest.main()
```
Para rodar os testes, basta executar no terminal:  
```bash
pytest test_prime.py
```

---

## **Comparação de Desempenho**
Aqui está uma breve análise do tempo de execução dos diferentes métodos de verificação de números primos:

| Método | Número de Iterações |
|--------|--------------------|
| Teste até N | **N-2** verificações |
| Teste até √N | **drástica redução** para √N verificações |
| Técnica `6k ± 1` | **eliminação de múltiplos de 2 e 3** |

🔹 **A otimização `6k ± 1` melhora muito a eficiência para números grandes!**  

---

## 📚 **Referências**
- [Explicação Matemática sobre Números Primos](https://www.khanacademy.org/math/algebra/x2f8bb11595b61c86:factorization/x2f8bb11595b61c86:prime-numbers/v/prime-numbers)
- [Otimização Algorítmica na Verificação de Primos](https://www.geeksforgeeks.org/efficient-prime-number-testing/)
- [GitHub Copilot para Debugging](https://github.com/features/copilot)

---

## **Conclusão:**
Com esta correção, agora o programa pode **verificar corretamente números primos**, garantindo que:  
✅ Números menores que `2` não sejam classificados como primos.  
✅ Os cálculos sejam feitos de forma **eficiente e precisa** usando `√N`.  
✅ A técnica **6k ± 1** melhora a performance ao eliminar múltiplos desnecessários.  
✅ O programa lida corretamente com **entradas inválidas**, garantindo estabilidade.  
✅ **Testes automatizados** asseguram que a lógica funciona em diferentes cenários. 
