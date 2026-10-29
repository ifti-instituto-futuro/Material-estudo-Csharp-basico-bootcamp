### Questão 7 — Boletim da turma

**Caminho 1 — `foreach`**

```csharp
// alunos: [0] nome, [1] nota 1, [2] nota 2
List<List<string>> alunos = new List<List<string>>();
alunos.Add(new List<string> { "Lia", "8", "6" });
alunos.Add(new List<string> { "Noah", "5", "4" });
alunos.Add(new List<string> { "Davi", "7", "4" });

foreach (List<string> aluno in alunos)
{
    int nota1 = int.Parse(aluno[1]);
    int nota2 = int.Parse(aluno[2]);
    decimal media = (nota1 + nota2) / 2m;

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

**Caminho 2 — `for` com índice**

```csharp
// alunos: [0] nome, [1] nota 1, [2] nota 2
List<List<string>> alunos = new List<List<string>>();
alunos.Add(new List<string> { "Lia", "8", "6" });
alunos.Add(new List<string> { "Noah", "5", "4" });
alunos.Add(new List<string> { "Davi", "7", "4" });

for (int i = 0; i < alunos.Count; i++)
{
    int nota1 = int.Parse(alunos[i][1]);
    int nota2 = int.Parse(alunos[i][2]);
    decimal media = (nota1 + nota2) / 2m;

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

**Compare:** no `foreach`, `aluno` já é a linha, então o campo é `aluno[1]`. No `for`, a linha é `alunos[i]`, então o campo é `alunos[i][1]`: o primeiro índice escolhe a linha, o segundo escolhe o campo. Se a divisão fosse por `2` (inteiro), Noah teria média 4 em vez de 4,5. `F1` mostra 1 casa decimal.
