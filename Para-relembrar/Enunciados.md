# Enunciados — Bootcamp C# — Questões com 2 Caminhos

## Questão 1 — Eleição do representante de turma (Tipagem, Operadores, `while`, `switch`, if/else)

**Situação.** A turma do 3º ano B vai eleger seu representante. As candidatas são Ana (número 1) e Bruno (número 2). O computador da sala fica aberto e cada aluno digita seu voto, um por vez. Qualquer valor diferente de 1 ou 2, inclusive letras, conta como voto nulo. Quando a professora digita 0, a votação termina e o programa mostra o resultado.

**O que o programa deve fazer.**

- Repetir a leitura de votos até alguém digitar 0. O 0 não conta como voto.
- Contar os votos de Ana, de Bruno e os nulos em 3 variáveis `int`.
- No fim, mostrar a contagem e o vencedor, ou Empate.

**Dois caminhos de solução.**

- Caminho 1: `while` que testa o voto na condição (`while (voto != "0")`) e `switch` para contar o voto.
- Caminho 2: `while` controlado por uma variável `bool` (`while (votacaoAberta)`) e if / else if para contar o voto. Quando alguém digita 0, a variável passa a ser `false` e o laço termina.

**Testes.**

| Votos digitados | Saída esperada |
| --- | --- |
| 1, 2, 1, x, 0 | Ana: 2 \| Bruno: 1 \| Nulos: 1 e Vencedora: Ana |
| 1, 2, 0 | Ana: 1 \| Bruno: 1 \| Nulos: 0 e Empate |

## Questão 2 — Cadastro de usuários da biblioteca digital (Strings, List, `foreach`, Operadores lógicos, if/else)

**Situação.** A biblioteca digital da escola cria um login para cada aluno. Três alunos já têm login: lia.souza, noah.lima e davi.rocha. O sistema só aceita um novo nome de usuário que siga 3 regras: ter de 4 a 12 caracteres, não ter espaços no meio e não repetir um usuário já cadastrado. A comparação não diferencia maiúsculas de minúsculas: NOAH.LIMA é o mesmo usuário que noah.lima. Os espaços digitados sem querer no início e no fim devem ser removidos antes das regras. Quando o nome não passa, o aluno precisa saber qual regra quebrou.

**O que o programa deve fazer.**

- Começar com uma `List<string>` com os 3 usuários já cadastrados.
- Ler o nome de usuário e remover os espaços do início e do fim.
- Testar as regras nesta ordem: tamanho, espaços, usuário repetido.
- Mostrar a mensagem da primeira regra que falhou.
- Se o nome passar nas 3 regras, acrescentá-lo na lista e mostrar o total de usuários.

**Dois caminhos de solução.**

- Caminho 1: `Contains(" ")` para achar espaços. Um `foreach` na lista, com uma variável `bool` e `ToLower()`, para achar o usuário repetido.
- Caminho 2: um `foreach` que passa por cada letra (`char`) do nome para achar espaços. Um for na lista, com a posição -1, `break` e `string.Equals` com `StringComparison.OrdinalIgnoreCase`, para achar o usuário repetido.

**Testes.**

| Entrada | Saída esperada |
| --- | --- |
| `Ana.Lima` | Usuário Ana.Lima criado. Total de usuários: 4 |
| `ana` | O usuário precisa ter de 4 a 12 caracteres. |
| `ana lima` | O usuário não pode ter espaços. |
| `NOAH.LIMA` | Este usuário já está cadastrado. |

## Questão 3 — Pães da padaria (`while`, Entrada e conversão, Strings, List, for e `foreach`, `decimal`)

**Situação.** Toda sexta à noite, o gerente da Padaria Pão Quente digita quantos pães franceses vendeu em cada dia útil da semana. Às vezes ele erra: aperta uma letra, deixa o campo vazio ou digita um sinal de menos. O programa não pode fechar nem pular o dia quando isso acontece. Ele avisa e pede o mesmo dia de novo. No fim, o gerente quer o total da semana, a média por dia e o dia com mais vendas.

**O que o programa deve fazer.**

- Guardar os dias (Segunda a Sexta) em uma `List<string>` e as quantidades em uma `List<int>`.
- Pedir a quantidade de cada dia com `while`. Só aceitar um texto que não seja vazio e tenha apenas dígitos de 0 a 9. Só então converter com `int.Parse`.
- Com valor inválido, mostrar Digite só números. Tente de novo. e pedir o mesmo dia.
- Mostrar o total, a média com 2 casas decimais e o dia com mais vendas.

**Dois caminhos de solução.**

- Caminho 1: conferir os caracteres com `foreach`. Fazer o resumo com for, guardando a posição do dia com mais vendas.
- Caminho 2: conferir os caracteres com for e `texto[i]`. Fazer o resumo com `foreach` e um contador de posição.

**Dicas para os 2 caminhos:**

- Use `int` dia = 0 como posição do dia atual. O `while (dia < dias.Count)` só termina quando os 5 dias forem preenchidos. Some 1 em dia apenas quando o valor for válido.
- Um caractere é dígito quando está entre '0' e '9'. Então ele é inválido quando letra < '0' || letra > '9'.
- Para a média ter casas decimais, guarde o total em uma variável `decimal`.

**Teste.** Digite em sequência: 120, abc, 95, 150, -10, 110, (vazio), 178.

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

## Questão 4 — Boletim da turma (Lista aninhada, for e `foreach`, Entrada e conversão, `decimal`, if/else)

**Situação.** A coordenação precisa fechar o boletim do bimestre. Cada aluno tem 2 notas inteiras, guardadas como texto em uma tabela: Lia (8 e 6), Noah (5 e 4) e Davi (7 e 4). A média é a soma das 2 notas dividida por 2. Média 7 ou mais é Aprovado, de 5 até menos de 7 é Recuperação, menos de 5 é Reprovado.

**O que o programa deve fazer.**

- Guardar os alunos em uma `List<List<string>>`, com os campos [0] nome, [1] nota 1, [2] nota 2.
- Converter as notas com `int.Parse` e calcular a média em `decimal`. Cuidado: divida por 2m, não por 2.
- Mostrar nome | média | situação para cada aluno, com a média em 1 casa decimal.

**Dois caminhos de solução.**

- Caminho 1: `foreach` nas linhas. Cada linha é um aluno, e o campo é lido com 1 índice: `aluno[1]`.
- Caminho 2: for com índice. O campo é lido com 2 índices: `alunos[i][1]`.

**Saída esperada.**

```text
Lia | média 7,0 | Aprovado
Noah | média 4,5 | Reprovado
Davi | média 5,5 | Recuperação
```
