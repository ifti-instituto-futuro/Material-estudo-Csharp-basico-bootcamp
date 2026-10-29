#### Questão 7 — Boletim da turma (Lista aninhada, for e foreach, Entrada e conversão, decimal, if/else)

**Situação.** A coordenação precisa fechar o boletim do bimestre. Cada aluno tem 2 notas inteiras, guardadas como texto em uma tabela: Lia (8 e 6), Noah (5 e 4) e Davi (7 e 4). A média é a soma das 2 notas dividida por 2. Média 7 ou mais é Aprovado, de 5 até menos de 7 é Recuperação, menos de 5 é Reprovado.

**O que o programa deve fazer.**

- Guardar os alunos em uma `List<List<string>>`, com os campos `[0] nome`, `[1] nota 1`, `[2] nota 2`.
- Converter as notas com `int.Parse` e calcular a média em `decimal`. Cuidado: divida por `2m`, não por `2`.
- Mostrar `nome | média | situação` para cada aluno, com a média em 1 casa decimal.

**Dois caminhos de solução.**

- **Caminho 1:** `foreach` nas linhas. Cada linha é um aluno, e o campo é lido com 1 índice: `aluno[1]`.
- **Caminho 2:** `for` com índice. O campo é lido com 2 índices: `alunos[i][1]`.

**Saída esperada.**

```text
Lia | média 7,0 | Aprovado
Noah | média 4,5 | Reprovado
Davi | média 5,5 | Recuperação
```
