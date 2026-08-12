# Two Pointers

## 📚 Introdução

**Two Pointers** é uma técnica utilizada para resolver problemas envolvendo sequências de elementos mantendo dois ponteiros que percorrem a estrutura de acordo com alguma condição.

Apesar do nome, não existe uma única forma de utilizar Two Pointers. Em geral, mantemos duas variáveis que representam posições em um ou mais vetores e movimentamos esses ponteiros conforme a lógica do problema.

Por exemplo, podemos utilizar dois ponteiros, um no início e outro no final de um vetor:

```cpp
int l = 0;
int r = n - 1;
```

A cada passo, decidimos qual ponteiro deve ser movimentado.

Essa técnica aparece em diversos tipos de problemas, como:

- verificar se uma sequência é um palíndromo;
- percorrer dois vetores simultaneamente;
- encontrar pares de elementos;
- trabalhar com subvetores;
- contar elementos dentro de determinados intervalos;
- encontrar o maior ou menor segmento que satisfaz uma condição.

Uma das formas mais importantes de Two Pointers é a **Sliding Window**, ou **janela deslizante**, que veremos com mais detalhes neste capítulo.

## ↔️ Dois ponteiros em sentidos opostos

Uma utilização bastante comum consiste em colocar um ponteiro no início da estrutura e outro no final, aproximando-os conforme o algoritmo é executado.

Um exemplo clássico é verificar se uma string é um **palíndromo**.

Uma string é um palíndromo quando pode ser lida da mesma forma da esquerda para a direita e da direita para a esquerda.

Por exemplo:

```text
arara
```

é um palíndromo, enquanto:

```text
computador
```

não é.

Podemos verificar isso comparando os caracteres das duas extremidades:

```cpp
int l = 0;
int r = s.size() - 1;

bool palindromo = true;

while (l < r) {
    if (s[l] != s[r]) {
        palindromo = false;
        break;
    }

    l++;
    r--;
}
```

A cada iteração, comparamos os elementos correspondentes e aproximamos os ponteiros.

O processo pode ser visualizado como:

```text
a b c b a
↑       ↑
L       R

  a b c b a
    ↑   ↑
    L   R

  a b c b a
      ↑
     L,R
```

A vantagem é que cada posição é analisada apenas algumas vezes, resultando em uma solução `O(n)`.

## 🔀 Two Pointers com dois vetores

Os dois ponteiros também podem pertencer a estruturas diferentes.

Um exemplo clássico é o processo de **intercalação de dois vetores ordenados**, utilizado no Merge Sort.

Considere:

```text
A = [1, 4, 7]
B = [2, 3, 8]
```

Podemos manter um ponteiro para cada vetor:

```cpp
int i = 0;
int j = 0;
```

Em cada passo, comparamos `A[i]` e `B[j]` e adicionamos o menor deles ao resultado.

```cpp
while (i < A.size() && j < B.size()) {
    if (A[i] < B[j]) {
        resultado.push_back(A[i]);
        i++;
    }
    else {
        resultado.push_back(B[j]);
        j++;
    }
}
```

Depois que um dos vetores termina, adicionamos os elementos restantes do outro vetor.

A ideia importante é que **cada ponteiro percorre seu vetor apenas uma vez**, resultando em complexidade `O(n + m)`.

# 🪟 Sliding Window

Uma das aplicações mais poderosas de Two Pointers é a técnica conhecida como **Sliding Window**, ou **janela deslizante**.

Nesse caso, os dois ponteiros representam as extremidades de uma janela dentro de um vetor:

```text
L               R
↓               ↓
[  4  2  3  1  5  2  1  ]
```

O ponteiro `R` normalmente é utilizado para **aumentar a janela**, enquanto `L` é utilizado para **diminuí-la**.

Podemos imaginar que estamos deslizando uma janela sobre o vetor:

```text
[ 4  2  3 ] 1  5  2  1
  L     R

  4 [ 2  3  1 ] 5  2  1
      L     R

  4  2 [ 3  1  5 ] 2  1
          L     R
```

Essa técnica é especialmente útil quando o problema pergunta sobre **subvetores contínuos** e existe uma maneira eficiente de adicionar ou remover elementos da janela.

## ➕ Aumentando e diminuindo a janela

