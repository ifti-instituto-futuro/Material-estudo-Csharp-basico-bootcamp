#### Questão 5 — Frete da loja online (Entrada e conversão, Strings, switch, if/else, Operadores, decimal)

**Situação.** A loja online Casa & Cia calcula o frete pela região de entrega e pelo peso do pacote. O frete base é R$ 15,00 para o Nordeste (1), R$ 25,00 para o Sudeste (2), R$ 30,00 para o Sul (3) e R$ 35,00 para o Norte e o Centro-Oeste (4). O frete base cobre até 5 kg. Cada kg acima de 5 custa R$ 2,50 a mais. O atendente digita a região e o peso em kg, arredondado para um número inteiro, e às vezes erra a digitação.

**O que o programa deve fazer.**

- Ler a região. Se for inválida, mostrar `Região inválida.` e não pedir o peso.
- Ler o peso. Só aceitar um texto que não seja vazio e tenha apenas dígitos de 0 a 9. Senão, mostrar `Digite o peso só com números.`
- Converter o peso com `int.Parse` e calcular o frete. Mostrar o valor com 2 casas decimais.

**Dois caminhos de solução.**

- **Caminho 1:** `switch` para a região e `foreach` para conferir os caracteres do peso.
- **Caminho 2:** `if / else if` para a região e `for` com `texto[i]` para conferir os caracteres do peso.

**Testes.**

| Região, peso | Saída esperada |
| --- | --- |
| 2, 8 | `Frete: R$ 32,50` |
| 1, 3 | `Frete: R$ 15,00` |
| 2, abc | `Digite o peso só com números.` |
| 3, 7,5 | `Digite o peso só com números.` |
| 9 | `Região inválida.` |
