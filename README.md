# Compiladores

Este repositório contém o código-fonte de um compilador desenvolvido em Haskell. O compilador processa uma linguagem imperativa simples, semelhante a C, e gera bytecode Jasmin, que pode então ser montado em arquivos `.class` Java para serem executados na Java Virtual Machine (JVM).

## Visão Geral do Projeto

O projeto implementa o pipeline clássico de compiladores, incluindo análise léxica, sintática e semântica, seguida pela geração de bytecode. Ele utiliza o conjunto de ferramentas padrão do Haskell, incluindo o gerador de analisador léxico **Alex** e o gerador de analisador sintático **Happy**.

A linguagem fonte suportada pelo compilador inclui:

* **Tipos de Dados**: `int`, `double`, `string`.
* **Controle de Fluxo**: instruções `if-else` e loops `while`.
* **Funções e Procedimentos**: Suporte para definições de funções, parâmetros e instruções `return`. Funções void (procedimentos) também são suportadas.
* **Expressões**: Operações aritméticas (`+`, `-`, `*`, `/`), relacionais (`==`, `/=`, `<`, `>`, `<=`, `>=`) e lógicas (`&&`, `||`, `!`).
* **Atribuições e E/S**: Atribuição de variáveis, impressão de valores com `print`.
* **Conversão de Tipos (Casting)**: Conversão explícita entre `int` e `double`.

## Pipeline do Compilador

O processo de compilação é dividido em várias fases distintas:

1. **Análise Léxica (`Lex.x`)**: O código-fonte é escaneado e dividido em uma sequência de tokens. Isso é tratado por um lexer gerado pelo Alex.
2. **Análise Sintática (`Parser.y`)**: O fluxo de tokens é analisado para construir uma Árvore de Sintaxe Abstrata (AST) que representa a estrutura do programa. Isso é tratado por um parser gerado pelo Happy.
3. **Análise Semântica (`Semantico.hs`)**: A AST é percorrida para realizar verificação de tipos, verificar declarações de variáveis e funções, lidar com coerções de tipos e relatar erros ou avisos semânticos.
4. **Geração de Código (`Gera_codigo.hs`)**: A AST validada e anotada é usada para gerar código assembly Jasmin de baixo nível (arquivo `.j`).

## Componentes Principais

* **`Main.hs`**: O driver principal do compilador. Ele lê o arquivo fonte (`teste.txt`), orquestra as fases de análise e geração de código, e grava o bytecode de saída em `Main.j`.
* **`Lex.x` / `Lex.hs**`: O arquivo fonte do Alex definindo as expressões regulares para tokens e o módulo lexer Haskell gerado.
* **`Parser.y` / `Parser.hs**`: O arquivo fonte do Happy definindo a gramática da linguagem e o módulo parser Haskell gerado.
* **`Token.hs`**: Define os tipos de dados para todos os tokens reconhecidos pelo lexer.
* **`Ri.hs`**: (Representação Intermediária) Define os tipos de dados Haskell para a Árvore de Sintaxe Abstrata (AST), incluindo expressões, comandos e estrutura do programa.
* **`Semantico.hs`**: Contém a lógica para análise semântica, incluindo verificação de tipos e gerenciamento de escopo.
* **`Gera_codigo.hs`**: Traduz a AST em instruções de bytecode Jasmin.
* **`teste.txt`**: Um arquivo fonte de exemplo demonstrando os recursos da linguagem compilada por este projeto.

## Uso

Para executar o compilador, você precisa do conjunto de ferramentas Haskell, incluindo GHC, Alex e Happy.

1. **Compilar e Executar**:
Execute o módulo principal usando `runghc`:
```sh
runghc Main.hs

```


2. **Entrada**:
O compilador está hardcoded para ler sua entrada do arquivo `teste.txt`.
3. **Saída**:
* Os resultados da análise léxica, sintática e semântica são impressos no console e também salvos em `resultados.txt`.
* O bytecode Jasmin gerado é salvo em um arquivo chamado `Main.j`.


4. **Montando e Executando o Bytecode**:
Você pode usar um assembler Jasmin para converter o arquivo `.j` em um arquivo `.class` Java.
```sh
java -jar jasmin.jar Main.j

```


Após a montagem, você pode executar o programa compilado usando o ambiente de execução Java:
```sh
java Main

```

! Esse README foi gerado por IA, mas os seus conteúdos foram conferidos e testados.