Considere um problema em que queremos encontrar o maior subvetor cuja soma seja menor ou igual a `K`.

Uma solução ingênua poderia testar todos os subvetores possíveis. Porém, existem `O(n²)` subvetores, o que pode ser muito lento para entradas grandes.

Podemos utilizar uma janela deslizante.

Inicialmente:

```cpp
int l = 0;
long long sum = 0;
```

Depois, fazemos `R` percorrer todos os elementos do vetor:

```cpp
for (int r = 0; r < n; r++) {
    sum += a[r];

    while (sum > K) {
        sum -= a[l];
        l++;
    }

    // [l, r] é uma janela válida
}
```

Quando `a[r]` é adicionado, a janela aumenta.

Se a soma ultrapassar `K`, a janela deixa de ser válida. Nesse caso, movemos `L` para a direita, removendo elementos da soma, até que a janela volte a ser válida.

## 🧩 Template geral

Grande parte dos problemas de Sliding Window pode ser pensada utilizando o seguinte modelo:

```cpp
int l = 0;

for (int r = 0; r < n; r++) {

    // add(a[r]);

    while (!good()) {

        // remove(a[l]);
        l++;
    }

    // utiliza a janela [l, r]
}
```

As operações mais importantes são:

### `add`

Quando `R` avança, adicionamos `a[R]` à janela.

Por exemplo, se estamos trabalhando com soma:

```cpp
sum += a[r];
```

### `good`

Precisamos saber se a janela atual satisfaz a condição do problema.

Por exemplo:

```cpp
sum <= K
```

### `remove`

Quando a janela deixa de ser válida, removemos elementos pelo lado esquerdo:

```cpp
sum -= a[l];
l++;
```

O importante é perceber que não precisamos implementar necessariamente funções chamadas `add`, `good` e `remove`. Esses nomes representam apenas as três operações que precisamos realizar durante o algoritmo.

## 📏 Encontrando o maior segmento

Voltando ao problema da soma menor ou igual a `K`, depois de ajustar `L`, temos a garantia de que `[L, R]` é uma janela válida.

Podemos então calcular seu tamanho:

```cpp
int tamanho = r - l + 1;
```

e atualizar a melhor resposta encontrada:

```cpp
ans = max(ans, tamanho);
```

A solução completa fica:

```cpp
int l = 0;
long long sum = 0;
int ans = 0;

for (int r = 0; r < n; r++) {
    sum += a[r];

    while (sum > K) {
        sum -= a[l];
        l++;
    }

    ans = max(ans, r - l + 1);
}
```

A grande vantagem é que `L` e `R` nunca voltam para trás. Cada um percorre o vetor no máximo uma vez, fazendo com que a solução seja `O(n)`.

## 🔢 Contando segmentos

Podemos fazer uma pequena alteração no algoritmo anterior para responder outra pergunta.

Em vez de encontrar o **maior** segmento cuja soma é menor ou igual a `K`, podemos querer contar **quantos segmentos** possuem essa propriedade.

Depois de ajustar `L`, sabemos que:

```text
[L, R]
```

é válido.

Mas não apenas ele é válido.

Se todos os elementos são positivos, então também são válidos:

```text
[L, R]
[L+1, R]
[L+2, R]
...
[R, R]
```

Existem exatamente:

```cpp
r - l + 1
```

desses segmentos.

Portanto, podemos simplesmente fazer:

```cpp
ans += r - l + 1;
```

O algoritmo fica:

```cpp
int l = 0;
long long sum = 0;
long long ans = 0;

for (int r = 0; r < n; r++) {
    sum += a[r];

    while (sum > K) {
        sum -= a[l];
        l++;
    }

    ans += r - l + 1;
}
```

Essa é uma ideia bastante importante em Sliding Window: às vezes não precisamos analisar individualmente todos os segmentos, pois conseguimos contar vários deles de uma só vez.

# 🔄 Outras variações

A mesma técnica pode ser adaptada para diferentes perguntas.

Por exemplo, podemos procurar:

- o maior segmento cuja soma é menor que `K`;
- o número de segmentos cuja soma é menor que `K`;
- o menor segmento cuja soma é maior ou igual a `K`;
- o número de segmentos cuja soma é maior ou igual a `K`.

