# Vetores e Strings

## 📚 Introdução

Até agora, quando precisávamos guardar vários valores, podíamos criar uma variável para cada um deles:

```cpp
int nota1, nota2, nota3;
cin >> nota1 >> nota2 >> nota3;
```

Essa abordagem funciona para poucos dados, mas se torna inviável quando precisamos armazenar centenas ou milhares de valores. Além disso, muitos problemas não informam antecipadamente quais posições serão consultadas ou modificadas.

Para organizar coleções de valores, utilizamos estruturas como **arrays** e **vetores**. Quando queremos trabalhar com sequências de caracteres, utilizamos **strings**.

Neste capítulo, aprenderemos a:

- declarar arrays e vetores;
- acessar e modificar elementos por meio de índices;
- percorrer e ordenar vetores;
- adicionar e remover elementos;
- distinguir `char` de `string`;
- concatenar e percorrer strings;
- converter caracteres numéricos em números;
- analisar a complexidade das principais operações.

## Arrays

Um **array** é uma estrutura que armazena vários elementos do mesmo tipo em posições consecutivas.

```cpp
int numeros[4];
```

Nesse exemplo, criamos um array capaz de guardar quatro números inteiros.

Também podemos fornecer os valores durante a declaração:

```cpp
int numeros[4] = {10, 20, 30, 40};
```

As posições de um array começam em `0`. Portanto:

| Índice |  `0` |  `1` |  `2` |  `3` |
| -----: | ---: | ---: | ---: | ---: |
|  Valor | `10` | `20` | `30` | `40` |

Podemos acessar ou modificar uma posição usando colchetes:

```cpp
cout << numeros[0] << "\n";  // 10

numeros[2] = 50;
cout << numeros[2] << "\n";  // 50
```

O tamanho de um array tradicional precisa ser conhecido no momento de sua criação e não pode ser alterado posteriormente. Essa é uma das razões pelas quais, em C++ moderno, utilizamos frequentemente `vector`.

## Vetores

Um `vector` também guarda elementos do mesmo tipo, mas oferece mais flexibilidade. Seu tamanho pode ser definido durante a execução do programa e pode aumentar ou diminuir conforme necessário.

Para utilizar vetores, podemos incluir:

```cpp
#include <vector>
```

Em programação competitiva, é comum utilizar:

```cpp
#include <bits/stdc++.h>
```

Esse cabeçalho reúne grande parte da biblioteca padrão do C++.

### Declarando um vetor

Um vetor vazio de inteiros pode ser declarado assim:

```cpp
vector<int> numeros;
```

Também podemos criar um vetor com um tamanho inicial:

```cpp
vector<int> numeros(5);
```

Nesse caso, o vetor possui cinco posições, todas inicialmente preenchidas com `0`.

Podemos escolher outro valor inicial:

```cpp
vector<int> numeros(5, -1);
```

Agora, as cinco posições começam com o valor `-1`.

Outra possibilidade é declarar o vetor já com seus elementos:

```cpp
vector<int> numeros = {11, 2, 3, 4, 5};
vector<string> competicoes = {"MFP", "OBI", "Maratona"};
```

O tipo colocado entre `<` e `>` determina o tipo dos elementos armazenados.

### Tamanho e índices

Utilizamos `size()` para descobrir quantos elementos existem em um vetor:

```cpp
cout << numeros.size() << "\n";
```

Se o vetor possui `n` elementos, seus índices válidos vão de `0` até `n - 1`.

```cpp
vector<int> numeros = {10, 20, 30};

cout << numeros[0] << "\n"; // 10
cout << numeros[2] << "\n"; // 30
```

O acesso a uma posição por índice possui complexidade $O(1)$.

## Lendo um vetor

Em muitos problemas, conhecemos a quantidade de elementos antes de ler os valores:

```cpp
int n;
cin >> n;

vector<int> numeros(n);

for (int i = 0; i < n; i++) {
    cin >> numeros[i];
}
```

Primeiro, criamos um vetor com `n` posições. Depois, armazenamos cada valor diretamente em sua posição.

Também podemos começar com um vetor vazio e acrescentar os elementos:

```cpp
int n;
cin >> n;

vector<int> numeros;

for (int i = 0; i < n; i++) {
    int valor;
    cin >> valor;
    numeros.push_back(valor);
}
```

Quando o tamanho já é conhecido, a primeira forma costuma ser mais direta.

