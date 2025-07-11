#  Palavras Reservadas da Linguagem G2DL

Palavras reservadas são identificadores especiais que **não podem ser usados como nomes de variáveis, funções ou objetos**, pois possuem um **significado fixo** na linguagem. Elas fazem parte da **gramática principal** e são reconhecidas diretamente pelo analisador léxico.

Abaixo está a lista completa das palavras reservadas da linguagem G2DL, junto com uma descrição do papel de cada uma.

---

## Controle de Fluxo

| Palavra       | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `if`          | Inicia uma estrutura condicional. Executa um bloco se a condição for verdadeira. |
| `else`        | Bloco alternativo executado se a condição do `if` for falsa.           |
| `while`       | Laço que executa um bloco enquanto a condição for verdadeira.          |
| `for`         | Estrutura de repetição com inicialização, condição e incremento definidos. |
| `break`       | Interrompe imediatamente a execução do laço atual (`for` ou `while`).  |

---

## Funções e Retornos

| Palavra       | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `function`    | Define uma função com nome, parâmetros e corpo.                        |
| `return`      | Encerra a função e opcionalmente retorna um valor.                    |

---
Em G2DL, funções seguem um modelo de execução baseado em pilha, semelhante ao da linguagem C. Cada vez que uma função é chamada, um novo frame é empilhado na stack de execução contendo os argumentos passados, variáveis locais e o endereço de retorno. Esse frame é descartado assim que a função termina, seja por meio de um return ou ao chegar ao final do bloco. Por isso, todas as variáveis declaradas dentro de uma função possuem tempo de vida limitado à duração da chamada, sendo recriadas em chamadas futuras. 
O valor de retorno é passado por valor, e a linguagem permite chamadas recursivas, já que cada instância da função mantém seu próprio ambiente isolado na pilha. Caso não haja uma condição de parada adequada, a recursão pode levar ao estouro da pilha. 
A única diferença prática em relação a C é a presença obrigatória da palavra-chave function para declarar funções.

## Valores Literais

| Palavra       | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `true`        | Valor booleano verdadeiro.                                             |
| `false`       | Valor booleano falso.                                                  |

---

## Entrada e Saída

| Palavra       | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `printf`      | Função nativa para exibir dados no terminal (semelhante à `printf` em C). |
| `input`       | Lê uma entrada do usuário e retorna uma string.                        |

---

## Tipos de Dados

| Palavra       | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `int`         | Declaração de variável do tipo inteiro.                                |
| `float`       | Declaração de variável do tipo ponto flutuante.                        |
| `string`      | Declaração de variável textual (cadeia de caracteres).                 |

---

## Operadores Aritméticos e de Atribuição (por ordem de precedência)

| Operador       | Função                                               | Tipo                   | Precedência |
|----------------|------------------------------------------------------|------------------------|-------------|
| `**`           | Exponenciação                                        | Aritmético             | Alta        |
| `*`            | Multiplicação                                        | Aritmético             | Alta        |
| `/`            | Divisão                                              | Aritmético             | Alta        |
| `%`            | Módulo (resto da divisão inteira)                    | Aritmético             | Alta        |
| `+`            | Soma                                                 | Aritmético             | Média       |
| `-`            | Subtração                                            | Aritmético             | Média       |
| `=`            | Atribuição                                           | Atribuição             | Baixa       |
| `+=`           | Atribuição com soma                                  | Atribuição composta    | Baixa       |
| `-=`           | Atribuição com subtração                             | Atribuição composta    | Baixa       |
| `*=`           | Atribuição com multiplicação                         | Atribuição composta    | Baixa       |
| `/=`           | Atribuição com divisão                               | Atribuição composta    | Baixa       |
| `%=`           | Atribuição com módulo                                | Atribuição composta    | Baixa       |
| `**=`          | Atribuição com exponenciação                         | Atribuição composta    | Baixa       |

---


## Operadores Relacionais e Lógicos

| Operador       | Função                                               |
|----------------|------------------------------------------------------|
| `==`           | Igualdade                                            |
| `!=`           | Diferença                                            |
| `<`            | Menor que                                            |
| `>`            | Maior que                                            |
| `<=`           | Menor ou igual                                       |
| `>=`           | Maior ou igual                                       |
| `&&`           | E lógico (AND)                                       |
| `||`           | Ou lógico (OR)                                       |
| `!`            | Negação lógica (NOT)                                 |

---

## Símbolos e Delimitadores

| Símbolo        | Função                                               |
|----------------|------------------------------------------------------|
| `(` `)`        | Delimitam argumentos de funções ou precedência       |
| `{` `}`        | Delimitam blocos de código                           |
| `[` `]`        | Delimitam listas, vetores ou índices                 |
| `,`            | Separador de argumentos ou elementos                 |
| `:`            | Pode ser usado em declarações ou blocos              |
| `;`            | Finaliza comandos                                    |

---

## Literais e Identificadores

| Tipo             | Exemplo               | Token retornado          |
|------------------|-----------------------|---------------------------|
| Inteiros         | `42`                  | `INTEGER`                 |
| Ponto flutuante  | `3.14`                | `FLOAT_LITERAL`           |
| String (aspas)   | `"texto"`             | `STRING_LITERAL`          |
| String (aspas simples) | `'texto'`       | `STRING_LITERAL`          |
| Identificador    | `minhaVariavel`       | `ID`                      |



##  Observações

- Todas essas palavras são reconhecidas diretamente pelo **lexer** e não exigem nenhuma declaração prévia.
- Elas **não podem ser sobrescritas** (por exemplo, não é possível criar uma função chamada `if`).
- São **case-sensitive** (sensíveis a maiúsculas/minúsculas). Portanto, `If` ou `ELSE` **não são válidas**.

