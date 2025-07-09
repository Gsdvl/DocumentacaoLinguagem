# 🔑 Palavras Reservadas da Linguagem G2DL

Palavras reservadas são identificadores especiais que **não podem ser usados como nomes de variáveis, funções ou objetos**, pois possuem um **significado fixo** na linguagem. Elas fazem parte da **gramática principal** e são reconhecidas diretamente pelo analisador léxico.

Abaixo está a lista completa das palavras reservadas da linguagem G2DL, junto com uma descrição do papel de cada uma.

---

## 🧠 Controle de Fluxo

| Palavra       | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `if`          | Inicia uma estrutura condicional. Executa um bloco caso a condição seja verdadeira. |
| `else`        | Define o bloco alternativo de um `if` quando a condição é falsa.       |
| `while`       | Cria um laço de repetição baseado em uma condição booleana.            |
| `for`         | Inicia um laço com controle explícito de variável e intervalo.         |
| `break`       | Interrompe a execução do laço mais próximo (`for` ou `while`).         |

---

## 🧮 Funções e Retornos

| Palavra       | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `function`    | Define uma função com nome, parâmetros e corpo executável.             |
| `return`      | Finaliza a função atual e retorna um valor opcional ao chamador.       |

---

## 🔢 Valores Literais

| Palavra       | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `true`        | Literal booleano verdadeiro.                                           |
| `false`       | Literal booleano falso.                                                |

---

## 🖨️ Entrada e Saída

| Palavra       | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `printf`      | Função nativa para exibir dados no terminal (semelhante à `printf` em C). |
| `input`       | Solicita entrada do usuário e retorna como string.                     |

---

## 🛡️ Observações

- Todas essas palavras são reconhecidas diretamente pelo **lexer** e não exigem nenhuma declaração prévia.
- Elas **não podem ser sobrescritas** (por exemplo, não é possível criar uma função chamada `if`).
- São **case-sensitive** (sensíveis a maiúsculas/minúsculas). Portanto, `If` ou `ELSE` **não são válidas**.

---

## 🧪 Exemplo de uso

```bash
function somar(a, b) {
    if (a > b) {
        printf("a é maior");
    } else {
        printf("b é maior ou igual");
    }
    return a + b;
}