## Percorrendo um vetor

### Percurso usando índices

Quando precisamos conhecer ou modificar a posição de cada elemento, utilizamos um `for` com índices:

```cpp
vector<int> numeros = {11, 2, 3, 4, 5};

for (int i = 0; i < numeros.size(); i++) {
    cout << "Posição " << i << ": " << numeros[i] << "\n";
}
```

### Percurso usando `for` baseado em intervalo

Quando queremos apenas utilizar os valores, podemos escrever:

```cpp
vector<string> competicoes = {"MFP", "OBI", "Maratona"};

for (string competicao : competicoes) {
    cout << competicao << "\n";
}
```

Também podemos substituir o tipo por `auto`:

```cpp
for (auto competicao : competicoes) {
    cout << competicao << "\n";
}
```

O compilador deduzirá o tipo de `competicao`.

Nesse formato, `competicao` recebe uma cópia do elemento. Alterar essa variável não modifica o vetor original:

```cpp
for (int valor : numeros) {
    valor = 0;
}
```

Para modificar os elementos, utilizamos uma **referência**, indicada por `&`:

```cpp
for (int &valor : numeros) {
    valor = 0;
}
```

## Operações importantes com vetores

Considere o seguinte vetor:

```cpp
vector<int> numeros = {5, 4, 3, 2, 1};
```

### Adicionando um elemento

`push_back()` adiciona um elemento ao final:

```cpp
numeros.push_back(6);
```

Essa operação possui complexidade amortizada $O(1)$. Ocasionalmente, o vetor precisa reservar uma área maior e copiar seus elementos, mas, considerando uma sequência de inserções, o custo médio por operação é constante.

### Removendo o último elemento

`pop_back()` remove o elemento que está no final:

```cpp
numeros.pop_back();
```

Sua complexidade é $O(1)$. O método não retorna o elemento removido.

Antes de utilizá-lo, é importante verificar se o vetor não está vazio:

```cpp
if (!numeros.empty()) {
    numeros.pop_back();
}
```

### Limpando o vetor

`clear()` remove todos os elementos:

```cpp
numeros.clear();
```

Depois disso, `numeros.size()` será igual a `0`.

### Verificando se está vazio

```cpp
if (numeros.empty()) {
    cout << "O vetor está vazio.\n";
}
```

`empty()` retorna `true` quando não há nenhum elemento.

### Primeiro e último elementos

```cpp
cout << numeros.front() << "\n";
cout << numeros.back() << "\n";
```

Assim como `pop_back()`, `front()` e `back()` só devem ser utilizados quando o vetor não está vazio.

## Ordenando um vetor

A função `sort()` coloca os elementos em ordem crescente:

```cpp
vector<int> numeros = {5, 4, 3, 2, 1};

sort(numeros.begin(), numeros.end());
```

Depois da ordenação, o vetor será:

```text
1 2 3 4 5
```

`begin()` representa o início do intervalo e `end()` representa a posição imediatamente após o último elemento.

A complexidade de `sort()` é $O(n \log n)$.

Para ordenar em ordem decrescente, podemos utilizar:

```cpp
sort(numeros.rbegin(), numeros.rend());
```

## Exemplo completo com vetores

O programa abaixo lê as pontuações de `n` competidores e mostra a menor pontuação, a maior pontuação e a soma total:

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int n;
    cin >> n;

    vector<int> pontuacoes(n);

    for (int i = 0; i < n; i++) {
        cin >> pontuacoes[i];
    }

    int menor = pontuacoes[0];
    int maior = pontuacoes[0];
    long long soma = 0;

    for (int pontuacao : pontuacoes) {
        menor = min(menor, pontuacao);
        maior = max(maior, pontuacao);
        soma += pontuacao;
    }

    cout << "Menor: " << menor << "\n";
    cout << "Maior: " << maior << "\n";
    cout << "Soma: " << soma << "\n";

    return 0;
}
```

Esse algoritmo percorre o vetor uma vez e, portanto, possui complexidade $O(n)$.

## Strings e caracteres

Em C++, utilizamos principalmente dois tipos para representar texto:

- `char`: armazena um único caractere;
- `string`: armazena uma sequência de caracteres.

```cpp
char letra = 'a';
string palavra = "algoritmo";
```

Aspas simples representam um `char`, enquanto aspas duplas representam uma `string`:

```cpp
char correto = 'A';
string texto = "A";
```

Embora ambos representem a letra A, eles possuem tipos diferentes.

## Lendo strings

O operador `cin` lê uma string até encontrar um espaço:

```cpp
string nome;
cin >> nome;
```

Se a entrada for `Programação Competitiva`, apenas `Programação` será armazenada.

Para ler uma linha inteira, utilizamos `getline()`:

```cpp
string frase;
getline(cin, frase);
```

Quando utilizamos `getline()` depois de `cin`, precisamos remover a quebra de linha que permaneceu na entrada:

```cpp
int n;
cin >> n;
cin.ignore();

