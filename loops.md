# Loops

## Introdução

Até agora, nossos programas executavam cada instrução apenas uma vez, seguindo a ordem em que elas apareciam no código. Porém, muitos problemas exigem que uma mesma ação seja repetida diversas vezes.

Imagine, por exemplo, que precisamos ler oito números e calcular a soma deles. Poderíamos criar oito variáveis e escrever oito comandos `cin`, mas isso deixaria o código longo e repetitivo. Se fossem mil números, essa abordagem seria praticamente inviável.

É para resolver situações como essa que utilizamos os **comandos de repetição**, também chamados de **loops** ou **laços de repetição**.

Um loop executa um bloco de código repetidamente enquanto uma determinada condição for satisfeita.

```cpp
int soma = 0;

for (int i = 0; i < 8; i++) {
    int valor;
    cin >> valor;
    soma += valor;
}
```

Nesse exemplo, o mesmo trecho é executado oito vezes. Em cada repetição, um número é lido e acrescentado à soma.

Cada execução do bloco de um loop recebe o nome de **iteração**.

## O comando `for`

O `for` é utilizado principalmente quando sabemos quantas vezes um bloco deve ser repetido.

Sua estrutura é:

```cpp
for (inicialização; condição; atualização) {
    // Código que será repetido
}
```

Observe o exemplo:

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << "\n";
}
```

A saída será:

```text
0
1
2
3
4
```

Esse loop possui três partes:

1. **Inicialização:** `int i = 0`
   - Cria a variável `i` e atribui a ela o valor inicial `0`.

2. **Condição:** `i < 5`
   - O loop continua enquanto essa condição for verdadeira.

3. **Atualização:** `i++`
   - Depois de cada iteração, o valor de `i` aumenta em uma unidade.

O funcionamento pode ser resumido da seguinte forma:

1. A inicialização é executada uma vez.
2. A condição é verificada.
3. Se a condição for verdadeira, o bloco é executado.
4. A atualização é realizada.
5. O processo volta para a verificação da condição.

Quando a condição se torna falsa, o loop termina.

### Começando em `0` ou em `1`

Na programação, é muito comum contar posições começando em `0`:

```cpp
for (int i = 0; i < n; i++) {
    cout << i << "\n";
}
```

Esse loop imprime os valores de `0` até `n - 1` e executa exatamente `n` vezes.

Quando o problema trabalha naturalmente com números de `1` até `n`, podemos escrever:

```cpp
for (int i = 1; i <= n; i++) {
    cout << i << "\n";
}
```

Preste atenção à diferença entre `<` e `<=`. Ela é uma das principais causas de erros em loops.

## Acumuladores

Um **acumulador** é uma variável utilizada para guardar um resultado que está sendo construído ao longo das iterações.

O código abaixo calcula a soma dos números de `1` até `n`:

```cpp
int n;
cin >> n;

long long soma = 0;

for (int i = 1; i <= n; i++) {
    soma += i;
}

cout << soma << "\n";
```

Se `n = 4`, o valor de `soma` muda da seguinte forma:

| Iteração | Valor de `i` | Valor de `soma` |
|---:|---:|---:|
| Inicial | - | 0 |
| 1 | 1 | 1 |
| 2 | 2 | 3 |
| 3 | 3 | 6 |
| 4 | 4 | 10 |

É importante inicializar o acumulador com um valor adequado. Para uma soma, geralmente começamos com `0`. Para uma multiplicação, normalmente começamos com `1`.

## Contadores

Um **contador** registra quantas vezes determinado evento aconteceu.

O exemplo abaixo lê `n` números e conta quantos deles são positivos:

```cpp
int n;
cin >> n;

int quantidade = 0;

for (int i = 0; i < n; i++) {
    int valor;
    cin >> valor;

    if (valor > 0) {
        quantidade++;
    }
}

cout << quantidade << "\n";
```

O contador só é incrementado quando a condição `valor > 0` é verdadeira.

## O comando `while`

O `while` repete um bloco enquanto sua condição for verdadeira.

Sua estrutura é:

```cpp
while (condição) {
    // Código que será repetido
}
```

Por exemplo:

```cpp
int contador = 0;

while (contador < 5) {
    cout << contador << "\n";
    contador++;
}
```

Assim como o exemplo com `for`, esse código imprime os números de `0` até `4`.

O `while` é especialmente útil quando não sabemos previamente quantas repetições serão necessárias.

Considere duas pontuações `a` e `b`. A cada rodada, `a` é triplicada e `b` é duplicada. Queremos descobrir quantas rodadas são necessárias para que `a` fique maior que `b`:

```cpp
int a, b;
cin >> a >> b;

int rodadas = 0;

while (a <= b) {
    a *= 3;
    b *= 2;
    rodadas++;
}

