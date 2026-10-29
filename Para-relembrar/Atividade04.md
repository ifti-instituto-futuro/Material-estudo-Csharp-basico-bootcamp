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

### Gabarito

#### Caminho 1 — `foreach`

```csharp
// Cada linha interna representa um aluno; os índices selecionam nome e notas.
// alunos: [0] nome, [1] nota 1, [2] nota 2
List<List<string>> alunos = new List<List<string>>();
alunos.Add(new List<string> { "Lia", "8", "6" });
alunos.Add(new List<string> { "Noah", "5", "4" });
alunos.Add(new List<string> { "Davi", "7", "4" });

// O foreach entrega uma linha completa a cada repetição.
foreach (List<string> aluno in alunos)
{
    int nota1 = int.Parse(aluno[1]);
    int nota2 = int.Parse(aluno[2]);
    // O divisor 2m força divisão decimal e mantém médias como 4,5.
    decimal media = (nota1 + nota2) / 2m;

    // As faixas são testadas da maior para a menor.
    if (media >= 7)
    {
        Console.WriteLine($"{aluno[0]} | média {media:F1} | Aprovado");
    }
    else if (media >= 5)
    {
        Console.WriteLine($"{aluno[0]} | média {media:F1} | Recuperação");
    }
    else
    {
        Console.WriteLine($"{aluno[0]} | média {media:F1} | Reprovado");
    }
}
```

> **Leitura do código**
>
> - **Linhas 1–6:** constrói uma lista de listas. Cada lista interna representa um aluno: posição `[0]` é o nome, `[1]` a primeira nota e `[2]` a segunda.
> - **Linhas 8–14:** o `foreach` entrega uma linha completa em `aluno`. As notas são convertidas de texto para `int`; dividir por `2m` força uma média decimal, como `4,5`.
> - **Linhas 16–29:** testa as faixas de nota da maior para a menor. Cada aluno recebe uma única situação e `F1` mostra uma casa decimal.

#### Caminho 2 — for com índice

```csharp
// A lista externa guarda as linhas; cada linha guarda nome e notas.
// alunos: [0] nome, [1] nota 1, [2] nota 2
List<List<string>> alunos = new List<List<string>>();
alunos.Add(new List<string> { "Lia", "8", "6" });
alunos.Add(new List<string> { "Noah", "5", "4" });
alunos.Add(new List<string> { "Davi", "7", "4" });

// O índice i seleciona qual aluno será processado.
for (int i = 0; i < alunos.Count; i++)
{
    // O primeiro índice escolhe a linha; o segundo escolhe o campo da nota.
    int nota1 = int.Parse(alunos[i][1]);
    int nota2 = int.Parse(alunos[i][2]);
    // O sufixo m mantém o resultado decimal, inclusive médias terminadas em ,5.
    decimal media = (nota1 + nota2) / 2m;

// As condições classificam a média em uma única situação.
    if (media >= 7)
    {
        Console.WriteLine($"{alunos[i][0]} | média {media:F1} | Aprovado");
    }
    else if (media >= 5)
    {
        Console.WriteLine($"{alunos[i][0]} | média {media:F1} | Recuperação");
    }
    else
    {
        Console.WriteLine($"{alunos[i][0]} | média {media:F1} | Reprovado");
    }
}
```

> **Leitura do código**
>
> - **Linhas 1–6:** organiza os dados na mesma lista aninhada: cada linha contém nome e duas notas.
> - **Linhas 8–15:** o `for` percorre as linhas usando `i`. Em `alunos[i][1]`, o primeiro índice escolhe o aluno e o segundo escolhe a nota. A divisão por `2m` preserva a parte decimal.
> - **Linhas 17–30:** compara a média com as faixas e imprime a situação. O nome usa `alunos[i][0]`, o campo zero da mesma linha que está sendo processada.

Compare: no `foreach`, aluno já é a linha, então o campo é `aluno[1]`. No for, a linha é alunos[i], então o campo é `alunos[i][1]`: o primeiro índice escolhe a linha, o segundo escolhe o campo. Se a divisão fosse por 2 (inteiro), Noah teria média 4 em vez de 4,5. F1 mostra 1 casa decimal.


### Recapitulando os conceitos

A estrutura `List<List<string>>` representa uma tabela: a lista externa reúne alunos e cada lista interna guarda os campos de uma linha. Nesta atividade, `[0]` é o nome, `[1]` é a primeira nota e `[2]` é a segunda. Como as notas foram guardadas como texto, `int.Parse` as converte antes da soma.

A média precisa aceitar resultados fracionários. O sufixo `m` em `2m` faz a divisão usar `decimal`; dividir dois inteiros poderia descartar a parte decimal de uma média como 4,5. O formato `F1` controla a apresentação e exibe uma casa decimal.

O `foreach` percorre cada linha e entrega a lista interna diretamente na variável `aluno`. O `for` percorre as mesmas linhas com o índice `i`; para ler um campo, primeiro seleciona a linha (`alunos[i]`) e depois a coluna (`[1]`, `[2]` ou `[0]`). As condições testam primeiro a média mais alta e seguem para as faixas menores, garantindo uma classificação por aluno.
