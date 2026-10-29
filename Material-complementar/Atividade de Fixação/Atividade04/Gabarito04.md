### Questão 4 — Pães da padaria

**Caminho 1 — validação com `foreach` e resumo com `for`**

```csharp
List<string> dias = new List<string> { "Segunda", "Terça", "Quarta", "Quinta", "Sexta" };
List<int> paes = new List<int>();

int dia = 0;
while (dia < dias.Count)
{
    Console.Write($"{dias[dia]} - pães vendidos: ");
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
        paes.Add(int.Parse(texto));
        dia++;
    }
    else
    {
        Console.WriteLine("Digite só números. Tente de novo.");
    }
}

decimal total = 0m;
int posicaoMaior = 0;

for (int i = 0; i < paes.Count; i++)
{
    total = total + paes[i];

    if (paes[i] > paes[posicaoMaior])
    {
        posicaoMaior = i;
    }
}

Console.WriteLine($"Total da semana: {total} pães");
Console.WriteLine($"Média por dia: {total / paes.Count:F2} pães");
Console.WriteLine($"Dia com mais vendas: {dias[posicaoMaior]} ({paes[posicaoMaior]} pães)");
```

**Caminho 2 — validação com `for` e resumo com `foreach`**

```csharp
List<string> dias = new List<string> { "Segunda", "Terça", "Quarta", "Quinta", "Sexta" };
List<int> paes = new List<int>();

int dia = 0;
while (dia < dias.Count)
{
    Console.Write($"{dias[dia]} - pães vendidos: ");
    string texto = (Console.ReadLine() ?? "").Trim();

    bool valido = texto != "";
    for (int i = 0; i < texto.Length; i++)
    {
        if (texto[i] < '0' || texto[i] > '9')
        {
            valido = false;
        }
    }

    if (valido)
    {
        paes.Add(int.Parse(texto));
        dia++;
    }
    else
    {
        Console.WriteLine("Digite só números. Tente de novo.");
    }
}

decimal total = 0m;
int maior = 0;
string diaMaior = "";
int posicao = 0;

foreach (int quantidade in paes)
{
    total = total + quantidade;

    if (quantidade > maior)
    {
        maior = quantidade;
        diaMaior = dias[posicao];
    }

    posicao++;
}

Console.WriteLine($"Total da semana: {total} pães");
Console.WriteLine($"Média por dia: {total / paes.Count:F2} pães");
Console.WriteLine($"Dia com mais vendas: {diaMaior} ({maior} pães)");
```

**Compare:** o ponto principal dos 2 caminhos é o `dia++` dentro do bloco válido. Com valor inválido, `dia` não muda, então o `while` pede o mesmo dia de novo. A validação começa com `valido = texto != ""`, que recusa o texto vazio. Depois, qualquer caractere fora de `'0'` a `'9'` muda `valido` para `false`, inclusive letras e o sinal `-`. Como o texto já foi conferido, o `int.Parse` nunca quebra. O `foreach` dá cada caractere direto. O `for` usa a posição `i` e lê o caractere com `texto[i]`. O total é `decimal` para que `total / paes.Count` mantenha as casas decimais (653 / 5 = 130,60).
