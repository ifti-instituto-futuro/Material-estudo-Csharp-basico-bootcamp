### Questão 1 — Eleição do representante de turma

**Caminho 1 — `while` e `switch`**

```csharp
int votosAna = 0;
int votosBruno = 0;
int nulos = 0;
string voto = "";

while (voto != "0")
{
    Console.Write("Voto (1 Ana, 2 Bruno, 0 encerra): ");
    voto = Console.ReadLine() ?? "";

    switch (voto)
    {
        case "1": votosAna++; break;
        case "2": votosBruno++; break;
        case "0": break;
        default: nulos++; break;
    }
}

Console.WriteLine($"Ana: {votosAna} | Bruno: {votosBruno} | Nulos: {nulos}");

if (votosAna > votosBruno)
{
    Console.WriteLine("Vencedora: Ana");
}
else if (votosBruno > votosAna)
{
    Console.WriteLine("Vencedor: Bruno");
}
else
{
    Console.WriteLine("Empate");
}
```

**Caminho 2 — `while` com variável `bool` e `if / else if`**

```csharp
int votosAna = 0;
int votosBruno = 0;
int nulos = 0;
bool votacaoAberta = true;

while (votacaoAberta)
{
    Console.Write("Voto (1 Ana, 2 Bruno, 0 encerra): ");
    string voto = Console.ReadLine() ?? "";

    if (voto == "0")
    {
        votacaoAberta = false;
    }
    else if (voto == "1")
    {
        votosAna++;
    }
    else if (voto == "2")
    {
        votosBruno++;
    }
    else
    {
        nulos++;
    }
}

Console.WriteLine($"Ana: {votosAna} | Bruno: {votosBruno} | Nulos: {nulos}");

if (votosAna > votosBruno)
{
    Console.WriteLine("Vencedora: Ana");
}
else if (votosBruno > votosAna)
{
    Console.WriteLine("Vencedor: Bruno");
}
else
{
    Console.WriteLine("Empate");
}
```

**Compare:** no caminho 1, o `case "0"` existe só para o `0` não cair no `default` e virar nulo. No caminho 2, o `0` é testado primeiro e só muda `votacaoAberta` para `false`. Assim, ele nunca chega ao `else` dos nulos. No caminho 2, `voto` pode ser declarada dentro do `while`, porque a condição do laço não usa `voto`. A variável `bool` de controle também serve quando o laço tem mais de um motivo para parar.