string frase;
getline(cin, frase);
```

Uma forma mais segura para ignorar tudo até a próxima quebra de linha é:

```cpp
cin.ignore(numeric_limits<streamsize>::max(), '\n');
```

## Tamanho e índices de uma string

Assim como um vetor, uma string possui posições numeradas a partir de `0`:

```cpp
string palavra = "FACOM";

cout << palavra[0] << "\n"; // F
cout << palavra[4] << "\n"; // M
cout << palavra.size() << "\n"; // 5
```

Para uma string `s` de tamanho `n`, os índices válidos vão de `0` até `n - 1`.

Também podemos modificar um caractere:

```cpp
string palavra = "gato";
palavra[0] = 'r';

cout << palavra << "\n"; // rato
```

O acesso a um caractere possui complexidade $O(1)$.

## Percorrendo uma string

Podemos percorrer uma string utilizando índices:

```cpp
string s;
cin >> s;

for (int i = 0; i < s.size(); i++) {
    cout << "Caractere " << i << ": " << s[i] << "\n";
}
```

Ou diretamente pelos caracteres:

```cpp
for (char caractere : s) {
    cout << caractere << "\n";
}
```

Percorrer todos os caracteres possui complexidade $O(n)$.

## Concatenando strings

Concatenar significa unir duas ou mais strings.

### Operador `+`

```cpp
string primeira = "FACOM";
string segunda = "petindo";

string nome = primeira + segunda;
cout << nome << "\n"; // FACOMpetindo
```

Também podemos acrescentar conteúdo com `+=`:

```cpp
string mensagem = "Olá, ";
mensagem += "competidor!";
```

### Método `append()`

```cpp
string mensagem = "FACOM";
mensagem.append("petindo");

cout << mensagem << "\n";
```

O método `append()` acrescenta uma string ao final de outra.

## Operações úteis com strings

Como `string` representa uma sequência de caracteres, ela possui várias operações semelhantes às de um vetor:

```cpp
string s = "abc";

s.push_back('d'); // abcd
s.pop_back();     // abc
cout << s.front() << "\n"; // a
cout << s.back() << "\n";  // c
```

Também podemos ordenar seus caracteres:

```cpp
string s = "caba";
sort(s.begin(), s.end());

cout << s << "\n"; // aabc
```

Essa ideia é útil para verificar se duas palavras são formadas pelas mesmas letras.

## Caracteres e valores numéricos

Os caracteres dos dígitos também podem ser armazenados em variáveis do tipo `char`:

```cpp
char digito = '7';
```

Entretanto, o caractere `'7'` não é diretamente o número inteiro `7`. Para fazer a conversão, subtraímos o caractere `'0'`:

```cpp
char digito = '7';
int valor = digito - '0';

cout << valor << "\n"; // 7
```

Isso funciona porque os caracteres de `'0'` até `'9'` possuem códigos consecutivos.

Para converter um número de `0` a `9` em caractere, fazemos a operação inversa:

```cpp
int valor = 7;
char digito = valor + '0';
```

### Exemplo: somando os dígitos

```cpp
string numero;
cin >> numero;

int soma = 0;

for (char digito : numero) {
    soma += digito - '0';
}

cout << soma << "\n";
```

Se a entrada for `2048`, a saída será `14`.

Ler um número como string é especialmente útil quando ele possui dígitos demais para caber nos tipos numéricos tradicionais ou quando precisamos analisar cada dígito separadamente.

## Exemplo completo com strings

O programa abaixo conta quantas vezes cada vogal aparece em uma palavra:

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    string palavra;
    cin >> palavra;

    vector<int> frequencia(5, 0);
    string vogais = "aeiou";

    for (char caractere : palavra) {
        for (int i = 0; i < vogais.size(); i++) {
            if (caractere == vogais[i]) {
                frequencia[i]++;
            }
        }
    }

    for (int i = 0; i < vogais.size(); i++) {
        cout << vogais[i] << ": " << frequencia[i] << "\n";
    }

    return 0;
}
```