cout << rodadas << "\n";
```

Não sabemos antecipadamente quantas rodadas serão necessárias. Sabemos apenas que devemos continuar enquanto `a <= b`.

## `for` ou `while`?

Em muitos casos, um mesmo problema pode ser resolvido com qualquer uma das estruturas.

Use normalmente:

- `for` quando a quantidade de repetições é conhecida;
- `while` quando a repetição depende de uma condição e não sabemos quantas iterações serão necessárias.

Por exemplo, para ler exatamente `n` valores, o `for` costuma ser mais natural:

```cpp
for (int i = 0; i < n; i++) {
    int valor;
    cin >> valor;
}
```

Para dividir um número repetidamente até ele chegar a `1`, o `while` costuma ser mais adequado:

```cpp
while (n > 1) {
    n /= 2;
}
```

## Loops aninhados

Um loop pode ser colocado dentro de outro. Nesse caso, dizemos que os loops estão **aninhados**.

```cpp
for (int linha = 0; linha < 3; linha++) {
    for (int coluna = 0; coluna < 4; coluna++) {
        cout << "#";
    }

    cout << "\n";
}
```

A saída será:

```text
####
####
####
```

Para cada uma das três linhas, o loop interno imprime quatro caracteres. Portanto, o comando `cout << "#"` é executado doze vezes.

Loops aninhados são comuns na construção de desenhos e, futuramente, no processamento de matrizes.

## Controlando um loop

### `break`

O comando `break` encerra imediatamente o loop mais próximo.

```cpp
for (int i = 1; i <= 100; i++) {
    if (i == 7) {
        break;
    }

    cout << i << "\n";
}
```

Esse código imprime os números de `1` até `6`. Quando `i` se torna `7`, o loop é encerrado.

### `continue`

O comando `continue` pula o restante da iteração atual e segue para a próxima.

```cpp
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;
    }

    cout << i << "\n";
}
```

Esse código imprime `1`, `2`, `4` e `5`.

Esses comandos são úteis, mas devem ser utilizados com cuidado para não tornar o fluxo do programa confuso.

## Erros comuns

### Esquecer a atualização

```cpp
int i = 0;

while (i < 5) {
    cout << i << "\n";
}
```

Como `i` nunca é alterado, a condição `i < 5` será sempre verdadeira. O programa ficará preso em um **loop infinito**.

A correção é atualizar `i` dentro do loop:

```cpp
while (i < 5) {
    cout << i << "\n";
    i++;
}
```

### Errar a condição de parada

```cpp
for (int i = 1; i < n; i++) {
    cout << i << "\n";
}
```

Esse código não imprime `n`. Se a intenção era imprimir de `1` até `n`, a condição deveria ser `i <= n`.

### Colocar um ponto e vírgula após o loop

```cpp
for (int i = 0; i < n; i++); {
    cout << "Olá!\n";
}
```

O ponto e vírgula encerra o `for`. Assim, o bloco seguinte não pertence ao loop e é executado apenas uma vez.

### Alterar a variável errada

Em loops aninhados, confira se cada atualização modifica a variável correta:

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
        // Use j++ no loop interno, não i++.
    }
}
```

## Relação com a complexidade

Loops permitem repetir instruções, mas cada repetição exige tempo de processamento.

Um loop que executa `n` vezes realiza aproximadamente `n` vezes o trabalho presente em seu interior. Dois loops aninhados que executam `n` vezes cada podem realizar aproximadamente $n^2$ operações.

Por isso, não basta construir um programa que produza a resposta correta: também precisamos verificar se ele consegue terminar dentro do limite de tempo. Esse será o assunto do próximo capítulo.

## Exercícios recomendados

1. [beecrowd 1067 - Números Ímpares](https://judge.beecrowd.com/pt/problems/view/1067)
2. [beecrowd 1071 - Soma de Ímpares Consecutivos I](https://judge.beecrowd.com/pt/problems/view/1071)
3. [Codeforces 791A - Bear and Big Brother](https://codeforces.com/problemset/problem/791/A)
4. [Codeforces 546A - Soldier and Bananas](https://codeforces.com/problemset/problem/546/A)
5. [Codeforces 510A - Fox And Snake](https://codeforces.com/problemset/problem/510/A)
6. [beecrowd 1151 - Fibonacci Fácil](https://judge.beecrowd.com/pt/problems/view/1151)

## Resumo

Neste capítulo, aprendemos que:

- loops permitem executar um bloco de código várias vezes;
- cada repetição de um loop é chamada de iteração;
- o `for` é indicado principalmente quando sabemos a quantidade de repetições;
- o `while` é indicado principalmente quando repetimos enquanto uma condição for verdadeira;
- acumuladores guardam resultados construídos durante as iterações;
- contadores registram quantas vezes determinado evento ocorreu;
- loops podem ser aninhados;
- uma condição de parada incorreta pode provocar um loop infinito;
- a quantidade de iterações influencia diretamente o tempo de execução do programa.
