### Questão 2 — Academia Movimento

**Caminho 1 — `if / else if`**

```csharp
Console.Write("Código do plano (1 Básico, 2 Plus, 3 Total): ");
string codigo = Console.ReadLine() ?? "";
Console.Write("Quantidade de meses: ");
int meses = int.Parse(Console.ReadLine() ?? "0");

string plano = "";
decimal precoMensal = 0m;

if (codigo == "1")
{
    plano = "Básico";
    precoMensal = 89.90m;
}
else if (codigo == "2")
{
    plano = "Plus";
    precoMensal = 119.90m;
}
else if (codigo == "3")
{
    plano = "Total";
    precoMensal = 149.90m;
}

if (plano == "")
{
    Console.WriteLine("Plano inválido.");
}
else
{
    decimal total = precoMensal * meses;
    Console.WriteLine($"Plano {plano}: {meses} mês(es) = R$ {total:F2}");
}
```

**Caminho 2 — `switch`**

```csharp
Console.Write("Código do plano (1 Básico, 2 Plus, 3 Total): ");
string codigo = Console.ReadLine() ?? "";
Console.Write("Quantidade de meses: ");
int meses = int.Parse(Console.ReadLine() ?? "0");

string plano = "";
decimal precoMensal = 0m;

switch (codigo)
{
    case "1": plano = "Básico"; precoMensal = 89.90m; break;
    case "2": plano = "Plus"; precoMensal = 119.90m; break;
    case "3": plano = "Total"; precoMensal = 149.90m; break;
}

if (plano == "")
{
    Console.WriteLine("Plano inválido.");
}
else
{
    decimal total = precoMensal * meses;
    Console.WriteLine($"Plano {plano}: {meses} mês(es) = R$ {total:F2}");
}
```

**Compare:** os dois caminhos usam `plano == ""` para saber se o código era válido. Para códigos fixos, o `switch` fica mais curto. `decimal` vezes `int` dá `decimal`, então o total não perde os centavos.
