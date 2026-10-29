### Questão 3 — Cadastro de usuários da biblioteca digital

**Caminho 1 — `Contains`, `foreach` e `ToLower`**

```csharp
List<string> usuarios = new List<string> { "lia.souza", "noah.lima", "davi.rocha" };

Console.Write("Nome de usuário: ");
string usuario = (Console.ReadLine() ?? "").Trim();

bool jaCadastrado = false;
foreach (string cadastrado in usuarios)
{
    if (cadastrado.ToLower() == usuario.ToLower())
    {
        jaCadastrado = true;
    }
}

if (usuario.Length < 4 || usuario.Length > 12)
{
    Console.WriteLine("O usuário precisa ter de 4 a 12 caracteres.");
}
else if (usuario.Contains(" "))
{
    Console.WriteLine("O usuário não pode ter espaços.");
}
else if (jaCadastrado)
{
    Console.WriteLine("Este usuário já está cadastrado.");
}
else
{
    usuarios.Add(usuario);
    Console.WriteLine($"Usuário {usuario} criado. Total de usuários: {usuarios.Count}");
}
```

**Caminho 2 — `foreach` nas letras, `for` com `break` e `string.Equals`**

```csharp
List<string> usuarios = new List<string> { "lia.souza", "noah.lima", "davi.rocha" };

Console.Write("Nome de usuário: ");
string usuario = (Console.ReadLine() ?? "").Trim();

bool temEspaco = false;
foreach (char letra in usuario)
{
    if (letra == ' ')
    {
        temEspaco = true;
    }
}

int posicao = -1;
for (int i = 0; i < usuarios.Count; i++)
{
    if (string.Equals(usuarios[i], usuario, StringComparison.OrdinalIgnoreCase))
    {
        posicao = i;
        break;
    }
}

if (usuario.Length < 4 || usuario.Length > 12)
{
    Console.WriteLine("O usuário precisa ter de 4 a 12 caracteres.");
}
else if (temEspaco)
{
    Console.WriteLine("O usuário não pode ter espaços.");
}
else if (posicao != -1)
{
    Console.WriteLine("Este usuário já está cadastrado.");
}
else
{
    usuarios.Add(usuario);
    Console.WriteLine($"Usuário {usuario} criado. Total de usuários: {usuarios.Count}");
}
```

**Compare:** uma `string` é uma sequência de `char`, então o `foreach` passa por cada letra. Um `char` fica entre aspas simples: `' '`. O `foreach` com `bool` só diz se o usuário existe. O `for` com `-1` também diz em que posição ele está, e o `break` para a busca no primeiro igual. O `else if` garante que só a primeira regra quebrada aparece, e que o `Add` só acontece quando todas passam.
