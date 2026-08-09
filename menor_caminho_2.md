# Algoritmo de Floyd-Warshall

## 📚 Introdução

Na aula anterior, vimos o funcionamento do algoritmo de Dijkstra, que encontra o menor caminho entre dois vértices em um grafo.

Porém, vamos imaginar agora, que queremos saber a distância de qualquer vértice para qualquer outro vértice.

Podemos fazer isso com o Djikstra, porém teriamos que rodar o algoritmo para cada vértice, o que seria muito ineficiente.

Vamos apresentar um outro algoritmo agora, o Algoritmo de Floyd-Warshall, que possui um código extremamente simples que resolve esse problema para nós em `O(N³)`.

## 🤷 Como funciona?

A ideia do Algoritmo de Floyd-Warshall é bem simples e consiste basicamente de:

- Selecionar um vértice k diferente por vez. Por simplicidade, percorreremos os vértices em ordem crescente.
- Ver, para par de vértices i e j, se é melhor manter a distância atual de i a j ou atualizar fazendo o caminho i→k e depois k→j.

Aplicando no exemplo anterior, vamos escolher uma cidade por vez e recalcular as distâncias entre as outras cidades, vendo se é melhor passar pela cidade escolhida ou não.

Vamos simular o algoritmo usando o mesmo grafo da aula anterior para exemplificar. Com uma pequena mudança que dessa vez usaremos uma matriz de adjacência, e definiremos a distância de um vértice para ele mesmo como 0.

<figure><img src="../assets/flw1.png" alt="primeira imagem do floyd-warshall"><figcaption></figcaption></figure>

Começamos executando no vértice 1 e a única distância que alteramos é entre os vértices 2 e 7.

<figure><img src="../assets/flw2.png" alt="segunda imagem do floyd-warshall"><figcaption></figcaption></figure>

Agora vamos para o vértice 2 e alteramos as distâncias entre os pares (1,3), (1,4) e (3,7).

<figure><img src="../assets/flw3.png" alt="terceira imagem do floyd-warshall"><figcaption></figcaption></figure>

Note que a partir daqui o grafo começa a ficar com muitas arestas, então talvez seja melhor dar mais atenção a matriz de distâncias.

De todas forma, vamos para o vértice 3, onde atualizamos as distâncias entre os pares (1,4) e (2,4).

<figure><img src="../assets/flw4.png" alt="quarta imagem do floyd-warshall"><figcaption></figcaption></figure>

Agora vamos para o vértice 4, onde atualizamos as distâncias dos pares (1,5), (2,5), (3,5), (3,7) e (5,7).

<figure><img src="../assets/flw5.png" alt="quinta imagem do floyd-warshall"><figcaption></figcaption></figure>

Quando executamos o processo nos vértices 5 e 6, nada é alterado. Quando executamos no vértice 7, alteramos as distâncias dos pares (1,3), (1,4), (1,5).

<figure><img src="../assets/flw6.png" alt="sexta imagem do floyd-warshall"><figcaption></figcaption></figure>

Com isso finalizamos o algoritmo e agora temos o menor caminho de qualquer vértice para qualquer outro vértice.

<figure><img src="../assets/flw7.png" alt="sétima imagem do floyd-warshall"><figcaption></figcaption></figure>

## 📝 Implementação

A implementação do código é bem simples, simplesmente usamos um `for` para iterar por todos os vértices que usaremos como pivô e mais dois loops para percorrer todos os pares de vértices.

O código em C++ fica:

```cpp
#include <bits/stdc++.h>

using namespace std;

const long long INF = 1e18;

int n;
vector<vector<long long>> dist(n, vector<long long>(n, INF));

// distância de um vértice para ele mesmo é 0
for (int i = 0; i < n; i++)
    dist[i][i] = 0;

for (int k = 0; k < n; k++) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
        }
    }
}
```

Como vimos, esse algoritmo possui uma complexidade de `O(N³)`, que aparenta ser um absurdo para resolver um problema de menor caminho, mas é a melhor solução para esse tipo de exercício, e pela complexidade os valores de `N` serão pequenos.
