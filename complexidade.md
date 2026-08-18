# Complexidade de Algoritmos

## Introdução

Depois de aprender loops, nossos programas deixam de executar todas as instruções apenas uma vez. Um mesmo comando pode ser executado uma, dez, mil ou milhões de vezes.

Isso afeta diretamente o tempo necessário para o programa terminar.

Considere duas soluções que produzem exatamente a mesma resposta:

- a primeira realiza mil operações;
- a segunda realiza um bilhão de operações.

Embora ambas estejam corretas, a segunda pode não terminar dentro do limite de tempo do problema.

A **complexidade de um algoritmo** descreve como a quantidade de operações cresce de acordo com o tamanho da entrada. Essa análise nos ajuda a estimar se uma solução será rápida o suficiente antes mesmo de implementá-la.

## Tamanho da entrada

Normalmente, utilizamos a letra $n$ para representar o tamanho da entrada.

Dependendo do problema, $n$ pode representar:

- a quantidade de números;
- o tamanho de uma sequência;
- a quantidade de pessoas;
- a quantidade de linhas de uma tabela;
- ou qualquer outra medida relevante.

Os limites apresentados no enunciado indicam o maior valor que $n$ pode assumir. Esses limites são essenciais para escolher uma solução adequada.

## Notação Big O

Utilizamos a notação **Big O** para representar a complexidade de um algoritmo. Ela é escrita como $O(1)$, $O(n)$, $O(n^2)$ e assim por diante.

O Big O não procura calcular o tempo exato em segundos. Ele descreve principalmente como o número de operações cresce quando a entrada aumenta.

Por exemplo:

- se dobrar $n$ não altera significativamente a quantidade de operações, temos um algoritmo constante;
- se dobrar $n$ aproximadamente dobra o trabalho, temos um algoritmo linear;
- se dobrar $n$ aproximadamente quadruplica o trabalho, temos um algoritmo quadrático.

## Complexidade constante: $O(1)$

Observe o algoritmo:

```cpp
int a, b;
cin >> a >> b;

cout << a + b << "\n";
```

Independentemente dos valores de `a` e `b`, o programa realiza uma quantidade fixa de operações. Portanto, sua complexidade é $O(1)$, chamada de **complexidade constante**.

Outro exemplo:

```cpp
if (a > b) {
    cout << a << "\n";
} else {
    cout << b << "\n";
}
```

Apenas um dos blocos será executado e não existe nenhuma repetição dependente do tamanho da entrada. A complexidade também é $O(1)$.

## Complexidade linear: $O(n)$

Considere um programa que lê `n` números e calcula a soma deles:

```cpp
int n;
cin >> n;

long long soma = 0;

for (int i = 0; i < n; i++) {
    int valor;
    cin >> valor;
    soma += valor;
}

cout << soma << "\n";
```

O loop executa `n` vezes. Em cada iteração, realizamos uma quantidade constante de operações: uma leitura e uma soma.

Assim, o número de operações cresce proporcionalmente a `n`, e a complexidade é $O(n)$, chamada de **complexidade linear**.

Se `n` dobrar, a quantidade aproximada de trabalho também dobrará.

## Complexidade quadrática: $O(n^2)$

Agora observe dois loops aninhados:

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        cout << i + j << "\n";
    }
}
```

Para cada uma das `n` iterações do loop externo, o loop interno também executa `n` vezes.

Portanto, o comando `cout` é executado

$$
n \cdot n = n^2
$$

vezes. A complexidade é $O(n^2)$, chamada de **complexidade quadrática**.

Se `n = 10`, o bloco interno executa aproximadamente cem vezes. Se `n = 1000`, ele executa aproximadamente um milhão de vezes.

Analisar a quantidade de loops aninhados é um bom primeiro passo para estimar a complexidade, embora nem todo código com dois loops seja necessariamente $O(n^2)$.

## Loops consecutivos e loops aninhados

Dois loops consecutivos não possuem o mesmo custo de dois loops aninhados.

### Loops consecutivos

```cpp
for (int i = 0; i < n; i++) {
    cout << i << "\n";
}

for (int i = 0; i < n; i++) {
    cout << i << "\n";
}
```

O primeiro loop executa `n` vezes e o segundo também:

$$
n+n=2n
$$

Ignorando a constante `2`, a complexidade é $O(n)$.

### Loops aninhados

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        cout << i << " " << j << "\n";
    }
}
```

Aqui, multiplicamos a quantidade de iterações:

$$
n \cdot n=n^2
$$

Logo, a complexidade é $O(n^2)$.

Como regra inicial:

- blocos consecutivos geralmente têm seus custos somados;
- blocos aninhados geralmente têm seus custos multiplicados.

