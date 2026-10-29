### Questão 8 — Caixa da cantina

**Caminho 1 — `while`, `switch` e percentual inteiro**

```csharp
decimal subtotal = 0m;
int itens = 0;
string codigo = "";

while (codigo != "0")
{
    Console.Write("Produto (1 Salgado, 2 Suco, 3 Bolo, 0 encerra): ");
    codigo = Console.ReadLine() ?? "";

    switch (codigo)
    {
        case "1": subtotal = subtotal + 6.50m; itens++; break;
        case "2": subtotal = subtotal + 5.00m; itens++; break;
        case "3": subtotal = subtotal + 4.50m; itens++; break;
        case "0": break;
        default: Console.WriteLine("Código inválido. Item ignorado."); break;
    }
}

decimal percentual = 0m;
if (subtotal >= 30m)
{
    percentual = 10m;
}
else if (subtotal >= 20m)
{
    percentual = 5m;
}

decimal desconto = subtotal * percentual / 100;

Console.WriteLine($"Itens: {itens}");
Console.WriteLine($"Subtotal: R$ {subtotal:F2}");
Console.WriteLine($"Desconto ({percentual}%): R$ {desconto:F2}");
Console.WriteLine($"Total: R$ {subtotal - desconto:F2}");
```

**Caminho 2 — `while` com variável `bool`, `if / else if` e taxa em fração**

```csharp
decimal subtotal = 0m;
int itens = 0;
bool caixaAberto = true;

while (caixaAberto)
{
    Console.Write("Produto (1 Salgado, 2 Suco, 3 Bolo, 0 encerra): ");
    string codigo = Console.ReadLine() ?? "";

    if (codigo == "0")
    {
        caixaAberto = false;
    }
    else if (codigo == "1")
    {
        subtotal = subtotal + 6.50m;
        itens++;
    }
    else if (codigo == "2")
    {
        subtotal = subtotal + 5.00m;
        itens++;
    }
    else if (codigo == "3")
    {
        subtotal = subtotal + 4.50m;
        itens++;
    }
    else
    {
        Console.WriteLine("Código inválido. Item ignorado.");
    }
}

decimal taxa;
if (subtotal >= 30m)
{
    taxa = 0.10m;
}
else if (subtotal >= 20m)
{
    taxa = 0.05m;
}
else
{
    taxa = 0m;
}

decimal desconto = subtotal * taxa;

Console.WriteLine($"Itens: {itens}");
Console.WriteLine($"Subtotal: R$ {subtotal:F2}");
Console.WriteLine($"Desconto ({taxa * 100:F0}%): R$ {desconto:F2}");
Console.WriteLine($"Total: R$ {subtotal - desconto:F2}");
```

**Compare:** o código do produto é comparado como texto, então letras caem no `default` (caminho 1) ou no `else` (caminho 2) e o programa nunca quebra. No caminho 1, o `case "0"` existe só para o `0` não virar código inválido. O teste das faixas de desconto começa pelo maior valor (`>= 30`). Se começasse por `>= 20`, uma compra de R$ 32,50 receberia só 5%. `F0` mostra o número sem casas decimais.
