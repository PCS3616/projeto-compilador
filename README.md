# Compilador de C--

## Introdução

Este projeto é uma introdução a Compiladores. Para entender corretamente
o que deve ser feito deve-se entendera a dinâmica de um compilador real,
tudo isso será aprofundado na disciplina "Linguagens e Compiladores" em
algum momento no futuro.

## Base de Compiladores

Um compilador é qualquer código que seja capaz de traduzir uma
linguagem-fonte em uma linguagem-objeto. Quando tanto a linguagem-fonte
quanto a linguagem-objeto são de baixo nível, o compilador recebe o nome
especial de montador (como o que você utilizou na última parte dos
laboratórios) e quando ambas são de alto nível recebe o nome especial de
tradutor. A utilidade básica de um compilador (esperamos que vocês já
saibam disso) é transformar um código de entrada (ASM por exemplo) em um
código que possa ser interpretado pela máquina (MVN por exemplo), porém
existem outras motivações para se escrever um montador, como para se
aplicar a técnica chamada "bootstrap", que serve para obter
compiladores sem passar pela dificuldade de codificar em linguagens de
baixo nível.

A estrutura macroscópica de um compilador, no geral, tem 3 componentes
principais:

1.  **Analisador léxico:** este componente é responsável por verificar se
    todas as palavras escritas no código recebido são coerentes e não
    infringem as regras da linguagem-fonte. Também é função do
    analisador léxico transformar o arquivo na linguagem-fonte em uma
    lista de tokens, identificando a qual classe (variável, palavra
    reservada, operador, etc.) cada palavra lida pertence.

2.  **Analisador sintático:** este componente é responsável por verificar se
    as sequências de palavras no código recebido são coerentes e não
    infringem as regras da linguagem-fonte. Este analisador tem como
    entrada os tokens classificados vindos do analisador anterior.

3.  **Analisador semântico:** este componente é responsável por traduzir as
    funções da linguagem-fonte (representada pelos tokens classificados)
    para a linguagem-objeto e escrever o arquivo de saída com o código
    final.

Essas etapas, especialmente os analisadores sintático e semântico, podem
ser representados por máquinas de estado finito, que realizam as funções
de cada analisador nas suas transições.

Um compilador também pode gerar mensagens de erro e aviso e escrever um
arquivo de log para registrar informações importantes da compilação
(como os erros e avisos). Para entender melhor todos estes processos
vale ler os capítulos 1 e 5 do livro do Professor João José Neto "Introdução
à Compilação".

## A linguagem C--

Esta linguagem que vamos utilizar aqui é uma simplificação da linguagem C
(assumimos que vocês tem familiaridade com ela) com apenas algumas
funcionalidades simples. O C-- suporta um tipo de variável, `int` (2
bytes). Ele permite atribuir valores, resultados de expressões ou outras
variáveis à variáveis. Atribuição de valores é feita com o símbolo `=`.
Cada instrução do código deve terminar com `;`. Não é possível inserir
comentários.

As palavras reservadas do C-- são:

| Palavras | Significado |
|----------|-------------|
| `int`    | tipo inteiro de 2 bytes        |
| `if`     | execução condicional           |
| `scan`   | comando de leitura do teclado  |
| `print`  | comando de escrita na tela     |

Os operadores aceitos no C-- são:

| Operador | Significado |
|----------|-------------|
| `+`      | operação de soma             |
| `-`      | operação de subtração        |
| `*`      | operação de multiplicação    |
| `/`      | operação de divisão inteira  |
| `<`      | comparador menor             |
| `>`      | comparador maior             |
| `==`     | comparador igual             |

Para simplificar o trabalho, deixamos aqui um resumo dos métodos que
serão necessárias para implementação.

### Analisador Léxico

Para o analisador léxico deve-se ler letra a letra o arquivo de entrada,
identificando se a a cadeia de símbolos não fere as necessidades da
linguagem[^1] e, ao término de uma palavra, identificar se ela se trata
de uma palavra reservada ou uma variável. Atente ao fato que a aparição
de um operador, mesmo sem espaço, deve terminar a palavra sendo lida.

[^1]: Isso só acontece se a palavra começar com um dígito e
    aparecer uma letra. "13" é um número, mas "13a" não é nada.

### Analisador Sintático

Para o analisador sintático pode ser utilizada a seguinte máquina (C
representa "Comando", V "variável", E "expressão e N "número", os
outros símbolos representam a si mesmos):

Máquina para um programa completo:

::: center
:::

Máquina para um comando:

::: center
:::

Máquina para uma expressão:

::: center
:::

## O trabalho

O trabalho consiste em implementar um compilador de C--, isto é, criar
um código que leia um arquivo em C-- e o traduza para ASM, seguindo as
regras de codificação de C-- colocadas acima. Evidentemente, o processo
inteiro é muito complexo para ser feito como um único projeto, assim é
necessário **escolher uma entre 3 sub-propostas** para realizar.

### Analisador Léxico: Proposta 2a

A proposta 2a consiste na implementação do analisador léxico, que deve
receber o arquivo com o código em linguagem-objeto e gerar um arquivo
com os tokens classificados.

### Analisador Sintático: Proposta 2a

A proposta 2b consiste na implementação do analisador sintático, que
deve receber o arquivo de tokens classificados e identificar se existe
alguma inconsistência de acordo com a máquina de estados apresentada e,
opcionalmente, gerar outras informações sobre as variáveis para auxiliar
o analisador semântico.

### Analisador Semântico: Proposta 2c

A proposta 2c consiste na implementação do analisador semântico, que
deve receber o arquivo de tokens classificados e outras informações
vindas do analisador sintático e gerar o código na linguagem-alvo,
traduzindo as estruturas das linguagens.

### Desafio
Uma função muito utilizada em linguagens de alto nível é a
definição de variáveis do tipo caractere. O trabalho do desafio é
extender o analisador implementado para suportar a definição de
variáveis desse tipo, que tem tamanho de 1 byte. Se forem aplicadas
operações sobre variáveis tipo char, as contas devem ser feitas com o
valor ASCII da letra.

O trabalho pode ser feito em duplas ou individualmente. Definir escopo
de uso do comunicador, mensagens de erro coerentes, eventuais limitações
e funcionalidades não comentadas acima FAZEM parte do trabalho.

## Perguntas

Seguem algumas perguntas a serem respondidas depois da codificação:

1.  Os algoritmos propostos podem ser mais eficientes? Como? Se sim, por
    que a forma menos eficiente foi escolhida?

2.  Os códigos escritos podem ser mais eficientes? Como? Se sim, por que
    a forma menos eficiente foi escolhida?

3.  Qual foi a maior dificuldade em implementar o compilador?

4.  O que teria que ser mudado no seu código para poder suportar
    definição de funções? E para suportar o uso de arrays (tanto de int
    como de char)?

## Entrega

Dois ou mais arquivos devem ser entregues:

1.  **Compilador:** um arquivo em ASM chamado
    `analisador_<nome do seu analisador>.asm` contendo o código do compilador
    de C--;

2. **Relatório:** um arquivo chamado `relatorio_<NUSP1>_<NUSP2>.pdf` para
    trabalhos realizados em dupla, ou `relatorio_<NUSP>.pdf` para individuais
    contendo uma descrição resumida do problema e dos conceitos e uma descrição
    detalhada das etapas de resolução, da estratégia utilizada em cada módulo
    e outras informações que julgarem úteis. O relatório pode conter imagens
    das execuções de teste;

3.  Outros arquivos que julgar necessário.

