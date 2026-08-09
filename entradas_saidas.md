# Entradas e saídas

## 📚 Introdução

Nesse artigo, vamos aprender como fazer as entradas e saídas nos exercícios de programação competitiva, em C++, temos dois pares de opções, se você é familiar com C, você pode usar `scanf` e `printf`, mas o mais comum é usar `cin` e `cout`, que são mais fáceis de usar e mais seguros, porém existem alguns casos que valem a pena serem explicados com mais detalhes, como os exercícios que utilizam EOF (End of File) e sobre fast io.

## 📥 Entradas

Como mencionado, normalmente usaremos o método padrão de input do C++, da biblioteca `iostream`, com a função `cin`.

Quando queremos ler mais de um valor na mesma linha, como por exemplo:

```
ufms feijoada
```

podemos fazer isso com o `cin`:

```cpp
#include <iostream>

using namespace std;

int main() {
    string a, b;
    cin >> a >> b;
}
```

Se precisarmos que os valores sejam armazenados em um vetor, podemos fazer isso com um loop:

```cpp
#include <iostream>
#include <bits/stdc++.h>

using namespace std

int main() {
    int n;
    cin >> n;

    vector<int> vet(n);
    for (int i = 0; i < n; i++) {
        cin >> vet[i];
    }
}
```

Antes de continuar, é importante conversar um pouco sobre os diferentes tipos de entradas que podemos encontrar, geralmente sabemos exatamente o número de linhas que serão lidas, por alguma estipulação do enunciado ou um valor do próprio input nos indica, como no exercício 1410 do Beecrowd:

<figure><img src="../assets/1410.png" alt="Exercício 1410 do Beecrowd"><figcaption></figcaption></figure>

A entrada pode parecer complicada, mas note que a primeira linha lida nos indica exatamente quantos valores vem a seguir, e o fim é indicado por dois valores 0 seguidos, então podemos ler a entrada da seguinte forma:

```cpp
#include <iostream>
#include <bits/stdc++.h>

using namespace std;

int main() {
    int atacantes, defensores;
    while (true) {
        cin >> atacantes >> defensores;

        if (atacantes == 0 || defensores == 0) {
            break;
        }
    }
}
```

Porém, existem casos onde não sabemos o número de linhas que serão lidas, como no exercício 2850 do Beecrowd:

<figure><img src="../assets/2850.png" alt="Exercício 2850 do Beecrowd"><figcaption></figcaption></figure>

O exercício nem nos disse isso, mas o final de um arquivo de entrada é sempre indicado por EOF (End of File), como não sabemos o número de linhas que serão lidas, temos que usar um while loop que lê até o EOF:

```cpp
#include <iostream>

using namespace std;

int main() {
    string lado;
    while (cin >> lado) {
        // restante do código
    }

    return 0;
}
```

Existe algo a mais que podemos fazer para deixar nossas entradas e saídas mais rápidas, isso é chamado de fast io, em C++ isso é feito colocando `ios::sync_with_stdio(false); cin.tie(0);` dentro da sua main, isso faz com que o `cin` e `cout`, sejam mais rápidos, porém atenção, se fizermos isso não podemos mais usar `scanf` e `printf`, pois eles não são mais sincronizados com o `cin` e `cout`.

## 📤 Saídas

O método padrão de output do C++ é o `cout`, e ele é bem simples de usar, como vimos anteriormente, podemos imprimir valores com ele:

```cpp
#include <iostream>

using namespace std;

int main() {
    int a = 10;
    cout << a << endl;
}
```

É mais recomendado usar `\n` ao invés de `endl`, pois o `endl` faz um flush no buffer, o que pode ser mais lento, e em exercícios de programação competitiva, a velocidade é importante, vamos ver um exemplo de como imprimir um vetor:

```cpp
#include <iostream>
#include <bits/stdc++.h>

using namespace std;

int main() {
    vector<int> vet = {1, 2, 3, 4, 5};
    for (auto i: vet) {
        cout << i << " ";
    }
    cout << "\n";
}
```

## 🧑‍🏫 Exercícios

Nenhum dos exercícios sugeridos abaixo necessariamente demanda o fast io, mas é uma boa hora pra você treinar isso e os diferentes tipos de entradas que vimos!

- Exercício [2850](https://judge.beecrowd.com/pt/problems/view/2850) do Beeecrowd, que estava no aquecimento da OBI 2018, na fase nacional.

- Exercício [1248](https://www.beecrowd.com.br/judge/pt/problems/view/1248) do Beecrowd, que caiu na OBI 2012.

- Exercício [2408](https://www.beecrowd.com.br/judge/pt/problems/view/2408) do Beecrowd, que caiu na OBI 2012.

- Exercício [2420](https://www.beecrowd.com.br/judge/pt/problems/view/2420) do Beecrowd, que caiu na OBI 2012.

- Exercício [1410](https://www.beecrowd.com.br/judge/pt/problems/view/1410) do Beecrowd, que caiu na ACM/ICPC South America Contest 2007.

- Exercício [2770](https://www.beecrowd.com.br/judge/pt/problems/view/2770) do Beecrowd, que caiu na V Maratona Norte Mineira de Programação, não se assuste com o nível 7 desse exercício, mantenha a calma e leia o que se pede.
