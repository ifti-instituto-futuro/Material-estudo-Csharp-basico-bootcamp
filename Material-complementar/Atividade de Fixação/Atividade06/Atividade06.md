#### Questão 6 — Lista de convidados do casamento (while, switch, if/else, Strings, List, Busca)

**Situação.** A cerimonialista de um casamento monta a lista de convidados no notebook nas semanas anteriores à festa. No dia do evento, o mesmo programa é usado na portaria. Os nomes são digitados de formas diferentes (`Ana Lima`, `ana lima`, `ANA LIMA`), e ninguém pode entrar duas vezes na lista. Nomes com menos de 3 caracteres são erros de digitação.

**O que o programa deve fazer.**

- Menu com 1 (adicionar), 2 (conferir na portaria), 3 (listar) e 0 (sair), repetido até a opção 0.
- Adicionar: remover espaços extras, recusar nomes curtos e recusar nomes repetidos sem diferenciar maiúsculas de minúsculas.
- Conferir: mostrar `Entrada liberada.` ou `Nome não está na lista.`
- Listar: mostrar os nomes numerados a partir de 1 e o total, ou `Nenhum convidado na lista.`

**Dois caminhos de solução.**

- **Caminho 1:** menu com `switch`. A busca usa `foreach`, uma variável `bool` e `ToLower()`.
- **Caminho 2:** menu com `if / else if`. A busca usa `for`, a posição `-1`, `break` e `string.Equals`. As opções 1 e 2 dividem a mesma busca.

**Teste.** Digite em sequência: 3 → 1 `  Ana Lima ` → 1 `ana lima` → 1 `Bo` → 1 `Davi` → 2 `ANA LIMA` → 2 `Eva` → 3 → 7 → 0. A saída esperada, na ordem:

```text
Nenhum convidado na lista.
Ana Lima adicionado.
ana lima já está na lista.
O nome precisa ter pelo menos 3 caracteres.
Davi adicionado.
Entrada liberada.
Nome não está na lista.
1. Ana Lima
2. Davi
Total: 2
Opção inválida. Escolha uma opção de 0 a 3.
Encerrando.
```
