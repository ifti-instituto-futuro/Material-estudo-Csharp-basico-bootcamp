### Questão 6 — Lista de convidados do casamento

**Caminho 1 — menu com `switch`, busca com `foreach` e `bool`**

```csharp
List<string> convidados = new List<string>();
string opcao = "";

while (opcao != "0")
{
    Console.WriteLine();
    Console.WriteLine("1 - Adicionar  2 - Conferir  3 - Listar  0 - Sair");
    Console.Write("Opção: ");
    opcao = Console.ReadLine() ?? "";

    switch (opcao)
    {
        case "1":
        {
            Console.Write("Nome do convidado: ");
            string nome = (Console.ReadLine() ?? "").Trim();

            bool jaExiste = false;
            foreach (string convidado in convidados)
            {
                if (convidado.ToLower() == nome.ToLower())
                {
                    jaExiste = true;
                }
            }

            if (nome.Length < 3)
            {
                Console.WriteLine("O nome precisa ter pelo menos 3 caracteres.");
            }
            else if (jaExiste)
            {
                Console.WriteLine($"{nome} já está na lista.");
            }
            else
            {
                convidados.Add(nome);
                Console.WriteLine($"{nome} adicionado.");
            }
            break;
        }
        case "2":
        {
            Console.Write("Nome na portaria: ");
            string busca = (Console.ReadLine() ?? "").Trim();

            bool encontrado = false;
            foreach (string convidado in convidados)
            {
                if (convidado.ToLower() == busca.ToLower())
                {
                    encontrado = true;
                }
            }

            if (encontrado)
            {
                Console.WriteLine("Entrada liberada.");
            }
            else
            {
                Console.WriteLine("Nome não está na lista.");
            }
            break;
        }
        case "3":
            if (convidados.Count == 0)
            {
                Console.WriteLine("Nenhum convidado na lista.");
            }
            else
            {
                for (int i = 0; i < convidados.Count; i++)
                {
                    Console.WriteLine($"{i + 1}. {convidados[i]}");
                }
                Console.WriteLine($"Total: {convidados.Count}");
            }
            break;
        case "0":
            Console.WriteLine("Encerrando.");
            break;
        default:
            Console.WriteLine("Opção inválida. Escolha uma opção de 0 a 3.");
            break;
    }
}
```

**Caminho 2 — menu com `if / else if`, busca com `for`, `-1` e `break`**

```csharp
List<string> convidados = new List<string>();
string opcao = "";

while (opcao != "0")
{
    Console.WriteLine();
    Console.WriteLine("1 - Adicionar  2 - Conferir  3 - Listar  0 - Sair");
    Console.Write("Opção: ");
    opcao = Console.ReadLine() ?? "";

    if (opcao == "1" || opcao == "2")
    {
        Console.Write("Nome: ");
        string nome = (Console.ReadLine() ?? "").Trim();

        int posicao = -1;
        for (int i = 0; i < convidados.Count; i++)
        {
            if (string.Equals(convidados[i], nome, StringComparison.OrdinalIgnoreCase))
            {
                posicao = i;
                break;
            }
        }

        if (opcao == "1")
        {
            if (nome.Length < 3)
            {
                Console.WriteLine("O nome precisa ter pelo menos 3 caracteres.");
            }
            else if (posicao != -1)
            {
                Console.WriteLine($"{nome} já está na lista.");
            }
            else
            {
                convidados.Add(nome);
                Console.WriteLine($"{nome} adicionado.");
            }
        }
        else if (posicao != -1)
        {
            Console.WriteLine("Entrada liberada.");
        }
        else
        {
            Console.WriteLine("Nome não está na lista.");
        }
    }
    else if (opcao == "3")
    {
        if (convidados.Count == 0)
        {
            Console.WriteLine("Nenhum convidado na lista.");
        }
        else
        {
            for (int i = 0; i < convidados.Count; i++)
            {
                Console.WriteLine($"{i + 1}. {convidados[i]}");
            }
            Console.WriteLine($"Total: {convidados.Count}");
        }
    }
    else if (opcao == "0")
    {
        Console.WriteLine("Encerrando.");
    }
    else
    {
        Console.WriteLine("Opção inválida. Escolha uma opção de 0 a 3.");
    }
}
```

**Compare:** o caminho 1 repete a mesma busca nas opções 1 e 2. O caminho 2 junta as duas opções com `||` e faz a busca uma só vez. Ele fica mais curto, mas mais difícil de ler. O `break` dentro do `for` para a busca no primeiro nome igual.
