# Busca Binária - 2

## 📚 Introdução

No primeiro contato com busca binária, normalmente aprendemos a procurar um elemento em um vetor ordenado. Se o elemento do meio for menor que o valor procurado, continuamos na metade direita; caso contrário, continuamos na metade esquerda.

Essa aplicação é importante, mas representa apenas uma parte do que a busca binária pode fazer.

Neste capítulo, veremos como utilizar a mesma ideia para:

- encontrar posições com as funções prontas da STL;
- localizar o primeiro ou o último valor que satisfaz uma condição;
- procurar diretamente a resposta de um problema;
- trabalhar com respostas representadas por números reais.

O elemento central de todas essas aplicações é a **monotonicidade**: conforme avançamos pelos valores possíveis, a resposta de uma condição muda no máximo uma vez.

## Relembrando a busca binária

Considere um vetor ordenado:

```cpp
vector<int> valores = {3, 5, 13, 16, 20};
```

Queremos descobrir se o valor `13` aparece no vetor.

Uma busca linear poderia verificar cada posição, gastando $O(n)$ no pior caso. Como o vetor está ordenado, podemos eliminar metade do espaço de busca em cada passo:

```cpp
int esquerda = 0;
int direita = valores.size() - 1;
int procurado = 13;

while (esquerda <= direita) {
    int meio = esquerda + (direita - esquerda) / 2;

    if (valores[meio] == procurado) {
        cout << "Encontrado!\n";
        break;
    }

    if (valores[meio] < procurado) {
        esquerda = meio + 1;
    } else {
        direita = meio - 1;
    }
}
```

A cada iteração, o intervalo restante é dividido aproximadamente pela metade. Por isso, a complexidade é $O(\log n)$.

Para valores inteiros de até aproximadamente $10^9$, são necessárias no máximo cerca de 32 iterações. Para valores de até $10^{18}$, cerca de 64 iterações são suficientes.

### Calculando o meio com segurança

É comum encontrar a seguinte expressão:

```cpp
int meio = (esquerda + direita) / 2;
```

Entretanto, `esquerda + direita` pode ultrapassar o limite do tipo utilizado. A forma abaixo evita esse problema:

```cpp
int meio = esquerda + (direita - esquerda) / 2;
```

Ao trabalhar com limites grandes, utilize também `long long`.

## Funções prontas da STL

Quando queremos procurar valores em um vetor ordenado, frequentemente não precisamos implementar a busca binária manualmente. A biblioteca padrão do C++ oferece funções prontas para isso.

Para utilizá-las, o intervalo deve estar ordenado.

```cpp
sort(valores.begin(), valores.end());
```

### `binary_search`

A função `binary_search` informa se um valor existe no intervalo. Ela retorna `true` ou `false`.

```cpp
vector<int> valores = {3, 5, 13, 16, 20};

bool existe = binary_search(
    valores.begin(),
    valores.end(),
    13
);

if (existe) {
    cout << "O valor aparece no vetor.\n";
}
```

Sua complexidade é $O(\log n)$.

### `lower_bound`

A função `lower_bound` retorna um iterador para o primeiro elemento **maior ou igual** ao valor procurado.

```cpp
vector<int> valores = {1, 2, 2, 2, 5, 8};

auto it = lower_bound(valores.begin(), valores.end(), 2);
int posicao = it - valores.begin();

cout << posicao << "\n";
```

Nesse exemplo, a saída é `1`, pois o primeiro `2` está na posição `1`.

Se todos os elementos forem menores que o valor procurado, o retorno será `valores.end()`.

```cpp
auto it = lower_bound(valores.begin(), valores.end(), 10);

if (it == valores.end()) {
    cout << "Não existe elemento maior ou igual.\n";
}
```

### `upper_bound`

A função `upper_bound` retorna um iterador para o primeiro elemento **estritamente maior** que o valor procurado.

```cpp
vector<int> valores = {1, 2, 2, 2, 5, 8};

auto it = upper_bound(valores.begin(), valores.end(), 2);
int posicao = it - valores.begin();

cout << posicao << "\n";
```

A saída é `4`, pois `valores[4] = 5` é o primeiro elemento maior que `2`.

