# formata-insert

Formata SQL Insert

![formata INSERT](/formata-insert.png "formata INSERT")

## Funcionalidades

- Formata `INSERT INTO tabela (col1, col2) VALUES (v1, v2)` como SQL
  válido, com uma coluna/valor por linha, fácil de ler e revisar.
- Suporta múltiplas linhas em um mesmo `INSERT` (`VALUES (...), (...), ...`).
- Suporta múltiplos `INSERT`s colados de uma vez, separados por `;`.
- Entende vírgulas e parênteses dentro de valores (strings com vírgula,
  chamadas de função como `NOW()`, `CONCAT(a, b)`, aspas escapadas).
- Formata automaticamente enquanto você digita/cola, sem precisar clicar
  em nada.
- Botão para copiar o resultado formatado.

Ferramenta 100% client-side: um único arquivo HTML, sem build, sem
dependências.

Confira online:

https://boaglio.github.io/formata-insert/
