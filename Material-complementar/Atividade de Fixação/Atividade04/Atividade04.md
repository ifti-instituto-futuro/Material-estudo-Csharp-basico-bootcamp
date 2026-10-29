#### Questão 4 — Pães da padaria (while, Entrada e conversão, Strings, List, for e foreach, decimal)

**Situação.** Toda sexta à noite, o gerente da Padaria Pão Quente digita quantos pães franceses vendeu em cada dia útil da semana. Às vezes ele erra: aperta uma letra, deixa o campo vazio ou digita um sinal de menos. O programa não pode fechar nem pular o dia quando isso acontece. Ele avisa e pede o mesmo dia de novo. No fim, o gerente quer o total da semana, a média por dia e o dia com mais vendas.

**O que o programa deve fazer.**

- Guardar os dias (`Segunda` a `Sexta`) em uma `List<string>` e as quantidades em uma `List<int>`.
- Pedir a quantidade de cada dia com `while`. Só aceitar um texto que não seja vazio e tenha apenas dígitos de 0 a 9. Só então converter com `int.Parse`.
- Com valor inválido, mostrar `Digite só números. Tente de novo.` e pedir o mesmo dia.
- Mostrar o total, a média com 2 casas decimais e o dia com mais vendas.

**Dois caminhos de solução.**

- **Caminho 1:** conferir os caracteres com `foreach`. Fazer o resumo com `for`, guardando a posição do dia com mais vendas.
- **Caminho 2:** conferir os caracteres com `for` e `texto[i]`. Fazer o resumo com `foreach` e um contador de posição.

Dicas para os 2 caminhos:

- Use `int dia = 0` como posição do dia atual. O `while (dia < dias.Count)` só termina quando os 5 dias forem preenchidos. Some 1 em `dia` apenas quando o valor for válido.
- Um caractere é dígito quando está entre `'0'` e `'9'`. Então ele é inválido quando `letra < '0' || letra > '9'`.
- Para a média ter casas decimais, guarde o total em uma variável `decimal`.

**Teste.** Digite em sequência: `120`, `abc`, `95`, `150`, `-10`, `110`, (vazio), `178`.

```text
Segunda - pães vendidos: 120
Terça - pães vendidos: abc
Digite só números. Tente de novo.
Terça - pães vendidos: 95
Quarta - pães vendidos: 150
Quinta - pães vendidos: -10
Digite só números. Tente de novo.
Quinta - pães vendidos: 110
Sexta - pães vendidos:
Digite só números. Tente de novo.
Sexta - pães vendidos: 178
Total da semana: 653 pães
Média por dia: 130,60 pães
Dia com mais vendas: Sexta (178 pães)
```
