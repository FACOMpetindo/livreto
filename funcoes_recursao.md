# **Funções e Recursão**

## **📚 Introdução**

Funções são uma das principais ferramentas para organizar um programa em C++. Elas permitem separar uma solução em partes menores, cada uma responsável por realizar uma tarefa específica.

Em Programação Competitiva, funções são especialmente úteis para evitar repetição de código e tornar a implementação mais organizada e fácil de entender. Além disso, muitos algoritmos podem ser descritos de forma natural utilizando funções.

Neste capítulo veremos como criar e utilizar funções em C++, como passar parâmetros, retornar valores e, por fim, como utilizar **recursão**, uma técnica em que uma função chama a si mesma.

---

# **🔧 Funções**

Uma função é um bloco de código que recebe algumas informações, realiza uma tarefa e pode retornar um resultado.

A estrutura básica de uma função é:

```cpp
tipo retorno nome(tipo parametro1, tipo parametro2) {
    // código
    return resultado;
}
```

Por exemplo, podemos criar uma função que soma dois números:

```cpp
int soma(int a, int b) {
    return a + b;
}
```

Depois, podemos utilizar essa função dentro do `main()`:

```cpp
#include <iostream>
using namespace std;

int soma(int a, int b) {
    return a + b;
}

int main() {

    int x = 10;
    int y = 20;

    cout << soma(x, y) << "\n";

}
```

A função `soma` recebe dois números inteiros e retorna outro número inteiro.

Uma função pode receber vários parâmetros, mas também pode não receber nenhum:

```cpp
void mensagem() {
    cout << "Olá!\n";
}
```

Nesse caso, utilizamos `void` para indicar que a função não retorna nenhum valor.

---

# **📤 Retorno**

Uma função pode retornar diferentes tipos de dados.

Por exemplo:

```cpp
int dobro(int x) {
    return 2 * x;
}

double metade(double x) {
    return x / 2;
}

bool par(int x) {
    return x % 2 == 0;
}
```

Cada função possui um tipo de retorno correspondente ao resultado produzido.

A palavra-chave `return` encerra a execução da função e devolve o valor para quem a chamou.

Podemos, por exemplo, utilizar o resultado de uma função em uma condição:

```cpp
if (par(10)) {
    cout << "O número é par\n";
}
```

Funções que possuem retorno diferente de `void` precisam retornar um valor compatível com o tipo declarado.

---

# **📥 Parâmetros**

Os parâmetros são as informações que uma função recebe para realizar sua tarefa.

Por exemplo:

```cpp
int maior(int a, int b) {
    if (a > b)
        return a;
    return b;
}
```

Ao chamar:

```cpp
int x = maior(10, 20);
```

os valores `10` e `20` são passados para os parâmetros `a` e `b`.

Por padrão, os parâmetros são **passados por valor**. Isso significa que a função recebe uma cópia do valor original.

```cpp
void muda(int x) {
    x = 100;
}

int main() {

    int a = 10;

    muda(a);

    cout << a << "\n";

}
```

A saída será:

```text
10
```

A variável `a` não foi modificada, pois a função recebeu uma cópia dela.

Em capítulos posteriores veremos outras formas de passar dados para funções, especialmente utilizando referências e vetores.

---

# **🔁 Reutilizando funções**

Uma das principais vantagens das funções é poder utilizá-las várias vezes.

Imagine que queremos verificar se vários números são primos. Podemos criar uma única função:

```cpp
bool primo(int n) {

    if (n < 2)
        return false;

    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return false;
    }

    return true;
}
```

Então podemos utilizá-la quantas vezes forem necessárias:

```cpp
if (primo(7))
    cout << "7 é primo\n";

if (primo(10))
    cout << "10 é primo\n";

if (primo(97))
    cout << "97 é primo\n";
```

Isso evita escrever a mesma lógica várias vezes e também facilita a correção do código: se houver algum erro na lógica para verificar números primos, precisamos corrigi-lo em apenas um lugar.

---

# **🔄 Recursão**