### Contando ocorrências

Podemos combinar `lower_bound` e `upper_bound` para contar quantas vezes um valor aparece em um vetor ordenado:

```cpp
auto primeiro = lower_bound(valores.begin(), valores.end(), 2);
auto depoisDoUltimo = upper_bound(valores.begin(), valores.end(), 2);

int quantidade = depoisDoUltimo - primeiro;
cout << quantidade << "\n";
```

No vetor `{1, 2, 2, 2, 5, 8}`, o valor `2` aparece três vezes.

## Generalizando a busca binária

A busca binária não precisa procurar necessariamente um número dentro de um vetor. Podemos utilizá-la sempre que os valores candidatos estiverem divididos em dois grupos contínuos.

Por exemplo:

```text
não  não  não  não  não  sim  sim  sim  sim
```

Nesse caso, podemos procurar o **primeiro valor válido**.

Também podemos encontrar uma sequência inversa:

```text
sim  sim  sim  sim  sim  não  não  não  não
```

Nesse caso, normalmente procuramos o **último valor válido**.

Uma função booleana que verifica se um valor é válido costuma receber nomes como:

```cpp
bool valido(long long x);
```

ou:

```cpp
bool consegue(long long x);
```

Essa função também é chamada de **predicado** ou **função de verificação**.

Para usar busca binária, o resultado dessa função precisa ser monotônico. Não pode existir uma sequência como:

```text
não  sim  não  sim
```

Se a validade alternar várias vezes, não saberemos qual metade pode ser descartada.

## Encontrando o primeiro valor válido

Considere a sequência:

```text
não  não  não  sim  sim  sim
```

Queremos encontrar o primeiro `sim`.

O modelo abaixo mantém a resposta dentro do intervalo fechado `[esquerda, direita]`:

```cpp
long long esquerda = menorCandidato;
long long direita = maiorCandidato;

while (esquerda < direita) {
    long long meio = esquerda + (direita - esquerda) / 2;

    if (valido(meio)) {
        direita = meio;
    } else {
        esquerda = meio + 1;
    }
}

cout << esquerda << "\n";
```

Quando `meio` é válido, ele ainda pode ser a primeira resposta válida. Por isso, fazemos `direita = meio`, mantendo-o no intervalo.

Quando `meio` não é válido, sabemos que ele e todos os candidatos anteriores podem ser descartados. Por isso, fazemos `esquerda = meio + 1`.

Esse modelo pressupõe que `maiorCandidato` é válido. Se isso não for garantido pelo problema, devemos verificar a existência da resposta separadamente.

## Encontrando o último valor válido

Agora considere:

```text
sim  sim  sim  sim  não  não
```

Queremos encontrar o último `sim`.

```cpp
long long esquerda = menorCandidato;
long long direita = maiorCandidato;

while (esquerda < direita) {
    long long meio = esquerda + (direita - esquerda + 1) / 2;

    if (valido(meio)) {
        esquerda = meio;
    } else {
        direita = meio - 1;
    }
}

cout << esquerda << "\n";
```

Observe o `+ 1` no cálculo do meio. Ele faz o meio ser arredondado para cima.

Sem esse arredondamento, quando `direita = esquerda + 1`, o meio seria igual a `esquerda`. Se esse valor fosse válido, atribuiríamos novamente `esquerda = meio`, e o intervalo não diminuiria. O programa entraria em um loop infinito.

Esse modelo pressupõe que `menorCandidato` é válido.

## Busca binária na resposta

Em alguns problemas, não queremos encontrar uma posição em um vetor. Queremos descobrir o menor ou o maior valor que pode ser a resposta.

Essa técnica é chamada de **busca binária na resposta**.

Para utilizá-la, precisamos responder quatro perguntas:

1. Qual valor representa uma resposta candidata?
2. Como verificar se uma resposta candidata é válida?
3. A validade é monotônica?
4. Quais são os limites inferior e superior da busca?

Um padrão muito comum é procurar o menor valor possível:

```text
impossível  impossível  impossível  possível  possível  possível
```

Se é possível concluir uma tarefa em cinco minutos, ela também poderá ser concluída em seis, sete ou mais minutos. Assim, procuramos o primeiro tempo possível.