## Ignorando constantes

Considere:

```cpp
for (int i = 0; i < 3 * n; i++) {
    cout << i << "\n";
}
```

O loop executa `3n` vezes. Ainda assim, representamos sua complexidade como $O(n)$.

No Big O, constantes multiplicativas são ignoradas:

$$
O(3n)=O(n)
$$

Isso acontece porque estamos interessados no comportamento do algoritmo quando a entrada cresce, e não em uma contagem exata de instruções.

Isso não significa que constantes nunca importam na prática. Um algoritmo que realiza `100n` operações provavelmente será mais lento que outro que realiza `n`, mas ambos apresentam crescimento linear.

## Considerando o termo dominante

Considere um algoritmo que realiza $n^2+n+10$ operações.

Quando `n` é grande, o termo $n^2$ cresce muito mais rapidamente que os demais. Por isso, mantemos apenas o termo dominante:

$$
O(n^2+n+10)=O(n^2)
$$

Outros exemplos:

$$
O(n+500)=O(n)
$$

$$
O(n^3+n^2+n)=O(n^3)
$$

## Complexidade logarítmica: $O(\log n)$

Observe o código:

```cpp
while (n > 1) {
    n /= 2;
}
```

Em cada iteração, o valor de `n` é dividido por `2`.

Se `n = 16`, os valores serão:

```text
16 → 8 → 4 → 2 → 1
```

Foram necessárias apenas quatro divisões. Mesmo que `n` seja muito grande, a quantidade de iterações cresce lentamente.

Essa complexidade é representada por $O(\log n)$ e aparece, por exemplo, na busca binária.

## Complexidade $O(n\log n)$

Alguns algoritmos realizam um trabalho logarítmico para cada um dos `n` elementos, resultando em $O(n\log n)$.

Essa complexidade aparece frequentemente em algoritmos eficientes de ordenação. Quando utilizamos `sort` em `n` elementos, consideramos normalmente uma complexidade de $O(n\log n)$.

Você estudará esses algoritmos com mais detalhes nos próximos capítulos.

## Complexidade cúbica: $O(n^3)$

Três loops de tamanho `n` completamente aninhados produzem uma complexidade cúbica:

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        for (int k = 0; k < n; k++) {
            cout << i + j + k << "\n";
        }
    }
}
```

O bloco mais interno é executado aproximadamente $n^3$ vezes. Esse tipo de solução só é adequado para valores relativamente pequenos de `n`.

## Estimando pelo limite da entrada

Em programação competitiva, costuma-se considerar que um programa em C++ consegue realizar aproximadamente entre $10^7$ e $10^8$ operações simples por segundo. Essa é apenas uma estimativa: o tempo real depende das operações, do computador, da linguagem e do limite de tempo.

A tabela abaixo serve como referência inicial:

| Complexidade | Nome | Valor aproximado de `n` |
|---|---|---:|
| $O(1)$ | Constante | Qualquer limite comum |
| $O(\log n)$ | Logarítmica | Até valores muito grandes, como $10^{18}$ |
| $O(n)$ | Linear | Até cerca de $10^7$ |
| $O(n\log n)$ | Linearítmica | Até cerca de $10^6$ |
| $O(n^2)$ | Quadrática | Até cerca de $10^4$ |
| $O(n^3)$ | Cúbica | Até cerca de $400$ ou $500$ |
| $O(2^n)$ | Exponencial | Até cerca de $20$ ou $25$ |
| $O(n!)$ | Fatorial | Até cerca de $10$ ou $11$ |

Esses valores não são regras absolutas. Sempre considere também:

- o limite de tempo do problema;
- o número de casos de teste;
- o tipo de operação realizada;
- a linguagem utilizada;
- as constantes escondidas pelo Big O.

## Vários casos de teste

Quando existem vários casos de teste, precisamos considerar o trabalho total.

```cpp
int t;
cin >> t;

