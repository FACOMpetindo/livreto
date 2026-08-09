# Sublime Text

## 📚 Introdução

Durante uma competição de programação, precisamos conseguir escrever, compilar e testar nossos programas rapidamente. Para isso, é importante utilizar um ambiente de desenvolvimento que facilite esse processo.

Neste treinamento utilizaremos o **Sublime Text**, um editor de texto leve e bastante rápido. Além de permitir escrever código, podemos configurá-lo para compilar e executar nossos programas diretamente pelo editor.

Uma das principais vantagens de configurar o Sublime dessa maneira é poder testar nossos programas utilizando arquivos de entrada e saída, de forma semelhante ao que fazemos ao submeter uma solução para um juiz online.

Neste capítulo aprenderemos a configurar o Sublime para programação competitiva e a utilizar esse ambiente para testar nossos códigos.

## 📝 Organização do ambiente

Para facilitar os testes, utilizaremos três arquivos principais:

- um arquivo `.cpp`, que contém o nosso programa;
- um arquivo `input.in`, que contém a entrada do programa;
- um arquivo `output.out`, onde será armazenada a saída produzida pelo programa.

Uma organização possível é:

```text
projeto/
├── programa.cpp
├── input.in
└── output.out
```

O nome do arquivo `.cpp` pode ser escolhido livremente. Já os arquivos `input.in` e `output.out` serão utilizados pelo sistema de compilação que configuraremos posteriormente.

## ⚙️ Configurando o layout

Uma configuração interessante para programação competitiva é dividir a janela do Sublime em três colunas.

Para isso, acesse:

```text
View → Layout → Columns: 3
```

Também é possível utilizar o atalho:

```text
Alt + Shift + 3
```

Depois, configure o número máximo de colunas dos grupos para duas:

```text
View → Groups → Max Columns: 2
```

A ideia é deixar o ambiente organizado de forma que possamos visualizar simultaneamente o código, a entrada e a saída do programa.

Uma organização possível é:

```text
┌──────────────────┬──────────────────┬──────────────────┐
│                  │                  │   input.in       │
│   programa.cpp   │      código      ├──────────────────┤
│                  │                  │   output.out     │
│                  │                  │                  │
└──────────────────┴──────────────────┴──────────────────┘
```

Essa organização é especialmente útil durante o desenvolvimento, pois podemos alterar a entrada e observar imediatamente a saída produzida pelo programa.

## 📄 Criando os arquivos

Na janela central, crie um novo arquivo e salve-o com a extensão `.cpp`.

Por exemplo:

```text
solucao.cpp
```

Na janela superior direita, crie um arquivo chamado:

```text
input.in
```

Na janela inferior direita, crie:

```text
output.out
```

Os três arquivos devem aparecer no navegador de arquivos do Sublime.

O arquivo `.cpp` será o código que iremos executar. O `input.in` representa os dados que seriam fornecidos ao programa, enquanto o `output.out` armazenará a resposta produzida.

## 🔨 Configurando a compilação

O Sublime permite criar diferentes configurações de compilação chamadas **Build Systems**.

Para criar uma configuração própria para programação competitiva, acesse:

```text
Tools → Build System → New Build System
```

Será aberto um arquivo de configuração. Cole nele o código de configuração encontrado [aqui](https://drive.google.com/file/d/1XVtLyQWLdVdwvXmpiNJQ5v3AGoNcA9aG/view?usp=drive_link).

```text
CP.sublime-build
```

Depois, selecione:

```text
Tools → Build System → CP
```

A partir desse momento, o Sublime poderá utilizar essa configuração para compilar e executar nossos programas.

## ▶️ Executando o programa

Depois de configurar o Build System, podemos executar nosso programa utilizando:

```text
Ctrl + Shift + B
```

Esse comando permite escolher qual variante de compilação queremos utilizar.

Na configuração do FACOMpetindo existem duas variantes principais:

### CP

A variante `CP` é indicada para testar os programas durante o desenvolvimento.

Ela utiliza diversas flags que ajudam a encontrar erros no código, facilitando o processo de **debug**.

Por utilizar essas verificações adicionais, essa configuração pode ser mais lenta.

### CP - Test

A variante `CP - Test` é utilizada para testar o desempenho do programa.

Sua compilação é equivalente à utilizada durante a prova da maratona, sendo útil para verificar se o programa possui um tempo de execução adequado.

Assim, podemos utilizar:

```text
CP
```

quando queremos encontrar possíveis problemas no código e:

```text
CP - Test
```

quando queremos realizar um teste mais próximo das condições reais de uma competição.

## ⚡ Executando novamente

Depois de escolher uma das variantes, não é necessário selecioná-la novamente a cada execução.

Para executar novamente utilizando a última variante escolhida, basta pressionar:

```text
Ctrl + B
```

Isso torna bastante rápido o ciclo de desenvolvimento:

```text
Alterar código
      ↓
Salvar
      ↓
Ctrl + B
      ↓
Executar
      ↓
Verificar a saída
```

Esse processo será repetido constantemente durante o treinamento e durante a resolução de problemas.

## 🧪 Testando um problema

Suponha que temos o seguinte programa:

```cpp
#include <iostream>

using namespace std;

int main() {
    int a, b;

    cin >> a >> b;

    cout << a + b << "\n";

    return 0;
}
```

Podemos colocar os valores de entrada no arquivo `input.in`:

```text
10 20
```

Ao executar o programa, o resultado será escrito em `output.out`:

```text
30
```

Isso permite testar diferentes casos sem precisar digitar a entrada manualmente toda vez.

Por exemplo, podemos alterar `input.in` para:

```text
100 250
```

e executar novamente o programa.

A saída será:

```text
350
```

Essa forma de testar é bastante conveniente para programação competitiva, pois podemos criar rapidamente diversos casos de teste e verificar se nosso programa produz as respostas esperadas.

## 🐛 Debug

Durante a resolução de problemas, nem sempre o código funciona corretamente na primeira tentativa.

Podemos utilizar o arquivo `input.in` para criar casos de teste específicos que nos ajudem a encontrar o erro.

Por exemplo, além dos casos apresentados no enunciado, podemos testar:

- valores mínimos;
- valores máximos;
- valores iguais;
- valores iguais a zero;
- casos em que uma condição muda de comportamento;
- casos pequenos que permitam verificar a resposta manualmente.

Testar casos diferentes dos exemplos fornecidos é uma habilidade muito importante em Programação Competitiva.
