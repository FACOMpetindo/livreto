# Condicionais

## 📚 Introdução

Até agora, nossos programas executavam as instruções sempre na mesma ordem. Porém, em muitos problemas precisamos que o programa tome decisões diferentes dependendo dos valores recebidos como entrada.

Por exemplo, podemos querer verificar se um número é positivo, descobrir qual de dois números é maior ou determinar se uma pessoa pode participar de determinada atividade.

Para isso, utilizamos as **estruturas condicionais**.

Em C++, as principais estruturas condicionais são:

- `if`;
- `else if`;
- `else`.

Elas permitem executar diferentes trechos do código dependendo de uma condição.

## 🔎 If

A estrutura `if` significa, basicamente, **"se"**.

Ela recebe uma condição entre parênteses. Caso essa condição seja verdadeira, o código dentro das chaves será executado.

```cpp
if (condicao) {
    // código executado caso a condição seja verdadeira
}
```

Por exemplo:

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int idade;

    cin >> idade;

    if (idade >= 18) {
        cout << "Maior de idade\n";
    }
}
```

Nesse exemplo, a mensagem será impressa somente quando `idade` for maior ou igual a `18`.

> **Atenção:** em C++, a condição do `if` deve estar entre parênteses.

## 🔀 Else

Podemos utilizar `else` quando queremos executar um código caso a condição do `if` seja falsa.

```cpp
if (condicao) {
    // caso a condição seja verdadeira
}
else {
    // caso a condição seja falsa
}
```

Por exemplo:

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int idade;

    cin >> idade;

    if (idade >= 18) {
        cout << "Maior de idade\n";
    }
    else {
        cout << "Menor de idade\n";
    }
}
```

Agora sempre teremos uma das duas mensagens como saída.

Se `idade` for maior ou igual a `18`, o primeiro bloco será executado. Caso contrário, o bloco do `else` será executado.

## 🔢 Operadores relacionais

Para construir condições, precisamos comparar valores.

Os principais operadores relacionais do C++ são:

| Operador | Significado    |
| :------: | -------------- |
|   `>`    | maior que      |
|   `>=`   | maior ou igual |
|   `<`    | menor que      |
|   `<=`   | menor ou igual |
|   `==`   | igual          |
|   `!=`   | diferente      |

Por exemplo:

```cpp
int x = 10;

if (x > 5) {
    cout << "x e maior que 5\n";
}
```

A condição `x > 5` será verdadeira, pois `10` é maior que `5`.

### ⚠️ Cuidado com `=` e `==`

Um erro muito comum entre iniciantes é confundir o operador de atribuição `=` com o operador de comparação `==`.

```cpp
x = 5;
```

significa **atribuir** o valor `5` a `x`.

Já:

```cpp
x == 5
```

significa **verificar se** `x` é igual a `5`.

Por exemplo:

```cpp
if (x == 5) {
    cout << "x vale 5\n";
}
```

## 🔗 Operadores lógicos

Às vezes, uma condição depende de mais de uma comparação. Para combinar condições, podemos utilizar os operadores lógicos.

Os principais são:

| Operador | Significado |
| :------: | ----------- | --- | --- |
|   `&&`   | E           |
|    `     |             | `   | OU  |
|   `!`    | NÃO         |

### Operador `&&`

O operador `&&` significa **E**.

As duas condições precisam ser verdadeiras para que o resultado seja verdadeiro.

```cpp
if (idade >= 18 && idade <= 60) {
    cout << "Idade dentro do intervalo\n";
}
```

Nesse caso, a mensagem será impressa somente quando `idade` for maior ou igual a `18` **e** menor ou igual a `60`.

### Operador `||`

O operador `||` significa **OU**.

Basta que uma das condições seja verdadeira.

```cpp
if (nota >= 7 || recuperacao == 1) {
    cout << "Aprovado\n";
}
```

Nesse exemplo, o aluno será considerado aprovado se tiver nota maior ou igual a `7` **ou** se tiver feito recuperação.

### Operador `!`

O operador `!` significa **NÃO** e inverte o resultado de uma condição.

```cpp
if (!aprovado) {
    cout << "Aluno reprovado\n";
}
```

Se `aprovado` for `true`, `!aprovado` será `false`. Se `aprovado` for `false`, `!aprovado` será `true`.

## 🔀 Else if

Podemos ter mais de duas possibilidades em um problema.

Nesse caso, utilizamos `else if`, que permite verificar novas condições caso as anteriores sejam falsas.

```cpp
if (condicao1) {
    // primeira possibilidade
}
else if (condicao2) {
    // segunda possibilidade
}
else {
    // nenhuma das condições anteriores
}
```