Uma função é chamada de **recursiva** quando ela chama a si mesma.

Por exemplo:

```cpp
void contar(int n) {

    if (n == 0)
        return;

    cout << n << "\n";

    contar(n - 1);
}
```

Podemos chamar:

```cpp
contar(5);
```

A execução será:

```text
5
4
3
2
1
```

Observe que a função continua chamando a si mesma até chegar ao caso `n == 0`.

Toda função recursiva precisa ter uma **condição de parada**, também chamada de **caso base**. Sem ela, a função continuaria chamando a si mesma indefinidamente.

---

# **🧱 Caso base**

O caso base é uma situação em que a função consegue responder diretamente, sem precisar fazer outra chamada recursiva.

Um exemplo clássico é o cálculo do fatorial:

$$
n! = n \times (n-1) \times (n-2) \times \dots \times 1
$$

Podemos observar que:

$$
0! = 1
$$

e, para `n > 0`:

$$
n! = n \times (n-1)!
$$

Essa definição pode ser transformada diretamente em uma função:

```cpp
int fatorial(int n) {

    if (n == 0)
        return 1;

    return n * fatorial(n - 1);
}
```

Ao calcular:

```cpp
cout << fatorial(4) << "\n";
```

podemos imaginar a execução como:

```text
fatorial(4)
    4 * fatorial(3)
        3 * fatorial(2)
            2 * fatorial(1)
                1 * fatorial(0)
                    1
```

Depois que chegamos ao caso base, as chamadas começam a retornar:

```text
fatorial(0) = 1
fatorial(1) = 1 * 1 = 1
fatorial(2) = 2 * 1 = 2
fatorial(3) = 3 * 2 = 6
fatorial(4) = 4 * 6 = 24
```

Portanto:

```text
24
```

Essa ideia de **dividir um problema em versões menores do próprio problema** é uma das principais características da recursão.

---

# **⚠️ Cuidado com a recursão**

Apesar de ser muito útil, a recursão possui alguns cuidados.

Cada chamada de uma função ocupa espaço na memória para armazenar suas variáveis e informações necessárias para continuar sua execução. Essas chamadas ficam armazenadas na **pilha de execução (call stack)**.

Uma quantidade muito grande de chamadas recursivas pode causar **stack overflow**, fazendo o programa exceder o espaço disponível para a pilha.

Por isso, nem todo problema deve ser resolvido com recursão. Quando existe uma solução iterativa simples, um `for`, `while` ou uma estrutura como `stack` pode ser uma alternativa melhor.

Também é importante verificar se cada chamada recursiva realmente se aproxima do caso base. Caso contrário, a função pode nunca terminar.

---

# **💡 Como pensar em uma função recursiva?**

Ao tentar resolver um problema utilizando recursão, podemos seguir três passos:

1. **Qual é o caso base?**
   Qual é a menor situação que conseguimos resolver diretamente?

2. **Como reduzir o problema?**
   Como transformar o problema atual em uma versão menor do mesmo problema?

3. **Como utilizar o resultado?**
   Depois de resolver o problema menor, como podemos utilizá-lo para resolver o problema original?

Por exemplo, no fatorial:

```cpp
int fatorial(int n) {

    if (n == 0)
        return 1;

    return n * fatorial(n - 1);
}
```

- Caso base: `n == 0`;
- Problema menor: `fatorial(n - 1)`;
- Resultado: multiplicamos por `n`.

Pensar dessa maneira ajuda a transformar definições matemáticas e problemas naturalmente recursivos em código.

---

## **🧑‍🏫 Exercícios**

### **🟢 Fáceis**

- [A. Function?](https://codeforces.com/problemset/problem/1385/A)

- [A. Recursive?](https://codeforces.com/problemset/problem/1335/A)

### **🟡 Médios**

- [Tower of Hanoi](https://judge.beecrowd.com/pt/problems/view/1257)

- [Counting Rooms](https://cses.fi/problemset/task/1192/)

### **🟠 Difíceis**

- [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/description/)

- [Subsets](https://leetcode.com/problems/subsets/description/)