---

##  Exemplo de uso

```c
function somar(a, b) {
    if (a > b) {
        printf("a é maior");
    } else {
        printf("b é maior ou igual");
    }
    return a + b;
}
```

## Diagrama de fluxo do Lexer

```
Entrada de código-fonte
        |
        v
+------------------------+
|  Ignorar espaços, \n  |
|  tabs e comentários   |
+------------------------+
        |
        v
+--------------------------+
| É palavra reservada?     |
| (if, else, for, etc.)    |
+--------------------------+
        | Sim
        v
Retorna TOKEN correspondente (ex: IF)
        |
        No
        v
+---------------------------+
| É operador/símbolo fixo?  |
| (+, ==, {, }, etc.)       |
+---------------------------+
        | Sim
        v
Retorna TOKEN correspondente (ex: PLUS, ASSIGNMENT)
        |
        No
        v
+-----------------------------+
| É literal numérico?         |
| (ex: 42, 3.14)              |
+-----------------------------+
        | Sim
        v
Converte e retorna INTEGER ou FLOAT_LITERAL
        |
        No
        v
+-----------------------------+
| É literal string?           |
| (ex: "texto", 'txt')        |
+-----------------------------+
        | Sim
        v
Extrai valor e retorna STRING_LITERAL
        |
        No
        v
+-------------------------------+
| É identificador (ID)?         |
| ([a-zA-Z_][a-zA-Z0-9_]*)      |
+-------------------------------+
        | Sim
        v
Retorna ID com string associada
        |
        No
        v
+-----------------------------+
| É comentário?               |
| (// ou /* */)               |
+-----------------------------+
        | Sim
        v
Ignora e continua
        |
        No
        v
+-----------------------------+
| Token inválido?             |
+-----------------------------+
        | Sim
        v
Imprime erro com `yytext`
```
## Tabela Completa de Tokens do Lexer

| Token                        | Representação Literal (Lexema)   | Categoria                    |
|-----------------------------|----------------------------------|------------------------------|
| `IF`                        | `if`                             | Palavra reservada            |
| `ELSE`                      | `else`                           | Palavra reservada            |
| `WHILE`                     | `while`                          | Palavra reservada            |
| `FOR`                       | `for`                            | Palavra reservada            |
| `FUNCTION`                  | `function`                       | Palavra reservada            |
| `RETURN`                    | `return`                         | Palavra reservada            |
| `BREAK`                     | `break`                          | Palavra reservada            |
| `TRUE`                      | `true`                           | Literal booleano             |
| `FALSE`                     | `false`                          | Literal booleano             |
| `PRINTF`                    | `printf`                         | Função embutida (I/O)        |
| `INPUT`                     | `input`                          | Função embutida (I/O)        |
| `PLUS_ASSIGNMENT`           | `+=`                             | Operador de atribuição       |
| `MINUS_ASSIGNMENT`          | `-=`                             | Operador de atribuição       |
| `MULTIPLY_ASSIGNMENT`       | `*=`                             | Operador de atribuição       |
| `DIVIDE_ASSIGNMENT`         | `/=`                             | Operador de atribuição       |
| `MOD_ASSIGNMENT`            | `%=`                             | Operador de atribuição       |
| `POWER_ASSIGNMENT`          | `**=`                            | Operador de atribuição       |
| `EQUAL`                     | `==`                             | Operador relacional          |
| `NOT_EQUAL`                 | `!=`                             | Operador relacional          |
| `LESS_THAN_OR_EQUAL`        | `<=`                             | Operador relacional          |
| `GREATER_THAN_OR_EQUAL`     | `>=`                             | Operador relacional          |
| `ASSIGNMENT`                | `=`                              | Operador de atribuição       |
| `LESS_THAN`                 | `<`                              | Operador relacional          |
| `GREATER_THAN`              | `>`                              | Operador relacional          |
| `PLUS`                      | `+`                              | Operador aritmético          |
| `MINUS`                     | `-`                              | Operador aritmético          |
| `MULTIPLY`                  | `*`                              | Operador aritmético          |
| `DIVIDE`                    | `/`                              | Operador aritmético          |
| `MOD`                       | `%`                              | Operador aritmético          |
| `POWER`                     | `**`                             | Operador aritmético          |
| `AND`                       | `&&`                             | Operador lógico              |
| `OR`                        | `||`                             | Operador lógico              |
| `NOT`                       | `!`                              | Operador lógico              |
| `LEFT_SQUARE_BRACKET`       | `[`                              | Símbolo                      |
| `RIGHT_SQUARE_BRACKET`      | `]`                              | Símbolo                      |
| `LEFT_PARENTHESIS`          | `(`                              | Símbolo                      |
| `RIGHT_PARENTHESIS`         | `)`                              | Símbolo                      |
| `LEFT_CURLY_BRACKET`        | `{`                              | Símbolo                      |
| `RIGHT_CURLY_BRACKET`       | `}`                              | Símbolo                      |
| `COMMA`                     | `,`                              | Símbolo                      |
| `COLON`                     | `:`                              | Símbolo                      |
| `';'` (char literal)        | `;`                              | Símbolo                      |
| `INT`                       | `int`                            | Tipo de dado                 |
| `FLOAT`                     | `float`                          | Tipo de dado                 |
| `STRING`                    | `string`                         | Tipo de dado                 |
| `INTEGER`                   | Ex: `42`                         | Literal numérico             |
| `FLOAT_LITERAL`             | Ex: `3.14`                       | Literal numérico             |
| `STRING_LITERAL`            | Ex: `"texto"` ou `'texto'`      | Literal textual              |
| `ID`                        | Ex: `variavel1`, `x`, `soma`    | Identificador                |
