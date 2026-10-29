### Programa A — Cadastro de produtos

```csharp
// produtos: [0] nome, [1] categoria
List<List<string>> produtos = new List<List<string>>();
string opcao = "";

while (opcao != "0")
{
    Console.WriteLine();
    Console.WriteLine("1 - Cadastrar produto");
    Console.WriteLine("2 - Listar produtos");
    Console.WriteLine("0 - Sair");
    Console.Write("Escolha uma opção: ");
    opcao = Console.ReadLine() ?? "";

    switch (opcao)
    {
        case "1":
        {
            Console.Write("Nome do produto: ");
            string nome = (Console.ReadLine() ?? "").Trim();

            if (nome.Length < 3)
            {
                Console.WriteLine("O nome precisa ter pelo menos 3 caracteres.");
                break;
            }

            bool jaExiste = false;
            foreach (List<string> produto in produtos)
            {
                if (produto[0].ToLower() == nome.ToLower())
                {
                    jaExiste = true;
                }
            }

            if (jaExiste)
            {
                Console.WriteLine("Este produto já está cadastrado.");
                break;
            }

            Console.Write("Categoria (1 - Papelaria, 2 - Informática): ");
            string codigo = Console.ReadLine() ?? "";
            string categoria = "";

            switch (codigo)
            {
                case "1": categoria = "Papelaria"; break;
                case "2": categoria = "Informática"; break;
            }

            if (categoria == "")
            {
                Console.WriteLine("Categoria inválida.");
                break;
            }

            produtos.Add(new List<string> { nome, categoria });
            Console.WriteLine($"Produto {nome} cadastrado em {categoria}.");
            break;
        }
        case "2":
            if (produtos.Count == 0)
            {
                Console.WriteLine("Nenhum produto cadastrado.");
            }
            else
            {
                foreach (List<string> produto in produtos)
                {
                    Console.WriteLine($"{produto[0]} | {produto[1]}");
                }
            }
            break;
        case "0":
            Console.WriteLine("Encerrando.");
            break;
        default:
            Console.WriteLine("Opção inválida. Escolha uma opção de 0 a 2.");
            break;
    }
}
```

O `break` dentro do `case "1"` encerra o `case` logo depois de uma validação que falhou. Assim, nada é guardado com dados inválidos.
