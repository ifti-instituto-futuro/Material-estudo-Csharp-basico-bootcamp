#### Questão 1 — Eleição do representante de turma (Tipagem, Operadores, while, switch, if/else)

**Situação.** A turma do 3º ano B vai eleger seu representante. As candidatas são Ana (número 1) e Bruno (número 2). O computador da sala fica aberto e cada aluno digita seu voto, um por vez. Qualquer valor diferente de 1 ou 2, inclusive letras, conta como voto nulo. Quando a professora digita 0, a votação termina e o programa mostra o resultado.

**O que o programa deve fazer.**

- Repetir a leitura de votos até alguém digitar `0`. O `0` não conta como voto.
- Contar os votos de Ana, de Bruno e os nulos em 3 variáveis `int`.
- No fim, mostrar a contagem e o vencedor, ou `Empate`.

**Dois caminhos de solução.**

- **Caminho 1:** `while` que testa o voto na condição (`while (voto != "0")`) e `switch` para contar o voto.
- **Caminho 2:** `while` controlado por uma variável `bool` (`while (votacaoAberta)`) e `if / else if` para contar o voto. Quando alguém digita `0`, a variável passa a ser `false` e o laço termina.

**Testes.**

| Votos digitados | Saída esperada |
| --- | --- |
| 1, 2, 1, x, 0 | `Ana: 2 \| Bruno: 1 \| Nulos: 1` e `Vencedora: Ana` |
| 1, 2, 0 | `Ana: 1 \| Bruno: 1 \| Nulos: 0` e `Empate` |
