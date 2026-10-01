# Crivo de Eratóstenes

## 📚 Introdução

O crivo de Eratóstenes é um algoritmo que permite encontrar todos os números primos até um determinado número `n`.

## 🤷 Como funciona?

Pense no seguinte problema, dado um número Q, devemos responder para cada número de 0 até Q-1 se ele é ou não é primo, por exemplo se Q = 100, precisamos responder para todo número de 0 até 99 se eles são primos. Como podemos resolver esse problema?

Uma solução ingênua seria, para cada um dos Q números (chamamos tal número de N), testar se ele é divisível por algum número de 2 até N-1, por exemplo:

```cpp
bool eh_primo(int n) {
    for (int i = 2; i < n; i++) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}
```

Esse algoritmo funciona, mas ele é muito lento, pois para cada um dos Q números, ele testa todos os números de 2 até N-1, o que resulta em uma complexidade de `O(Q*N)`.

Podemos melhorar esse algoritmo, se percebermos que não precisamos testar todos os números de 2 até N-1, pois se um número `N` não for divisível por nenhum número de 2 até `N-1`, então ele não é divisível por nenhum número de 2 até `N/2`, pois se ele fosse divisível por um número maior que `N/2`, ele também seria divisível por um número menor que `N/2`.

Então podemos melhorar o algoritmo da seguinte forma:

```cpp
bool eh_primo(int n) {
    for (int i = 2; i < n/2; i++) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}
```

Agora o algoritmo está um pouco mais rápido, mas ainda é lento, pois para cada um dos Q números, ele testa todos os números de 2 até `N/2`, o que resulta em uma complexidade de `O(Q*N/2)`.

Podemos melhorar ainda mais esse algoritmo, se percebermos que não precisamos testar todos os números de 2 até `N/2`, podemos testar apenas os números de 2 até a raiz quadrada de N + 1, essa é uma propriedade bem legal da matemática que nos permite reduzir a complexidade ainda mais.

O código ficaria da seguinte forma:

```cpp
#include <cmath>

bool eh_primo(int n) {
    for (int i = 2; i < sqrt(n)+1; i++) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}
```

Agora o algoritmo está bem mais rápido, com uma complexidade de `O(Q*sqrt(N))`, porém para um número Q muito grande, esse código ainda pode demorar muito para responder para todos os N números.

Estamos esquecendo de algo muito importante! Se um dado número é primo, então duas vezes esse número não é primo, 3 vezes esse número não é primo e assim por diante, podemos visualizar isso na [animação abaixo](https://pt.wikipedia.org/wiki/Ficheiro:New_Animation_Sieve_of_Eratosthenes.gif):

<figure><img src="assets/crivo.gif" alt="Animação de números primos"><figcaption></figcaption></figure>

Podemos aplicar isso da seguinte forma, poderíamos usar um vetor e percorrer todos os números de 2 a Q, se ele estiver marcado, o número é um primo, então desmarcamos todos os múltiplos desse primo menores que Q, pois eles não são primos.

No final, só consultamos o vetor para ver se dado número é primo.

O código ficaria da seguinte forma:

```cpp
#include <vector>

using namespace std;

vector<bool> crivo(int n) {
    vector<bool> primos(n+1, true);
    primos[0] = false;  // 0 não é primo
    primos[1] = false;  // 1 não é primo
    for (int i = 2; i <= n; i++) {
        if (primos[i]) {  // se i é primo
            for (int j = i*i; j <= n; j += i) {  // marca todos os múltiplos de i como não primos
                primos[j] = false;
            }
        }
    }
    return primos;
}
```

Essa solução tem uma complexidade de `O(N * log(log(N)))`, sendo assim bastante rápida.

Para finalizar, temos que ter em mente que o Crivo de Erástotenes é um algoritmo muito eficiente para encontrar todos os números primos até um determinado número, mas, temos que ter em mente que criamos uma lista com o tamanho do número `Q`, e que fazemos múltiplas operações repetidas, então em casos onde você precisa responder poucas vezes se um número é primo ou não, a solução ingênua otimizada pode ser mais eficiente.

## 🧑‍🏫 Exercícios

- Exercício [1165](https://www.beecrowd.com.br/judge/pt/problems/view/1165) do Beecrowd, não tem muito o que falar sobre esse exercício, diga se um número é primo ou não!

- Exercício [3002](https://www.beecrowd.com.br/judge/pt/problems/view/3002) do Beecrowd, esse exercício gira em torno de números primos e de uma propriedade matemática chamada de Conjectura de Goldbach, um problema muito interessante e que vale a pena tentar resolver!
