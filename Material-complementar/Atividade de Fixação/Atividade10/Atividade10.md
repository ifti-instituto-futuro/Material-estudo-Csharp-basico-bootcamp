#### Programa B — Fila de impressão (while, switch, Strings, List, Operadores lógicos)

**Situação.** A impressora do escritório imprime os documentos na ordem em que foram enviados. Antes de imprimir, o funcionário informa o número de cópias, de 1 a 5.

- Menu com 1 (enviar documento), 2 (ver fila), 3 (imprimir próximo) e 0 (sair).
- Ver fila mostra a posição a partir de 1, ou `A fila está vazia.`
- Com número de cópias inválido, o documento continua no início da fila.
- **Caminho 1:** validar as cópias com um `switch` com `case "1"` a `case "5"` seguidos. **Caminho 2:** validar as cópias com `if`, conferindo que o texto tem 1 caractere (`copias.Length == 1`) e que ele está entre `'1'` e `'5'`.
- **Teste:** envie `relatorio.pdf` e `foto.png`. Imprima com `abc`: `relatorio.pdf` continua em 1º lugar. Imprima com `2`: `foto.png` passa para o 1º lugar. Imprima com `6`: `foto.png` continua na fila.