## Exemplo: máquinas produzindo itens

Uma fábrica possui `n` máquinas. A máquina `i` demora `tempo[i]` segundos para produzir um item. Todas as máquinas trabalham simultaneamente, e queremos produzir pelo menos `alvo` itens.

Precisamos encontrar o menor tempo necessário.

### Definindo a resposta candidata

Nossa resposta candidata será uma quantidade de segundos chamada `tempoTotal`.

### Criando a função de verificação

Em `tempoTotal` segundos, a máquina `i` produz:

$$
\left\lfloor\frac{\text{tempoTotal}}{\text{tempo}[i]}\right\rfloor
$$

itens.

Somamos a produção de todas as máquinas e verificamos se ela é pelo menos `alvo`:

```cpp
vector<long long> tempo;
long long alvo;

bool consegue(long long tempoTotal) {
    long long producao = 0;

    for (long long duracao : tempo) {
        producao += tempoTotal / duracao;

        if (producao >= alvo) {
            return true;
        }
    }

    return false;
}
```

Interromper o loop assim que atingimos o objetivo também evita que `producao` cresça desnecessariamente.

### Verificando a monotonicidade

Se é possível produzir todos os itens em determinado tempo, também será possível produzi-los em qualquer tempo maior.

Temos, portanto:

```text
não  não  não  não  sim  sim  sim  sim
```

Precisamos encontrar o primeiro `sim`.

### Escolhendo os limites

O menor tempo possível é `0`.

Como limite superior, podemos considerar o tempo necessário para que apenas a máquina mais rápida produza todos os itens:

$$
\min(\text{tempo})\cdot\text{alvo}
$$

Esse limite certamente é suficiente.

### Solução completa

```cpp
#include <bits/stdc++.h>

using namespace std;

vector<long long> tempo;
long long alvo;

bool consegue(long long tempoTotal) {
    long long producao = 0;

    for (long long duracao : tempo) {
        producao += tempoTotal / duracao;

        if (producao >= alvo) {
            return true;
        }
    }

    return false;
}

int main() {
    int n;
    cin >> n >> alvo;

    tempo.resize(n);

    for (long long &duracao : tempo) {
        cin >> duracao;
    }

    long long esquerda = 0;
    long long direita =
        *min_element(tempo.begin(), tempo.end()) * alvo;

    while (esquerda < direita) {
        long long meio = esquerda + (direita - esquerda) / 2;

        if (consegue(meio)) {
            direita = meio;
        } else {
            esquerda = meio + 1;
        }
    }

    cout << esquerda << "\n";
}
```

Se a função `consegue` percorre as `n` máquinas, ela custa $O(n)$. A busca binária realiza $O(\log R)$ iterações, em que `R` é o limite superior. Portanto, a complexidade total é:

$$
O(n\log R)
$$

## Outro exemplo: capacidade de um navio

Considere uma sequência de pacotes que deve ser transportada, na ordem apresentada, em no máximo `dias` dias. Queremos encontrar a menor capacidade possível para o navio.

Uma capacidade candidata pode ser verificada com uma simulação:

```cpp
bool consegue(long long capacidade) {
    int diasUsados = 1;
    long long cargaAtual = 0;

    for (int peso : pesos) {
        if (cargaAtual + peso > capacidade) {
            diasUsados++;
            cargaAtual = 0;
        }

        cargaAtual += peso;
    }

    return diasUsados <= dias;
}
```

Os limites podem ser definidos da seguinte forma:

- a capacidade mínima é o peso do pacote mais pesado;
- a capacidade máxima é a soma dos pesos de todos os pacotes.

Se determinada capacidade é suficiente, qualquer capacidade maior também será. Novamente, procuramos o primeiro valor válido.

## Como escolher os limites

Escolher bons limites é uma das partes mais importantes da busca binária na resposta.

O limite inferior deve ser um valor menor ou igual à resposta, enquanto o limite superior deve ser maior ou igual à resposta.

Algumas estratégias comuns são:

- usar o menor e o maior valor permitidos pelo enunciado;
- construir uma solução certamente válida para obter o limite superior;
- usar `0`, `1`, $10^9$ ou $10^{18}$ quando os limites permitem;
- utilizar o maior elemento, o menor elemento ou a soma dos elementos;
- dobrar progressivamente o limite superior até encontrar um valor válido.

Não escolha um limite apenas porque ele “parece grande”. É necessário justificar que a resposta está dentro do intervalo.

## Busca binária com números reais

Alguns problemas possuem uma resposta real, como uma distância, um tempo ou uma temperatura.

Nesses casos, não podemos utilizar `meio + 1` ou `meio - 1`, pois não existe um próximo número real bem definido. Entre dois valores reais diferentes, sempre existem outros valores.

Uma forma simples de implementar a busca é realizar uma quantidade fixa de iterações:

```cpp
double esquerda = menorValor;
double direita = maiorValor;

for (int iteracao = 0; iteracao < 100; iteracao++) {
    double meio = (esquerda + direita) / 2.0;

    if (consegue(meio)) {
        direita = meio;
    } else {
        esquerda = meio;
    }
}

cout << fixed << setprecision(10) << direita << "\n";
```

Após cem iterações, o intervalo terá sido dividido por $2^{100}$, oferecendo precisão suficiente para a maioria dos problemas de programação competitiva.

Também é possível utilizar uma condição baseada em erro:

```cpp
while (direita - esquerda > 1e-7) {
    double meio = (esquerda + direita) / 2.0;

    if (consegue(meio)) {
        direita = meio;
    } else {
        esquerda = meio;
    }
}
```

Entretanto, o número fixo de iterações costuma ser mais simples e evita alguns problemas de precisão na condição do `while`.

## Exemplo com números reais: ponto de encontro

Considere `n` pessoas em uma reta. A pessoa `i` começa na posição `x[i]` e pode se mover com velocidade máxima `v[i]`. Queremos descobrir o menor tempo para que todas possam se encontrar em algum ponto.

Em um tempo `t`, a pessoa `i` consegue alcançar o intervalo:

$$
[x_i-v_i\cdot t,\;x_i+v_i\cdot t]
$$

Para que todos consigam se encontrar, a interseção desses intervalos precisa ser não vazia.

```cpp
vector<double> posicao;
vector<double> velocidade;

bool consegue(double tempo) {
    double limiteEsquerdo = -1e30;
    double limiteDireito = 1e30;

    for (int i = 0; i < posicao.size(); i++) {
        limiteEsquerdo = max(
            limiteEsquerdo,
            posicao[i] - velocidade[i] * tempo
        );

        limiteDireito = min(
            limiteDireito,
            posicao[i] + velocidade[i] * tempo
        );
    }

    return limiteEsquerdo <= limiteDireito;
}
```

Se todos conseguem se encontrar em determinado tempo, também conseguem se encontrar em qualquer tempo maior. Assim, podemos realizar uma busca binária pelo primeiro tempo válido.

```cpp
double esquerda = 0.0;
double direita = 1e18;

for (int iteracao = 0; iteracao < 100; iteracao++) {
    double meio = (esquerda + direita) / 2.0;

    if (consegue(meio)) {
        direita = meio;
    } else {
        esquerda = meio;
    }
}

cout << fixed << setprecision(10) << direita << "\n";
```

## Precisão e comparação de `double`

Números representados por `double` podem sofrer pequenos erros de aproximação. Por isso, geralmente não devemos testar igualdade diretamente:

```cpp
if (a == b) {
    // Pode falhar devido à precisão.
}
```

Quando for necessário verificar se dois valores estão suficientemente próximos, podemos utilizar uma tolerância:

```cpp
const double EPS = 1e-9;

if (abs(a - b) <= EPS) {
    cout << "Valores aproximadamente iguais.\n";
}
```

O valor adequado de `EPS` depende da tolerância exigida pelo problema.

Ao imprimir uma resposta real, utilize `fixed` e `setprecision`:

```cpp
cout << fixed << setprecision(10) << resposta << "\n";
```

Imprimir mais casas decimais que o mínimo exigido normalmente é seguro.

## Erros comuns

### Aplicar busca binária sem monotonicidade

Antes de implementar, escreva alguns valores candidatos e determine o resultado da função de verificação. Ela deve mudar no máximo uma vez.

