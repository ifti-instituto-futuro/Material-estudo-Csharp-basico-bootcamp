### Questão 5 — Frete da loja online

**Caminho 1 — `switch` e validação com `foreach`**

```csharp
Console.Write("Região (1 Nordeste, 2 Sudeste, 3 Sul, 4 Norte/Centro-Oeste): ");
string regiao = Console.ReadLine() ?? "";

decimal freteBase = 0m;
switch (regiao)
{
    case "1": freteBase = 15.00m; break;
    case "2": freteBase = 25.00m; break;
    case "3": freteBase = 30.00m; break;
    case "4": freteBase = 35.00m; break;
}

if (freteBase == 0m)
{
    Console.WriteLine("Região inválida.");
}
else
{
    Console.Write("Peso em kg (número inteiro): ");
    string texto = (Console.ReadLine() ?? "").Trim();

    bool valido = texto != "";
    foreach (char letra in texto)
    {
        if (letra < '0' || letra > '9')
        {
            valido = false;
        }
    }

    if (valido)
    {
        int peso = int.Parse(texto);
        decimal frete = freteBase;

        if (peso > 5)
        {
            frete = frete + (peso - 5) * 2.50m;
        }

        Console.WriteLine($"Frete: R$ {frete:F2}");
    }
    else
    {
        Console.WriteLine("Digite o peso só com números.");
    }
}
```

**Caminho 2 — `if / else if` e validação com `for`**

```csharp
Console.Write("Região (1 Nordeste, 2 Sudeste, 3 Sul, 4 Norte/Centro-Oeste): ");
string regiao = Console.ReadLine() ?? "";

decimal freteBase;
if (regiao == "1")
{
    freteBase = 15.00m;
}
else if (regiao == "2")
{
    freteBase = 25.00m;
}
else if (regiao == "3")
{
    freteBase = 30.00m;
}
else if (regiao == "4")
{
    freteBase = 35.00m;
}
else
{
    freteBase = 0m;
}

if (freteBase == 0m)
{
    Console.WriteLine("Região inválida.");
}
else
{
    Console.Write("Peso em kg (número inteiro): ");
    string texto = (Console.ReadLine() ?? "").Trim();

    bool valido = texto != "";
    for (int i = 0; i < texto.Length; i++)
    {
        if (texto[i] < '0' || texto[i] > '9')
        {
            valido = false;
        }
    }

    if (!valido)
    {
        Console.WriteLine("Digite o peso só com números.");
    }
    else if (int.Parse(texto) <= 5)
    {
        Console.WriteLine($"Frete: R$ {freteBase:F2}");
    }
    else
    {
        int pesoExtra = int.Parse(texto) - 5;
        decimal frete = freteBase + pesoExtra * 2.50m;
        Console.WriteLine($"Frete: R$ {frete:F2}");
    }
}
```

**Compare:** os 2 caminhos usam `freteBase == 0m` para saber se a região era válida, porque nenhuma região real tem frete zero. O caminho 1 calcula o frete em uma variável e soma o extra só se o peso passar de 5 kg. O caminho 2 testa primeiro o erro e depois cada faixa de peso em uma linha de `else if`. No teste 2, 8: o excesso é 3 kg × R$ 2,50 = R$ 7,50, e o frete fica R$ 25,00 + R$ 7,50 = R$ 32,50. `7,5` é recusado porque a vírgula não é um dígito.
