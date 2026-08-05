# formata-insert

Formata SQL Insert

![formata INSERT](/formata-insert.png "formata INSERT")

## Funcionalidades

- Dois formatos de saída, à sua escolha: **SQL formatado** (continua
  sendo um `INSERT` válido, só que com uma coluna/valor por linha) ou
  **Coluna: valor** (uma listagem `coluna: valor`, útil para conferir
  rapidamente cada campo).
- Suporta múltiplas linhas em um mesmo `INSERT` (`VALUES (...), (...), ...`).
- Suporta múltiplos `INSERT`s colados de uma vez, separados por `;`.
- Entende vírgulas e parênteses dentro de valores (strings com vírgula,
  chamadas de função como `NOW()`, `CONCAT(a, b)`, aspas escapadas).
- Formata automaticamente enquanto você digita/cola, sem precisar clicar
  em nada.
- Botão de exemplo, para carregar um SQL grande de amostra e testar a
  ferramenta sem precisar colar nada.
- Botão para copiar o resultado formatado.

Ferramenta 100% client-side: um único arquivo HTML, sem build, sem
dependências.

Confira online:

https://boaglio.github.io/formata-insert/
