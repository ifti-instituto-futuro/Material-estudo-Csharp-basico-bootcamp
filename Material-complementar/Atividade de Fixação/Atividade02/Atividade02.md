#### Questão 2 — Academia Movimento (Tipagem, Entrada e conversão, if/else, switch, decimal)

**Situação.** A Academia Movimento tem 3 planos mensais: Plano Básico (código 1) por R$ 89,90, Plano Plus (código 2) por R$ 119,90 e Plano Total (código 3) por R$ 149,90. O aluno pode pagar vários meses de uma vez. A recepcionista digita o código do plano e a quantidade de meses. Ela precisa ver o nome do plano e o total a cobrar, para informar o aluno antes de passar o cartão.

**O que o programa deve fazer.**

- Ler o código do plano (texto) e a quantidade de meses (número inteiro).
- Descobrir o nome e o preço mensal do plano.
- Mostrar o total com 2 casas decimais. Um código que não existe mostra `Plano inválido.`
- Escolher o tipo certo para cada dado: `string` para o nome, `decimal` para o preço, `int` para os meses.

**Dois caminhos de solução.**

- **Caminho 1:** use `if / else if` para comparar o código e definir o nome e o preço.
- **Caminho 2:** use `switch` com um `case` para cada código.

**Testes.**

| Entrada | Saída esperada |
| --- | --- |
| Plano 2, 3 meses | `Plano Plus: 3 mês(es) = R$ 359,70` |
| Plano 9, 3 meses | `Plano inválido.` |
