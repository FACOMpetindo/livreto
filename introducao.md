# Introdução

## 📚 O que é Programação Competitiva?

A Programação Competitiva é um esporte da mente no qual os participantes resolvem problemas de programação utilizando raciocínio lógico, algoritmos e estruturas de dados.

Cada problema descreve uma situação e fornece uma entrada. O objetivo é desenvolver um programa que produza exatamente a saída esperada para qualquer caso de teste dentro do tempo limite estabelecido.

Além de ser uma atividade bastante divertida para quem gosta de resolver desafios, a Programação Competitiva também desenvolve habilidades importantes para qualquer profissional da computação, como:

- resolução de problemas;
- pensamento lógico;
- conhecimento de algoritmos;
- estruturas de dados;
- otimização de código;
- trabalho em equipe (em algumas competições).

Essas habilidades são valorizadas tanto no meio acadêmico quanto no mercado de trabalho.

---

## 🏆 Principais competições

Existem diversas competições de Programação Competitiva ao redor do mundo. No Brasil, destacam-se três delas.

### OBI

A **Olimpíada Brasileira de Informática (OBI)** é organizada pela UNICAMP e possui três fases.

Na modalidade universitária, apenas estudantes ingressantes (calouros) podem participar. Durante a competição, cada participante resolve individualmente quatro problemas em três horas.

Cada problema vale até 100 pontos e pode possuir subtarefas, permitindo que soluções parciais também recebam pontuação.

---

### Maratona Feminina de Programação

A **Maratona Feminina de Programação (MFP)** é organizada pela Sociedade Brasileira de Computação (SBC) e busca incentivar a participação feminina na área.

A competição possui uma fase online e uma fase presencial. Assim como na OBI, as competidoras resolvem os problemas individualmente durante três horas.

---

### Maratona SBC de Programação

A **Maratona SBC de Programação**, que faz parte do ICPC (_International Collegiate Programming Contest_), é a maior competição universitária de Programação Competitiva do país.

Nela, cada equipe é formada por **três estudantes e apenas um computador**. Durante cinco horas, as equipes tentam resolver aproximadamente uma dúzia de problemas.

Cada problema resolvido corretamente rende um balão colorido para a equipe, tornando o ambiente da competição bastante característico.

---

## ⚖️ Como funciona uma competição?

Em uma competição, não existe um professor corrigindo seu código manualmente.

Quando você envia sua solução, ela é executada automaticamente em diversos casos de teste preparados pelos autores do problema.

Cada caso de teste possui uma entrada diferente e uma saída esperada. O seu programa deve produzir exatamente a mesma saída para todos eles.

Além disso, cada problema possui um limite de tempo e, em alguns casos, também um limite de memória. Caso sua solução seja lenta demais ou produza uma resposta incorreta, ela será rejeitada.

Os sistemas responsáveis por executar e corrigir automaticamente as soluções são chamados de **juízes online** (_online judges_).

---

## 📖 Como ler um problema

Ler corretamente um problema é uma das habilidades mais importantes em Programação Competitiva.

Ao resolver um exercício, procure sempre:

- entender exatamente o que está sendo pedido;
- observar o formato da entrada;
- prestar atenção ao formato da saída;
- verificar os limites das variáveis;
- pensar em casos de teste diferentes dos exemplos fornecidos.

Grande parte dos erros cometidos por iniciantes acontece por descuido na leitura da descrição do problema.

---

## ⏱️ Tempo limite

Quase todos os problemas possuem um tempo limite para execução.

Em muitas plataformas esse limite é de aproximadamente **1 segundo**, embora possa variar de acordo com o problema.

Isso significa que seu programa precisa produzir a resposta antes que esse tempo seja excedido.

Nas próximas aulas aprenderemos sobre **complexidade de algoritmos**, que nos permitirá estimar se uma solução será rápida o suficiente para determinado problema.

---

## 💻 Por que utilizamos C++?

Diversas linguagens são aceitas nas principais competições, porém o **C++** tornou-se a linguagem mais utilizada pela comunidade.

Isso acontece porque ele oferece um excelente equilíbrio entre desempenho e produtividade.

Além disso, o C++ possui a **STL (Standard Template Library)**, uma biblioteca que disponibiliza diversas estruturas de dados e algoritmos prontos para uso, como:

- vetores (`vector`);
- filas (`queue`);
- pilhas (`stack`);
- mapas (`map`);
- conjuntos (`set`);
- algoritmos de ordenação (`sort`);
- busca binária (`lower_bound` e `upper_bound`);
- entre muitos outros.

Ao longo deste livreto utilizaremos C++ em todos os exemplos.

---

## 🔢 Tipos básicos

Nesta primeira aula utilizaremos apenas os tipos básicos da linguagem.

| Tipo     | Descrição                           |
| -------- | ----------------------------------- |
| `int`    | Números inteiros                    |
| `float`  | Números reais de precisão simples   |
| `double` | Números reais de dupla precisão     |
| `char`   | Um único caractere                  |
| `bool`   | Valores lógicos (`true` ou `false`) |

Nas próximas aulas conheceremos outros tipos e estruturas mais avançadas.

---

## ⌨️ Entrada e saída

A maioria dos problemas consiste em ler alguns valores da entrada, realizar um processamento e imprimir a resposta.

Em C++, utilizamos principalmente:

```cpp
cin >> variavel;
cout << resposta << "\n";
```

Por enquanto, esses dois comandos serão suficientes para resolver os primeiros exercícios do treinamento.

---

## ▶️ Como executar programas

Existem diversas maneiras de executar programas em C++.

Uma opção simples é utilizar compiladores online, como o **OnlineGDB**.

Caso prefira programar localmente, basta instalar um compilador C++ e executar:

```bash
g++ programa.cpp
./a.out
```

Também é possível utilizar editores como VS Code ou outras IDEs de sua preferência.

---

## 📈 Como treinar?

A melhor maneira de aprender Programação Competitiva é resolvendo muitos problemas.

Algumas plataformas bastante utilizadas são:

- **Beecrowd**: ideal para iniciantes e muito utilizado em universidades brasileiras.
- **Codeforces**: uma das maiores plataformas do mundo, com competições semanais e sistema de rating.
- **AtCoder**: plataforma japonesa conhecida por seus problemas educativos e contests bem organizados.
- **LeetCode**: muito utilizada para preparação para entrevistas técnicas e prática de algoritmos.

Além dessas plataformas, o projeto FACOMpetindo disponibiliza este livreto, listas de exercícios e outros materiais de apoio para acompanhar as aulas.

---

## 🚀 Próximos passos

Nas próximas aulas começaremos a estudar os principais conceitos da linguagem C++ e, gradualmente, aprenderemos algoritmos e estruturas de dados utilizados nas competições.

Não se preocupe caso algum assunto pareça difícil no início. Programação Competitiva é uma habilidade desenvolvida com prática constante, e cada problema resolvido representa um passo importante na construção do seu raciocínio algorítmico.