A estrutura do algoritmo permanece bastante parecida. O que muda são a condição que define uma janela válida e a maneira como atualizamos a resposta.

Por exemplo, para procurar o **menor segmento cuja soma é maior ou igual a `K`**, podemos aumentar `R` até a janela ficar válida e então mover `L` enquanto ela continuar válida, tentando diminuí-la o máximo possível.

# 🧠 Quando usar Two Pointers?

Reconhecer quando um problema pode ser resolvido com Two Pointers é tão importante quanto saber implementar a técnica.

Uma situação muito comum é quando estamos trabalhando com um **subvetor contínuo** e conseguimos atualizar rapidamente as informações da janela quando adicionamos ou removemos um elemento.

Na Sliding Window, uma propriedade particularmente importante é a seguinte:

> Se uma janela é válida, ao diminuir essa janela ela continua válida.

Por exemplo, se todos os elementos são positivos e:

```text
soma da janela <= K
```

então remover elementos da janela nunca fará sua soma aumentar.

Isso permite que `L` avance apenas quando necessário, sem precisar voltar.

Também existem problemas com a propriedade inversa: uma janela válida pode continuar válida quando adicionamos elementos.

Por exemplo, podemos ter condições como:

```text
soma >= K
```

ou:

```text
quantidade de elementos distintos >= K
```

Nesses casos, a forma de movimentar os ponteiros pode ser adaptada à propriedade que estamos tentando manter.

## ⚠️ Cuidado com a propriedade da janela

Nem todo problema envolvendo subvetores pode ser resolvido com Sliding Window.

É necessário verificar se conseguimos manter a informação da janela de maneira eficiente e se o movimento dos ponteiros possui uma propriedade que permita evitar testar todas as possibilidades.

Por exemplo, no caso de soma de elementos **positivos**, quando aumentamos a janela, a soma nunca diminui. Quando diminuímos a janela, a soma nunca aumenta.

Essa propriedade é justamente o que permite mover os ponteiros de maneira eficiente.

Se os elementos puderem ser negativos, essa propriedade pode deixar de existir e o algoritmo acima pode não funcionar.

Portanto, antes de aplicar Two Pointers, pergunte:

1. Estou trabalhando com uma sequência contínua?
2. Consigo adicionar um elemento à janela eficientemente?
3. Consigo remover um elemento da janela eficientemente?
4. Existe uma propriedade que permita movimentar `L` e `R` sem voltar para trás?
5. Consigo manter a condição da janela durante esse processo?

Se a resposta for sim, Two Pointers pode ser uma boa candidata.

# ⏱️ Complexidade

Uma das principais vantagens da técnica é reduzir soluções que poderiam ser `O(n²)` para `O(n)`.

Apesar de existir um `for` e um `while` no código:

```cpp
for (int r = 0; r < n; r++) {
    while (!good()) {
        l++;
    }
}
```

isso **não significa que a complexidade seja `O(n²)`**.

O ponteiro `R` avança no máximo `n` vezes e o ponteiro `L` também avança no máximo `n` vezes.

Assim, o número total de operações é proporcional a:

```text
n + n = 2n
```

e, portanto, a complexidade é:

```text
O(n)
```

Essa análise é chamada de **complexidade amortizada** e é fundamental para entender por que a técnica funciona.

# 💡 Resumindo

Two Pointers não é uma única implementação, mas uma família de técnicas que utiliza dois ponteiros para percorrer uma ou mais estruturas de forma eficiente.

Podemos utilizar os ponteiros de diferentes maneiras:

- um no início e outro no final, como em palíndromos;
- um em cada vetor, como na intercalação de vetores ordenados;
- ambos delimitando uma janela, como na Sliding Window.

Na Sliding Window, o padrão mais importante é:

```cpp
int l = 0;

for (int r = 0; r < n; r++) {

    // adiciona a[r]

    while (!good()) {

        // remove a[l]
        l++;
    }

    // utiliza a janela [l, r]
}
```

A ideia central é manter uma janela válida enquanto `R` percorre o vetor. Quando a janela deixa de satisfazer a condição, avançamos `L` até que ela volte a ser válida.

Com prática, muitos problemas que inicialmente parecem exigir testar todos os `O(n²)` subvetores podem ser reduzidos a uma solução `O(n)`.
