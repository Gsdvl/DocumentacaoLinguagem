Documentação da AST
# Estrutura da AST (`ast.c`)
Este mdulo implementa as funes de construo e gerenciamento da **rvore de Sintaxe
Abstrata (AST)** da linguagem. Ele responsvel por representar a estrutura lgica do
cdigo-fonte aps a anlise sinttica, permitindo que fases posteriores como anlise semntica
e interpretao/executao sejam realizadas.
## Estrutura Geral
- **Arquivo:** `ast.c`
- **Cabealhos:** `#include "ast.h"`
- **Uso de memria:** Todas as alocaes so feitas via `malloc`, `realloc`, `strdup`, e
liberadas com `free`.
- **Origem da linha:** Cada n da AST marcado com a varivel global `yylineno` (linha
atual do lexer/parser).
## Criao de Ns da AST
Todos os ns so derivados de `AstNode` e criados com uma funo base:
static AstNode* create_base_node(AstNodeType type, size_t size);
Ela aloca memoria, atribui o tipo do n e o nmero da linha.

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
Representa uma lista dinmica de ns da AST (como blocos de instrues ou arrays).
- `create_ast_node_list_from_node(node)`
- `append_to_ast_node_list(list, node)`
### `ArgumentNode`
Representa uma lista encadeada de argumentos de funo ou `printf`.
- `create_argument_node(node)`
- `free_argument_list(list)`
## Liberao de Memria
A funo `free_ast(node)` percorre toda a rvore de forma recursiva e libera a memria
alocada por:
- Strings duplicadas (`strdup`)
- Subns e listas
- Argumentos
Ela identifica o tipo de n via `node->type` e aplica a liberao correta para cada caso.
Tambm imprime um erro padro caso o tipo seja desconhecido.
## Observaes Importantes
- A arquitetura separa bem a construo da AST do parsing.
- A AST projetada para **preservar informao de linha**, til para erros e debug.
- possvel expandir facilmente com novos tipos de ns seguindo o mesmo padro.
## Exemplos futuros
Em arquivos futuros, como o parser (`parser.y`) ou interpretador, voc pode usar chamadas
como:
AstNode* n = create_binary_op_node(a, OP_PLUS, b);
AstNode* stmt = create_if_statement_node(cond, bloco1, bloco2);
Esses ns so ento ligados rvore de forma recursiva e estruturada.
