# Filas de Prioridade

## 📚 Introdução

No capítulo anterior conhecemos algumas das principais estruturas da STL, como pilhas, filas e conjuntos. Neste capítulo estudaremos outra estrutura extremamente importante em Programação Competitiva: a **fila de prioridade** (`priority_queue`).

Diferente de uma fila comum, onde os elementos são removidos na ordem em que foram inseridos (FIFO), uma fila de prioridade sempre remove primeiro o elemento com maior prioridade. Em C++, essa estrutura é implementada utilizando uma **heap**, permitindo consultar rapidamente o elemento de maior prioridade.

As principais operações possuem as seguintes complexidades:

| Operação  | Complexidade |
| --------- | :----------: |
| `top()`   |    `O(1)`    |
| `push()`  |  `O(log n)`  |
| `pop()`   |  `O(log n)`  |
| `empty()` |    `O(1)`    |
| `size()`  |    `O(1)`    |

Sempre que um problema exigir escolher repetidamente o maior ou o menor elemento de um conjunto que muda ao longo da execução, uma fila de prioridade provavelmente será a estrutura mais adequada.

---

## 📝 Implementação

### 📋 Inicializando uma fila de prioridade

Para utilizar uma fila de prioridade em C++, basta incluir a biblioteca `<queue>` e declarar uma variável do tipo `priority_queue`.

Por padrão, a `priority_queue` do C++ é uma **max-heap**, ou seja, o maior elemento sempre ficará no topo da fila.

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
    priority_queue<int> fila;

    fila.push(5);
    fila.push(3);
    fila.push(1);
    fila.push(4);
    fila.push(2);

    cout << fila.top() << "\n"; // 5

    return 0;
}
```

Observe que o valor retornado por `top()` é o maior elemento da fila, independentemente da ordem em que os elementos foram inseridos.

Isso não significa que todos os elementos estejam ordenados. A `priority_queue` apenas garante que o elemento de maior prioridade estará disponível no topo da estrutura.

---

### 📋 Inserindo e removendo elementos

Os elementos podem ser adicionados utilizando a função `push()` e removidos utilizando `pop()`.

Sempre que um elemento é inserido ou removido, a estrutura reorganiza automaticamente a heap para manter suas propriedades.

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
    priority_queue<int> fila;

    fila.push(5);
    fila.push(3);
    fila.push(1);
    fila.push(4);
    fila.push(2);

    fila.push(6);

    cout << fila.top() << "\n"; // 6

    fila.pop();

    cout << fila.top() << "\n"; // 5

    return 0;
}
```

Além de `push()`, `pop()` e `top()`, também podemos utilizar:

- `empty()`: verifica se a fila está vazia;
- `size()`: retorna a quantidade de elementos armazenados.

---

### 📋 Menor elemento primeiro

Como vimos anteriormente, a `priority_queue` do C++ retorna sempre o maior elemento.

Caso desejemos que o menor elemento tenha prioridade, podemos utilizar o comparador `greater`.

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

int main() {
    priority_queue<
        int,
        vector<int>,
        greater<int>
    > fila;

    fila.push(5);
    fila.push(3);
    fila.push(1);
    fila.push(4);
    fila.push(2);

    cout << fila.top() << "\n"; // 1
}
```

Esse tipo de fila de prioridade é bastante utilizado em algoritmos como o Dijkstra, onde precisamos acessar continuamente o menor custo disponível.

---

### 📋 Exemplo de uso

Imagine que você é um treinador de Pokémon e, após capturar vários Pokémon, finalmente está pronto para desafiar o ginásio da cidade. Sempre que uma batalha acontece, você deseja utilizar seu Pokémon mais forte.

Será dada uma sequência de operações. Cada operação pode representar a captura de um novo Pokémon (`C`) ou uma batalha (`B`). Sempre que ocorrer uma batalha, o Pokémon mais forte será utilizado e, após a luta, seu poder será reduzido pela metade.

Para cada batalha, imprima o nome do Pokémon escolhido.

```cpp
#include <iostream>
#include <queue>
#include <string>

using namespace std;

int main() {
    priority_queue<pair<int, string>> fila;

    char op;

    while (cin >> op) {
        if (op == 'C') {
            string nome;
            int poder;

            cin >> nome >> poder;

            fila.push({poder, nome});
        }
        else if (op == 'B') {
            auto pokemon = fila.top();
            fila.pop();

            cout << pokemon.second << "\n";

            fila.push({pokemon.first / 2, pokemon.second});
        }
    }

    return 0;
}
```

Nesse exemplo, cada elemento da fila é um `pair`, em que o primeiro valor representa o poder do Pokémon e o segundo representa seu nome.

Como a `priority_queue` do C++ é uma **max-heap**, o Pokémon com maior poder permanecerá automaticamente no topo da fila. Assim, sempre que uma batalha acontece, basta acessar o topo da estrutura para obter o Pokémon mais forte.

Após a batalha, removemos esse Pokémon da fila, reduzimos seu poder pela metade e o inserimos novamente. A fila reorganiza automaticamente seus elementos para que o próximo Pokémon mais forte volte a ocupar o topo.

Esse exemplo ilustra bem uma das principais aplicações das filas de prioridade: problemas em que precisamos escolher repetidamente o melhor elemento dentre vários candidatos, enquanto esse conjunto de elementos muda ao longo da execução.

## 🧑‍🏫 Exercícios

### 🟡 Médios

- [O Rolê Bad Vibes](https://www.beecrowd.com.br/judge/pt/problems/view/2958)
