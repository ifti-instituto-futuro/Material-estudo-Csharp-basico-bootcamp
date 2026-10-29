#### Questão 3 — Cadastro de usuários da biblioteca digital (Strings, List, foreach, Operadores lógicos, if/else)

**Situação.** A biblioteca digital da escola cria um login para cada aluno. Três alunos já têm login: `lia.souza`, `noah.lima` e `davi.rocha`. O sistema só aceita um novo nome de usuário que siga 3 regras: ter de 4 a 12 caracteres, não ter espaços no meio e não repetir um usuário já cadastrado. A comparação não diferencia maiúsculas de minúsculas: `NOAH.LIMA` é o mesmo usuário que `noah.lima`. Os espaços digitados sem querer no início e no fim devem ser removidos antes das regras. Quando o nome não passa, o aluno precisa saber qual regra quebrou.

**O que o programa deve fazer.**

- Começar com uma `List<string>` com os 3 usuários já cadastrados.
- Ler o nome de usuário e remover os espaços do início e do fim.
- Testar as regras nesta ordem: tamanho, espaços, usuário repetido.
- Mostrar a mensagem da primeira regra que falhou.
- Se o nome passar nas 3 regras, acrescentá-lo na lista e mostrar o total de usuários.

**Dois caminhos de solução.**

- **Caminho 1:** `Contains(" ")` para achar espaços. Um `foreach` na lista, com uma variável `bool` e `ToLower()`, para achar o usuário repetido.
- **Caminho 2:** um `foreach` que passa por cada letra (`char`) do nome para achar espaços. Um `for` na lista, com a posição `-1`, `break` e `string.Equals` com `StringComparison.OrdinalIgnoreCase`, para achar o usuário repetido.

**Testes.**

| Entrada | Saída esperada |
| --- | --- |
| `  Ana.Lima ` | `Usuário Ana.Lima criado. Total de usuários: 4` |
| `ana` | `O usuário precisa ter de 4 a 12 caracteres.` |
| `ana lima` | `O usuário não pode ter espaços.` |
| `NOAH.LIMA` | `Este usuário já está cadastrado.` |
