Documentação da AST
# Estrutura da AST (`ast.c`)
Este módulo implementa as funções de construção e gerenciamento da Árvore de Sintaxe Abstrata (AST) da linguagem. 
Ele é responsável por representar a estrutura lógica do código-fonte após a análise sintática, permitindo que fases posteriores como análise semântica e interpretação/execução sejam realizadas.
## Estrutura Geral
- **Arquivo:** `ast.c`
- **Cabealhos:** `#include "ast.h"`
- **Uso de memória:** Todas as alocações so feitas via `malloc`, `realloc`, `strdup`, e
liberadas com `free`.
- **Origem da linha:** Cada n da AST marcado com a varivel global `yylineno` (linha
atual do lexer/parser).
## Criação de Nós da AST
Todos os nós são derivados de `AstNode` e criados com uma função base:
static AstNode* create_base_node(AstNodeType type, size_t size);
Ela aloca memoria, atribui o tipo do nó e o número da linha.

### Tipos de Nós Literais

| Função                               | Tipo de Nó                  | Descrição                               |
| ------------------------------------ | --------------------------- | --------------------------------------- |
| `create_int_literal_node(int)`       | `NODE_TYPE_INT_LITERAL`     | Representa um número inteiro.           |
| `create_float_literal_node(float)`   | `NODE_TYPE_FLOAT_LITERAL`   | Representa um número de ponto flutuante.|
| `create_string_literal_node(char*)`  | `NODE_TYPE_STRING_LITERAL`  | Representa uma string.                  |
| `create_identifier_node(char*)`      | `NODE_TYPE_IDENTIFIER`      | Representa um identificador (nome).     |

### Expressões

| Função                                     | Tipo de Nó                       | Descrição                                 |
| ------------------------------------------ | -------------------------------- | ----------------------------------------- |
| `create_assignment_node(target, op, expr)` | `NODE_TYPE_ASSIGNMENT`           | Atribuição com operador (ex: `+=`).       |
| `create_binary_op_node(left, op, right)`   | `NODE_TYPE_BINARY_OP`            | Operação binária (`+`, `-`, etc).         |
| `create_unary_op_node(op, operand)`        | `NODE_TYPE_UNARY_OP`             | Operação unária (`!`, `-`, etc).          |
| `create_expression_statement_node(expr)`   | `NODE_TYPE_EXPRESSION_STATEMENT` | Expressão isolada como instrução.         |

### Blocos e Controle de Fluxo

| Função                                      | Tipo de Nó                    | Descrição                               |
| ------------------------------------------- | ----------------------------- | --------------------------------------- |
| `create_block_node(statements)`             | `NODE_TYPE_BLOCK`             | Bloco de múltiplas instruções.           |
| `create_if_statement_node(cond, then, else)`| `NODE_TYPE_IF_STATEMENT`      | Condicional `if`/`else`.                |
| `create_while_node(cond, body)`             | `NODE_TYPE_WHILE_LOOP`        | Laço `while`.                           |
| `create_for_node(init, cond, incr, body)`   | `NODE_TYPE_FOR_LOOP`          | Laço `for`.                             |
| `create_break_statement_node()`             | `NODE_TYPE_BREAK_STATEMENT`   | Interrupção de laço.                    |
| `create_return_statement_node(expr)`        | `NODE_TYPE_RETURN_STATEMENT`  | Retorno de função.                      |

### Entrada e Saída

| Função                              | Tipo de Nó                   | Descrição                                     |
| ----------------------------------- | ---------------------------- | --------------------------------------------- |
| `create_printf_node(fmt_str, args)` | `NODE_TYPE_PRINTF_STATEMENT` | Comando `printf` com múltiplos argumentos.    |
| `create_printf_id_node(id)`         | `NODE_TYPE_PRINTF_ID`        | Impressão direta de uma variável.             |
| `create_input_node()`               | `NODE_TYPE_INPUT`            | Comando de entrada `input`.                   |

### Arrays

| Função                                         | Tipo de Nó                | Descrição                                     |
| ---------------------------------------------- | ------------------------- | --------------------------------------------- |
| `create_array_literal_node(elements)`          | `NODE_TYPE_ARRAY_LITERAL` | Criação de vetor com valores literais.        |
| `create_array_access_node(array, index_expr)`  | `NODE_TYPE_ARRAY_ACCESS`  | Acesso a elemento do vetor.                   |
| `create_array_assignment_node(array_access, expr)` | `NODE_TYPE_ASSIGNMENT`    | Atribuição de valor a um índice do vetor.     |

### Funções

| Função                                       | Tipo de Nó                  | Descrição                      |
| -------------------------------------------- | --------------------------- | ------------------------------ |
| `create_function_declaration_node(name, body)`| `NODE_TYPE_FUNCTION_DECL`   | Declaração de uma função.      |
| `create_function_call_node(name, args)`      | `NODE_TYPE_FUNCTION_CALL`   | Chamada de função.             |

## Estruturas de Suporte
### `AstNodeList`
Representa uma lista dinmica de nós da AST (como blocos de instrues ou arrays).
- `create_ast_node_list_from_node(node)`
- `append_to_ast_node_list(list, node)`
### `ArgumentNode`
Representa uma lista encadeada de argumentos de função ou `printf`.
- `create_argument_node(node)`
- `free_argument_list(list)`
## Liberação de Memória
A função `free_ast(node)` percorre toda a árvore de forma recursiva e libera a memória
alocada por:
- Strings duplicadas (`strdup`)
- Subnós e listas
- Argumentos
Ela identifica o tipo de nó via `node->type` e aplica a liberação correta para cada caso.
Também imprime um erro padrão caso o tipo seja desconhecido.
- A AST é projetada para **preservar informao de linha**, útil para erros e debug.