while (t--) {
    int n;
    cin >> n;

    for (int i = 0; i < n; i++) {
        // Operação constante
    }
}
```

Se todos os casos tiverem tamanho `n`, a complexidade será $O(t\cdot n)$.

Muitos enunciados informam que a soma dos valores de `n` entre todos os casos não ultrapassa determinado limite. Nesse caso, devemos utilizar essa soma para estimar o número total de operações.

## Condicionais dentro de loops

Adicionar um `if` com operações constantes dentro de um loop não muda sua ordem de complexidade:

```cpp
for (int i = 0; i < n; i++) {
    if (i % 2 == 0) {
        cout << i << "\n";
    }
}
```

O loop ainda testa todos os `n` valores. Portanto, sua complexidade continua sendo $O(n)$.

Por outro lado, se o bloco do `if` contiver outro loop, será necessário analisar quantas vezes esse segundo loop poderá ser executado.

## Melhor caso e pior caso

Algoritmos podem executar quantidades diferentes de operações dependendo da entrada.

```cpp
for (int i = 1; i <= n; i++) {
    if (i == procurado) {
        break;
    }
}
```

Se o valor procurado estiver logo no início, o loop termina rapidamente. Se estiver no final ou não existir, o programa percorre todos os valores.

Em programação competitiva, normalmente analisamos o **pior caso**, pois precisamos garantir que a solução funcione para qualquer entrada válida. Nesse exemplo, a complexidade de pior caso é $O(n)$.

## Complexidade de memória

Além do tempo, também podemos analisar quanta memória um algoritmo utiliza.

Um programa que guarda apenas algumas variáveis utiliza espaço constante, representado por $O(1)$:

```cpp
int a, b, soma;
```

Se futuramente armazenarmos `n` valores em um vetor, utilizaremos espaço $O(n)$.

Por enquanto, o mais importante é compreender a complexidade de tempo, mas a memória também deve respeitar o limite informado no enunciado.

## Exemplos de análise

### Exemplo 1

```cpp
int resposta = n * (n + 1) / 2;
```

A expressão é calculada uma única vez. Complexidade: $O(1)$.

### Exemplo 2

```cpp
for (int i = 0; i < n; i++) {
    cout << i << "\n";
}
```

O bloco executa `n` vezes. Complexidade: $O(n)$.

### Exemplo 3

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        cout << i + j << "\n";
    }
}
```

Cada loop executa `n` vezes e eles estão aninhados. Complexidade: $O(n^2)$.

### Exemplo 4

```cpp
for (int i = 0; i < n; i++) {
    cout << i << "\n";
}

for (int j = 0; j < n * n; j++) {
    cout << j << "\n";
}
```

O primeiro loop custa $O(n)$ e o segundo custa $O(n^2)$. O termo dominante é $n^2$, então a complexidade total é $O(n^2)$.

## Como analisar uma solução

Ao analisar a complexidade de um código, siga estes passos:

1. Identifique o tamanho da entrada e seus limites.
2. Encontre os loops presentes no código.
3. Determine quantas vezes cada loop pode executar.
4. Verifique se os loops são consecutivos ou aninhados.
5. Observe se a variável de controle aumenta de um em um ou é multiplicada/dividida.
6. Some os blocos consecutivos e multiplique os aninhados.
7. Remova constantes e mantenha o termo que cresce mais rapidamente.
8. Compare a complexidade obtida com os limites do problema.

## Exercícios de fixação

Determine a complexidade dos códigos abaixo antes de consultar as respostas.

### Exercício 1

```cpp
cout << n * 2 << "\n";
```

<details>
<summary>Resposta</summary>

$O(1)$, pois a quantidade de operações não depende do valor de `n`.

</details>

### Exercício 2

```cpp
for (int i = 0; i < n; i++) {
    cout << i << "\n";
}
```

<details>
<summary>Resposta</summary>

$O(n)$, pois o loop executa `n` vezes.

</details>

### Exercício 3

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        cout << i * j << "\n";
    }
}
```

<details>
<summary>Resposta</summary>

$O(n^2)$, pois existem dois loops de tamanho `n` aninhados.

</details>

### Exercício 4

```cpp
for (int i = 0; i < n; i++) {
    cout << i << "\n";
}

for (int j = 0; j < n; j++) {
    cout << j << "\n";
}
```

<details>
<summary>Resposta</summary>

$O(n)$. Os loops são consecutivos, então temos $O(n+n)=O(2n)=O(n)$.

</details>

### Exercício 5

```cpp
while (n > 0) {
    n /= 2;
}
```

<details>
<summary>Resposta</summary>

$O(\log n)$, pois o valor de `n` é dividido por `2` a cada iteração.

</details>

## Resumo

Neste capítulo, aprendemos que:

- a complexidade estima como o trabalho de um algoritmo cresce com a entrada;
- usamos a notação Big O para representar esse crescimento;
- instruções independentes da entrada geralmente são $O(1)$;
- um loop que percorre `n` elementos geralmente é $O(n)$;
- dois loops de tamanho `n` completamente aninhados geralmente são $O(n^2)$;
- loops consecutivos têm seus custos somados, enquanto loops aninhados geralmente têm seus custos multiplicados;
- constantes e termos menores são removidos na notação Big O;
- dividir repetidamente o tamanho da entrada costuma produzir $O(\log n)$;
- os limites do enunciado ajudam a determinar qual complexidade é aceitável;
- normalmente analisamos o pior caso da solução;
- uma solução correta também precisa respeitar os limites de tempo e memória.