### Procurar o lado errado

Para encontrar o primeiro valor válido em uma sequência `não...sim`, um valor válido deve mover o limite direito:

```cpp
if (valido(meio)) {
    direita = meio;
}
```

Para encontrar o último valor válido em uma sequência `sim...não`, um valor válido deve mover o limite esquerdo:

```cpp
if (valido(meio)) {
    esquerda = meio;
}
```

### Não reduzir o intervalo

Atualizações como `esquerda = meio` podem gerar um loop infinito quando o meio é arredondado para baixo. Para procurar o último valor válido, calcule o meio com arredondamento para cima.

### Escolher limites incorretos

Se a resposta não estiver dentro do intervalo inicial, nenhuma implementação da busca binária conseguirá encontrá-la.

### Estourar o tipo numérico

Produtos como `menorTempo * alvo` podem exigir `long long`. Somas realizadas dentro da função de verificação também podem ultrapassar o limite se não forem interrompidas após atingir o objetivo.

### Misturar divisão inteira e real

Em uma expressão com inteiros, o C++ realiza divisão inteira:

```cpp
double resultado = 1 / 2; // resultado recebe 0
```

Para realizar uma divisão real, pelo menos um dos operandos deve ser real:

```cpp
double resultado = 1.0 / 2.0; // resultado recebe 0.5
```

### Usar `+ 1` em uma busca real

Em uma busca com `double`, atualize os limites diretamente para `meio`. Operações como `meio + 1` descartariam uma região inteira de respostas possíveis.

## Complexidade

Se a função de verificação custa $O(f(n))$ e o intervalo possui tamanho `R`, uma busca binária inteira custa:

$$
O(f(n)\log R)
$$

Por exemplo, se verificamos `n` máquinas a cada iteração, a complexidade é $O(n\log R)$.

Em uma busca real com cem iterações, a função de verificação é chamada exatamente cem vezes. Assim, sua complexidade pode ser escrita como:

$$
O(100\cdot f(n))=O(f(n))
$$

Embora o Big O remova a constante `100`, ela continua relevante para estimar o tempo real do programa.

## Roteiro para reconhecer a técnica

Ao encontrar um problema de otimização, faça as seguintes perguntas:

1. O problema pede o menor ou o maior valor possível?
2. Consigo verificar se uma resposta candidata funciona?
3. Se um valor funciona, todos os valores maiores também funcionam?
4. Ou, se um valor funciona, todos os valores menores também funcionam?
5. Consigo definir limites que certamente contêm a resposta?
6. A verificação é rápida o suficiente para ser chamada várias vezes?

Se as respostas indicarem uma sequência monotônica, a busca binária na resposta provavelmente é uma boa opção.

## Exercícios recomendados

1. [CSES - Factory Machines](https://cses.fi/problemset/task/1620)
2. [LeetCode 875 - Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
3. [LeetCode 1011 - Capacity to Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)
4. [Codeforces 165B - Burning Midnight Oil](https://codeforces.com/problemset/problem/165/B)
5. [Codeforces 1613C - Poisoned Dagger](https://codeforces.com/problemset/problem/1613/C)
6. [Codeforces 782B - The Meeting Place Cannot Be Changed](https://codeforces.com/problemset/problem/782/B)

## Resumo

Neste capítulo, aprendemos que:

- a busca binária elimina metade do espaço de busca a cada iteração;
- `binary_search` verifica se um valor existe em um intervalo ordenado;
- `lower_bound` encontra o primeiro elemento maior ou igual a um valor;
- `upper_bound` encontra o primeiro elemento estritamente maior que um valor;
- podemos procurar o primeiro ou o último valor que satisfaz uma condição;
- a função de verificação precisa ser monotônica;
- a busca binária na resposta procura diretamente o menor ou o maior valor possível;
- os limites precisam conter a resposta e devem ser justificados;
- buscas inteiras utilizam atualizações com `+ 1` ou `- 1`;
- buscas com `double` podem utilizar uma quantidade fixa de iterações;
- comparações com números reais devem considerar erros de precisão;
- a complexidade total depende do custo da função de verificação e da quantidade de iterações da busca.
