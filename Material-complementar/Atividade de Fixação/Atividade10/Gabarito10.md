### Programa B — Fila de impressão

```csharp
List<string> impressao = new List<string>();
string opcao = "";

while (opcao != "0")
{
    Console.WriteLine();
    Console.WriteLine("1 - Enviar documento");
    Console.WriteLine("2 - Ver fila");
    Console.WriteLine("3 - Imprimir próximo");
    Console.WriteLine("0 - Sair");
    Console.Write("Escolha uma opção: ");
    opcao = Console.ReadLine() ?? "";

    switch (opcao)
    {
        case "1":
        {
            Console.Write("Nome do documento: ");
            string documento = (Console.ReadLine() ?? "").Trim();

            if (documento == "")
            {
                Console.WriteLine("Nome vazio. O documento não foi enviado.");
            }
            else
            {
                impressao.Add(documento);
                Console.WriteLine($"{documento} entrou no fim da fila.");
            }
            break;
        }
        case "2":
            if (impressao.Count == 0)
            {
                Console.WriteLine("A fila está vazia.");
            }
            else
            {
                Console.WriteLine("Posição Documento");
                for (int i = 0; i < impressao.Count; i++)
                {
                    Console.WriteLine($"{i + 1} {impressao[i]}");
                }
            }
            break;
        case "3":
        {
            if (impressao.Count == 0)
            {
                Console.WriteLine("Não há documentos na fila.");
                break;
            }

            string proximo = impressao[0];
            Console.Write($"Cópias de {proximo} (1 a 5): ");
            string copias = Console.ReadLine() ?? "";

            switch (copias)
            {
                case "1": case "2": case "3": case "4": case "5":
                    impressao.RemoveAt(0);
                    Console.WriteLine($"{proximo} impresso com {copias} cópia(s).");
                    break;
                default:
                    Console.WriteLine($"Número de cópias inválido. {proximo} continua no início da fila.");
                    break;
            }
            break;
        }
        case "0":
            Console.WriteLine("Encerrando.");
            break;
        default:
            Console.WriteLine("Opção inválida. Escolha uma opção de 0 a 3.");
            break;
    }
}
```

O ponto principal está no `case "3"`: o programa lê `impressao[0]`, valida as cópias e só chama `RemoveAt(0)` dentro do `case` válido. O `switch` de dentro tem o seu próprio `break`, que encerra só esse `switch`. Depois, o `break` de fora encerra o `case "3"` do menu.
