# STL

## 📚 Introdução

A STL (_Standard Template Library_) é uma biblioteca da linguagem C++ que fornece diversas estruturas de dados e algoritmos prontos para uso. Em Programação Competitiva, ela é indispensável, pois permite escrever soluções menores, mais rápidas e menos propensas a erros.

Embora seja possível implementar muitas dessas estruturas manualmente, a STL oferece implementações otimizadas e testadas, permitindo que o competidor concentre seus esforços na lógica do problema em vez da implementação das estruturas.

Neste capítulo veremos algumas das estruturas mais utilizadas em competições: `pair`, `map`, `set`, `stack`, `queue` e `deque`.

---

# 📦 Pair

O `pair` é uma estrutura utilizada para armazenar dois valores relacionados entre si. Esses valores podem ser do mesmo tipo ou de tipos diferentes, tornando-o bastante útil quando precisamos agrupar duas informações que representam um mesmo objeto.

Podemos pensar em um `pair` como uma estrutura simples com dois campos: `first` e `second`. Esses campos podem ser acessados e modificados diretamente.

Essa estrutura aparece com frequência em problemas envolvendo coordenadas, grafos (armazenando peso e vértice), intervalos, competidores e diversas outras situações em que duas informações sempre caminham juntas.

```cpp
#include <iostream>
#include <utility>

using namespace std;

int main() {
    pair<int, string> aluno = {2026, "Gabriel"};

    cout << aluno.first << "\n";
    cout << aluno.second << "\n";
}
```

Também é comum utilizar vetores de pares.

```cpp
vector<pair<int, int>> pontos;
```

Ao ordenar um vetor de pares utilizando `sort()`, o C++ ordena primeiro pelo campo `first`. Caso existam empates, utiliza automaticamente o campo `second` como critério de desempate.

---

# 🗺️ Map

Um `map` funciona como um dicionário, permitindo associar uma chave a um valor.

Enquanto em um vetor acessamos elementos através de índices numéricos (`v[3]`), em um `map` podemos utilizar praticamente qualquer tipo como chave, como inteiros ou strings.

Internamente, o `map` mantém as chaves ordenadas, permitindo que inserções, buscas e remoções sejam realizadas em `O(log n)`.

Uma das aplicações mais comuns é realizar contagem de frequências, armazenar informações associadas a nomes ou identificar rapidamente se determinado elemento já apareceu.

```cpp
#include <iostream>
#include <map>

using namespace std;

int main() {
    map<string, int> gols;

    gols["Brasil"]++;
    gols["Brasil"]++;
    gols["Argentina"]++;

    cout << "Brasil: " << gols["Brasil"] << "\n";
    cout << "Argentina: " << gols["Argentina"] << "\n";
}
```

Também existe o `unordered_map`, que utiliza uma tabela hash ao invés de uma árvore. Ele não mantém os elementos ordenados, porém possui complexidade média `O(1)` para inserções e buscas, sendo uma ótima escolha quando a ordem das chaves não é importante.

---

# 🎯 Set

Um `set` representa um conjunto de elementos únicos.

Ao inserir um valor que já existe no conjunto, nenhuma alteração é feita. Além disso, todos os elementos permanecem ordenados automaticamente.

As operações de inserção, remoção e busca possuem complexidade `O(log n)`.

```cpp
#include <iostream>
#include <set>

using namespace std;

int main() {
    set<int> numeros;

    numeros.insert(5);
    numeros.insert(2);
    numeros.insert(5);
    numeros.insert(8);

    for (int x : numeros)
        cout << x << " ";
}
```

Saída:

```
2 5 8
```

Os conjuntos aparecem frequentemente em problemas onde precisamos remover duplicatas, verificar rapidamente se um elemento já foi visitado ou manter elementos sempre ordenados.

Assim como no `map`, também existe o `unordered_set`, que não mantém os elementos ordenados, mas oferece operações com complexidade média `O(1)`.

---

# 📚 Stack