Por exemplo:

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int nota;

    cin >> nota;

    if (nota >= 7) {
        cout << "Aprovado\n";
    }
    else if (nota >= 5) {
        cout << "Recuperacao\n";
    }
    else {
        cout << "Reprovado\n";
    }
}
```

As condições são verificadas de cima para baixo.

Se `nota` for `8`, a primeira condição será verdadeira e o programa imprimirá `Aprovado`. As outras condições não serão verificadas.

Se `nota` for `6`, a primeira condição será falsa e a segunda será verdadeira, resultando em `Recuperacao`.

Caso nenhuma das condições seja verdadeira, o `else` será executado.

## 🧱 Chaves

As chaves `{}` delimitam o bloco de código que será executado quando uma condição for verdadeira.

Por exemplo:

```cpp
if (x > 0) {
    cout << "Positivo\n";
    x++;
}
```

Nesse caso, as duas instruções pertencem ao `if`.

Quando existe apenas uma instrução dentro do bloco, o C++ permite omitir as chaves:

```cpp
if (x > 0)
    cout << "Positivo\n";
```

O mesmo pode ser feito com `else` e `else if`.

Apesar disso, utilizar as chaves mesmo quando elas são opcionais pode tornar o código mais fácil de ler e evitar erros ao adicionar novas instruções posteriormente.

## 🔢 Condições encadeadas

Podemos combinar vários operadores para criar condições mais complexas.

Por exemplo:

```cpp
if (x >= 0 && x <= 100) {
    cout << "Valor valido\n";
}
```

Esse código verifica se `x` está no intervalo entre `0` e `100`, incluindo os extremos.

Também podemos utilizar várias condições:

```cpp
if (x > 0 && y > 0 && x == y) {
    cout << "Os valores sao iguais e positivos\n";
}
```

Ao escrever condições maiores, procure organizá-las de forma que seja fácil entender o que o programa está verificando.

## ❓ Operador ternário

Quando queremos escolher entre dois valores com base em uma condição simples, podemos utilizar o **operador ternário**.

Sua estrutura é:

```cpp
condicao ? valor_se_verdadeiro : valor_se_falso
```

Por exemplo:

```cpp
int x = 10;

string resposta = x > 0 ? "positivo" : "nao positivo";
```

Nesse caso, `resposta` receberá `"positivo"` porque `x > 0` é verdadeiro.

O mesmo código utilizando `if` seria:

```cpp
string resposta;

if (x > 0) {
    resposta = "positivo";
}
else {
    resposta = "nao positivo";
}
```

O operador ternário é útil quando queremos realizar uma escolha simples em uma única expressão.

Porém, para condições mais complexas, normalmente é melhor utilizar `if` e `else`, pois o código fica mais fácil de compreender.

## ✅ Variáveis booleanas

Uma variável do tipo `bool` representa um valor lógico.

Ela pode assumir apenas dois valores:

```cpp
true
false
```

Podemos utilizá-la para representar informações que possuem apenas duas possibilidades.

```cpp
bool aprovado = true;

if (aprovado) {
    cout << "Aprovado\n";
}
```

Também podemos atribuir diretamente o resultado de uma comparação a uma variável booleana:

```cpp
int x = 10;

bool positivo = x > 0;

if (positivo) {
    cout << "x e positivo\n";
}
```

Nesse exemplo, a expressão `x > 0` resulta em `true`, então `positivo` recebe esse valor.

Isso pode ser especialmente útil quando uma condição precisa ser calculada em uma parte do programa e utilizada posteriormente.

## 🧠 Como pensar em condicionais?

Ao resolver um problema, tente identificar quais situações diferentes podem acontecer.

Por exemplo, suponha que precisamos classificar um número:

```text
n > 0  → positivo
n < 0  → negativo
n = 0  → zero
```

Podemos transformar diretamente essa lógica em código:

```cpp
if (n > 0) {
    cout << "positivo\n";
}
else if (n < 0) {
    cout << "negativo\n";
}
else {
    cout << "zero\n";
}
```

Uma boa prática é primeiro pensar nas possibilidades do problema e só depois transformar essas possibilidades em condições no código.

## 🏁 Conclusão

As estruturas condicionais são uma das ferramentas mais básicas e importantes da programação. Elas permitem que nossos programas deixem de executar sempre as mesmas instruções e passem a tomar decisões de acordo com os dados recebidos.

Neste capítulo aprendemos:

- `if` para executar código quando uma condição é verdadeira;
- `else` para tratar o caso contrário;
- `else if` para lidar com várias possibilidades;
- operadores relacionais para comparar valores;
- operadores lógicos para combinar condições;
- operador ternário para escolhas simples;
- variáveis `bool` para representar valores verdadeiros ou falsos.

A partir daqui, poderemos combinar condicionais com os outros conceitos da linguagem para começar a resolver problemas cada vez mais interessantes.
