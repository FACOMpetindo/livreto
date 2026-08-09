# Soma Máxima em um Intervalo

## 📚 Introdução

Um exemplo de exercício que aparece em competições de programação é o problema da soma máxima em um intervalo. Ele consiste em dado um vetor de números inteiros, encontrar a soma máxima de um intervalo desse vetor.

Por exemplo, dado o vetor `[1, 2, -3, 4, 5]`, a soma máxima de um intervalo desse vetor é `9`, que é a soma do intervalo `[4, 5]`.

Uma solução ingênua para esse problema seria testar todas as possíveis somas de intervalos do vetor, e retornar a maior soma encontrada. Porém, essa solução tem complexidade `O(n³)`, o que não é suficiente para resolver esse tipo de problema em tempo hábil.

## 🤷 Como resolver?

Em desafios desse tipo, a soma só pode ser entre números adjacentes, o que facilita nossa resolução.

Imagine que x seja a maior soma possível até o elemento atual, só temos duas opções para o próximo elemento, ou usamos ele na soma, ou não usamos.

Usando isto, podemos escrever o algoritmo da seguinte maneira.

```cpp
#include <vector>

using namespace std;

int maior_soma(vector<int> vet) {
    int resp = 0;
    int maior = 0;

    for (int i = 0; i < vet.size(); i++) {
        maior = max(0, maior+vet[i]);
        resp = max(resp, maior);
    }

    return resp;
}
```

A variável `maior` guarda a maior soma possível até o elemento atual, e a variável `resp` guarda a maior soma encontrada até o momento.

A cada iteração, a variável `maior` é atualizada, e a variável `resp` é atualizada caso a variável `maior` seja maior que ela.

O algoritmo tem complexidade `O(n)`, pois percorre o vetor uma única vez.

## 🧑‍🏫 Exercícios

- Exercício [2463](https://www.beecrowd.com.br/judge/pt/problems/view/2463) do Beecrowd, que caiu na OBI 2014, esse é um exercício bem simples, que pode ser resolvido com o algoritmo acima.
