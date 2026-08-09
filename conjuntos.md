# Conjuntos

## 📚 Introdução

Conjuntos são uma ferramenta muito útil em programação competitiva, a ideia básica de um conjunto é uma lista que não contém elementos repetidos, ou seja, se você tentar adicionar um elemento que já está no conjunto, ele não será adicionado.

Conjuntos em C++ são ordenados, ou seja, os elementos são armazenados em ordem crescente, entretando não é possível acessar o elemento de um conjunto pelo seu índice.

Também não é possível alterar o valor de um elemento de um conjunto, porém é possível adicionar e remover elementos de um conjunto.

## 🔨 Criando um conjunto

Para criar um conjunto em C++ basta adicionar a biblioteca `set` e criar uma variável do tipo set conforme o exemplo abaixo:

```cpp
#include <set>

using namespace std;

int main(){
    set<int> S; //Cria um conjunto para armazenar números inteiros
}
```

## 📥 Inserindo elementos

Para inserir um elemento em um conjunto, basta usar o método `insert`:

```cpp
#include <set>

using namespace std;

int main(){
    set<int> S; //Cria um conjunto para armazenar números inteiros

    S.insert(10); //Adiciona o elemento 10
    S.insert(3); //Adiciona o elemento 3
}
```

É importante notar que a complexidade de inserção em um conjunto é `O(log n)`, onde `n` é o tamanho do conjunto, ou seja, inserir um elemento em um conjunto é mais lento do que inserir diretamente na posição `n` de um vetor.

## 🔍 Buscando elementos

Para realizar uma busca no set utilizamos o comando `find`, ele retorna um ponteiro que aponta para o elemento procurado caso o elemento esteja no conjunto, ou para o final dele, caso o elemento procurado não exista, sua complexidade também é `O(log ⁡n)`.

```cpp
#include <set>

using namespace std;

int main(){
    set<int> S; //Cria um conjunto para armazenar números inteiros

    S.insert(10); //Adiciona o elemento 10
    S.insert(3); //Adiciona o elemento 3

    if(S.find(3) != S.end()){ //Se 3 está no conjunto
      cout<<3<<"\n";
    }
}
```

## 🗑️ Deletando elementos

Para deletar um elemento de um conjunto, basta usar o método `erase`:

```cpp
#include <set>

using namespace std;

int main(){
    set<int> S; //Cria um conjutno

    S.insert(10); //Adiciona o elemento 10
    S.insert(3); //Adiciona o elemento 3

    S.erase(10); //Apaga o elemento
}
```

Outros métodos que também devemos conhecer são os:

- `clear`: Apaga todos os elementos.
- `size`: Retorna a quantidade de elementos.
- `begin`: Retorna um ponteiro para o inicio do set
- `end`: Retorna um ponteiro para o final do set

Por fim, algumas vezes queremos passar por todos os elementos presentes no conjunto e podemos fazer isso utilizando o código abaixo.

```cpp
#include <set>
#include <iostream>

using namespace std;

int main(){
    set<int> S; //Cria um conjunto para armazenar números inteiros

    S.insert(7); //Adiciona o elemento 7
    S.insert(10); //Adiciona o elemento 10
    S.insert(3); //Adiciona o elemento 3

    for (auto i: S){
      cout << i << " ";
    }
    cout<<"\n";
}
```

É importante lembrar que quando passarmos pelos elementos, iremos acessar eles de forma ordenada. Logo, no exemplo acima o código imprime `3 7 10`.

## 🚀 Demonstração

Vamos analisar o exercício 2410 do Beecrowd que caiu na OBI 2012, o enunciado do exercício é o seguinte:

<figure><img src="../assets/2410.png" alt="Exercício 2410 do Beecrowd"><figcaption></figcaption></figure>

Primeiramente, esse exercício pode parecer muito simples de resolver! Simplesmente lemos as entradas, colocamos o número do aluno em uma lista se ele não estava lá, e no final verificamos o tamanho da lista, certo?

Não exatamente, o problema é que a lista é uma estrutura de dados muito lenta para esse problema, como o enunciado nos diz que podemos ter até 10ˆ5 alunos, temos que olhar na lista 10ˆ5 vezes (pois você pode ter certeza que um dos casos de teste terá o número máximo de alunos), e essa verificação tem complexidade O(n), ou seja, a solução terá complexidade O(nˆ2), o que é muito lento para esse problema.

Fora que como estamos em C++, ou temos que criar um vetor de tamanho 10ˆ5, ou temos que usar alocação dinâmica, o que é mais lento ainda.

Mas esquecemos um detalhe importante, o enunciado nos diz que os números dos alunos são únicos, ou seja, não temos números repetidos, e isso é um indicativo claro de que devemos usar um conjunto, já que como discutimos, ele não aceita números repetidos, podemos simplesmente adicionar cada aluno a um conjunto e usar a função `size()` para ver quantos alunos foram pra aula!

```cpp
#include <iostream>
#include <set>

using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(0);

    set<int> alunos;
    int n, x;
    cin >> n;
    for(int i = 0; i < n; i++){
        cin >> x;
        alunos.insert(x);
    }
    cout << alunos.size() << endl;
}
```

## 🧑‍🏫 Exercícios

- Exercício [1581](https://www.beecrowd.com.br/judge/pt/problems/view/1581) do Beecrowd, esse é um exercício que é resolvido facilmente com conjuntos.

- Exercício [2322](https://www.beecrowd.com.br/judge/pt/problems/view/2322) do Beecrowd, que caiu na OBI 2007, esse é um exercício simples que serve para treinar o uso de conjuntos.

- Exercício [2410](https://www.beecrowd.com.br/judge/pt/problems/view/2410) tente replicar a solução que foi discutida acima.

- Exercício [2469](https://www.beecrowd.com.br/judge/pt/problems/view/2469) do Beecrowd, que caiu na OBI 2014, esse exercício pode ser resolvido de várias maneiras, mas uma das mais simples é usando um conjunto e uma lista.