Como existem sempre cinco vogais, para cada caractere fazemos no máximo cinco comparações. Portanto, a complexidade é $O(n)$.

## Vetor de frequências

Quando os valores possíveis pertencem a um intervalo pequeno, podemos usar um vetor para contar quantas vezes cada valor aparece.

Por exemplo, para contar as letras maiúsculas de uma string:

```cpp
string s;
cin >> s;

vector<int> frequencia(26, 0);

for (char letra : s) {
    frequencia[letra - 'A']++;
}
```

A posição `0` representa a letra `A`, a posição `1` representa `B` e assim por diante.

Para imprimir as frequências:

```cpp
for (int i = 0; i < 26; i++) {
    char letra = 'A' + i;
    cout << letra << ": " << frequencia[i] << "\n";
}
```

Essa técnica aparece com frequência em problemas que pedem para comparar palavras, encontrar letras repetidas ou verificar anagramas.

## Complexidade das operações

As complexidades mais importantes deste capítulo são:

| Operação                                      |      Complexidade |
| --------------------------------------------- | ----------------: |
| Acessar `v[i]` ou `s[i]`                      |            $O(1)$ |
| Consultar `size()` ou `empty()`               |            $O(1)$ |
| Adicionar no final com `push_back()`          | $O(1)$ amortizado |
| Remover do final com `pop_back()`             |            $O(1)$ |
| Percorrer todos os elementos                  |            $O(n)$ |
| Concatenar uma string de tamanho `m`          |            $O(m)$ |
| Ordenar `n` elementos com `sort()`            |     $O(n \log n)$ |
| Inserir ou remover no início/meio de um vetor |            $O(n)$ |

Inserções no início ou no meio podem exigir o deslocamento de vários elementos. Quando precisamos inserir e remover frequentemente nessas posições, outras estruturas podem ser mais adequadas.

## Erros comuns

### Acessar uma posição inexistente

```cpp
vector<int> numeros = {10, 20, 30};
cout << numeros[3] << "\n";
```

Os índices válidos são `0`, `1` e `2`. Acessar `numeros[3]` provoca comportamento indefinido e pode causar um erro de execução.

O mesmo cuidado vale para strings.

### Usar `<=` ao percorrer

```cpp
for (int i = 0; i <= numeros.size(); i++) {
    cout << numeros[i] << "\n";
}
```

Quando `i == numeros.size()`, a posição acessada não existe. A condição correta é:

```cpp
for (int i = 0; i < numeros.size(); i++) {
    cout << numeros[i] << "\n";
}
```

### Confundir tamanho e último índice

Se uma string possui tamanho `5`, seu último índice é `4`, e não `5`:

```cpp
char ultimo = s[s.size() - 1];
```

Esse acesso só é válido quando a string não está vazia.

### Confundir aspas simples e duplas

```cpp
char letra = 'a';
string palavra = "a";
```

Use aspas simples para um caractere e aspas duplas para uma string.

### Remover elementos de uma estrutura vazia

Antes de chamar `pop_back()`, verifique se a estrutura possui algum elemento:

```cpp
if (!numeros.empty()) {
    numeros.pop_back();
}
```

### Alterar o tamanho durante o percurso

Adicionar ou remover elementos enquanto percorremos um vetor pode modificar seus índices e invalidar referências ou iteradores. Faça isso apenas quando o comportamento estiver bem planejado.

### Confundir um dígito com seu valor

```cpp
char digito = '5';
int valor = digito; // Não resulta no número 5.
```

Para obter o valor numérico, utilize:

```cpp
int valor = digito - '0';
```

## Exercícios recomendados

1. [Codeforces 734A - Anton and Danik](https://codeforces.com/problemset/problem/734/A)
2. [Codeforces 266A - Stones on the Table](https://codeforces.com/problemset/problem/266/A)
3. [Codeforces 141A - Amusing Joke](https://codeforces.com/problemset/problem/141/A)
4. [Codeforces 136A - Presents](https://codeforces.com/problemset/problem/136/A)
5. [Codeforces 59A - Word](https://codeforces.com/problemset/problem/59/A)
