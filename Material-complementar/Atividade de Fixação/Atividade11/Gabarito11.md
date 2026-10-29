### Programa C — Ingressos do cinema

```csharp
using System.Globalization;

CultureInfo.CurrentCulture = new CultureInfo("pt-BR");

Console.Write("Tipo de ingresso (1 - Inteira, 2 - Meia, 3 - Estudante): ");
string codigoTipo = Console.ReadLine() ?? "";

decimal percentual = 0m;
string tipo = "";

switch (codigoTipo)
{
    case "1": tipo = "Inteira";   percentual = 0m;  break;
    case "2": tipo = "Meia";      percentual = 50m; break;
    case "3": tipo = "Estudante"; percentual = 30m; break;
}

if (tipo == "")
{
    Console.WriteLine("Tipo inválido.");
}
else
{
    Console.Write("Sessão (1 - Tarde R$ 30,00, 2 - Noite R$ 44,00): ");
    string codigoSessao = Console.ReadLine() ?? "";
    decimal precoBase = 0m;

    switch (codigoSessao)
    {
        case "1": precoBase = 30.00m; break;
        case "2": precoBase = 44.00m; break;
    }

    if (precoBase == 0m)
    {
        Console.WriteLine("Sessão inválida.");
    }
    else
    {
        decimal valorFinal = precoBase - (precoBase * percentual / 100);
        Console.WriteLine($"Ingresso {tipo} ({percentual}%). Valor: R$ {valorFinal:F2}");
    }
}
```