Uma `stack` (pilha) segue a política **LIFO (Last In, First Out)**, ou seja, o último elemento inserido será o primeiro a ser removido.

Uma boa analogia é uma pilha de pratos: só conseguimos retirar o prato que está no topo e, ao colocar um novo prato, ele passa a ocupar essa posição.

Diferente de um vetor, não podemos acessar qualquer posição da pilha. Apenas o elemento do topo pode ser consultado ou removido.

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main() {
    stack<int> pilha;

    pilha.push(10);
    pilha.push(20);
    pilha.push(30);

    cout << pilha.top() << "\n";

    pilha.pop();

    cout << pilha.top() << "\n";
}
```

As principais funções são:

- `push()` adiciona um elemento ao topo;
- `pop()` remove o elemento do topo;
- `top()` retorna o elemento do topo;
- `empty()` verifica se a pilha está vazia;
- `size()` retorna a quantidade de elementos.

Pilhas são bastante utilizadas em algoritmos de busca em profundidade (DFS), avaliação de expressões, verificação de parênteses balanceados e em diversas simulações.

---

# 🚶 Queue

Uma `queue` (fila) segue a política **FIFO (First In, First Out)**.

O primeiro elemento inserido será sempre o primeiro a ser removido, exatamente como acontece em uma fila de banco ou supermercado.

Assim como ocorre com a pilha, não podemos acessar qualquer posição da fila. Apenas os elementos da frente e de trás podem ser consultados.

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
    queue<int> fila;

    fila.push(10);
    fila.push(20);
    fila.push(30);

    cout << fila.front() << "\n";

    fila.pop();

    cout << fila.front() << "\n";
}
```

As principais funções são:

- `push()` adiciona um elemento ao final;
- `pop()` remove o elemento da frente;
- `front()` retorna o primeiro elemento;
- `back()` retorna o último elemento;
- `empty()` verifica se a fila está vazia;
- `size()` retorna a quantidade de elementos.

Filas são amplamente utilizadas em simulações e em algoritmos como a Busca em Largura (BFS), onde os vértices precisam ser processados exatamente na ordem em que foram descobertos.

---

# 🔀 Deque

`deque` é a abreviação de **Double Ended Queue**, que pode ser traduzido como "fila de duas pontas".

Enquanto uma `queue` permite inserções apenas no final e remoções apenas no início, o `deque` permite inserir e remover elementos em ambas as extremidades.

Essa flexibilidade faz com que ele possa reproduzir tanto o comportamento de uma fila quanto o de uma pilha.

```cpp
#include <iostream>
#include <deque>

using namespace std;

int main() {
    deque<int> d;

    d.push_back(2);
    d.push_back(3);
    d.push_front(1);

    cout << d.front() << "\n";
    cout << d.back() << "\n";

    d.pop_front();
    d.pop_back();
}
```

As principais funções são:

- `push_front()`
- `push_back()`
- `pop_front()`
- `pop_back()`
- `front()`
- `back()`
- `empty()`
- `size()`

Podemos utilizar um `deque` de diferentes maneiras:

- `push_back()` + `pop_front()` → comportamento de uma fila (FIFO);
- `push_back()` + `pop_back()` → comportamento de uma pilha (LIFO);
- `push_front()` e `push_back()` juntos → quando o problema exige inserções em ambas as extremidades.

Apesar de ser mais flexível, muitas vezes é preferível utilizar `stack` ou `queue` quando já sabemos exatamente qual comportamento desejamos. Isso torna o código mais legível e deixa mais clara a intenção do algoritmo.

## 🧑‍🏫 Exercícios

### 🟢 Fáceis

- [Football](https://codeforces.com/contest/43/problem/A)

### 🟡 Médios

- [Jogando Cartas Fora](https://judge.beecrowd.com/pt/problems/view/1110)

### 🟠 Difícil

- [Partition Array According to Given Pivot](https://leetcode.com/problems/partition-array-according-to-given-pivot/description/)
