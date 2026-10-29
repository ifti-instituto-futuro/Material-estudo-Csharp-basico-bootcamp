#### Questão 8 — Caixa da cantina (while, switch, if/else, Operadores, decimal e porcentagem)

**Situação.** A cantina da escola instalou um caixa de autoatendimento. O aluno digita o código de cada produto: 1 Salgado (R$ 6,50), 2 Suco (R$ 5,00) e 3 Bolo (R$ 4,50). Quando termina, ele digita 0. Um código que não existe é ignorado com um aviso, e o caixa continua funcionando. No fim, a cantina dá um desconto progressivo: 10% para compras de R$ 30,00 ou mais, 5% para compras de R$ 20,00 ou mais, e nenhum desconto abaixo disso.

**O que o programa deve fazer.**

- Repetir a leitura de códigos até o aluno digitar `0`.
- Somar o preço de cada produto válido e contar quantos itens entraram.
- Para um código inválido, mostrar `Código inválido. Item ignorado.`
- Mostrar a quantidade de itens, o subtotal, o percentual e o valor do desconto, e o total.

**Dois caminhos de solução.**

- **Caminho 1:** `while (codigo != "0")` e `switch` para somar o produto. O percentual fica guardado como número inteiro (`10m`), e o cálculo é `subtotal * percentual / 100`.
- **Caminho 2:** `while` controlado por uma variável `bool` e `if / else if` para somar o produto. A taxa fica guardada como fração (`0.10m`), e o cálculo é `subtotal * taxa`.

**Testes.**

| Códigos digitados | Saída esperada |
| --- | --- |
| 1, 1, 2, x, 3, 1, 0 | 1 aviso de código inválido. `Itens: 5`, `Subtotal: R$ 29,00`, `Desconto (5%): R$ 1,45`, `Total: R$ 27,55` |
| 1, 1, 1, 1, 1, 0 | `Itens: 5`, `Subtotal: R$ 32,50`, `Desconto (10%): R$ 3,25`, `Total: R$ 29,25` |
| 1, 2, 0 | `Itens: 2`, `Subtotal: R$ 11,50`, `Desconto (0%): R$ 0,00`, `Total: R$ 11,50` |
