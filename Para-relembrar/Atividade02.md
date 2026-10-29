## Questão 2 — Cadastro de usuários da biblioteca digital (Strings, List, `foreach`, Operadores lógicos, if/else)

**Situação.** A biblioteca digital da escola cria um login para cada aluno. Três alunos já têm login: lia.souza, noah.lima e davi.rocha. O sistema só aceita um novo nome de usuário que siga 3 regras: ter de 4 a 12 caracteres, não ter espaços no meio e não repetir um usuário já cadastrado. A comparação não diferencia maiúsculas de minúsculas: NOAH.LIMA é o mesmo usuário que noah.lima. Os espaços digitados sem querer no início e no fim devem ser removidos antes das regras. Quando o nome não passa, o aluno precisa saber qual regra quebrou.

**O que o programa deve fazer.**

- Começar com uma `List<string>` com os 3 usuários já cadastrados.
- Ler o nome de usuário e remover os espaços do início e do fim.
- Testar as regras nesta ordem: tamanho, espaços, usuário repetido.
- Mostrar a mensagem da primeira regra que falhou.
- Se o nome passar nas 3 regras, acrescentá-lo na lista e mostrar o total de usuários.

**Dois caminhos de solução.**

- Caminho 1: `Contains(" ")` para achar espaços. Um `foreach` na lista, com uma variável `bool` e `ToLower()`, para achar o usuário repetido.
- Caminho 2: um `foreach` que passa por cada letra (`char`) do nome para achar espaços. Um for na lista, com a posição -1, `break` e `string.Equals` com `StringComparison.OrdinalIgnoreCase`, para achar o usuário repetido.

**Testes.**

| Entrada | Saída esperada |
| --- | --- |
| `Ana.Lima` | Usuário Ana.Lima criado. Total de usuários: 4 |
| `ana` | O usuário precisa ter de 4 a 12 caracteres. |
| `ana lima` | O usuário não pode ter espaços. |
| `NOAH.LIMA` | Este usuário já está cadastrado. |

### Gabarito

#### Caminho 1 — Contains, `foreach` e ToLower

```csharp
// A lista começa com os nomes já cadastrados.
List<string> usuarios = new List<string> { "lia.souza", "noah.lima", "davi.rocha" };

Console.Write("Nome de usuário: ");
// Trim remove espaços das pontas antes de validar.
string usuario = (Console.ReadLine() ?? "").Trim();

// A variável registra se a busca encontrar o nome.
bool jaCadastrado = false;
foreach (string cadastrado in usuarios)
{
    // ToLower faz a comparação ignorar diferenças entre maiúsculas e minúsculas.
    if (cadastrado.ToLower() == usuario.ToLower())
    {
        jaCadastrado = true;
    }
}

// As regras são verificadas em ordem; a primeira falha define a mensagem.
if (usuario.Length < 4 || usuario.Length > 12)
{
    Console.WriteLine("O usuário precisa ter de 4 a 12 caracteres.");
}
// Contains detecta espaço no meio do nome.
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
    // Só adiciona à lista depois que todas as validações passam.
    usuarios.Add(usuario);
    Console.WriteLine($"Usuário {usuario} criado. Total de usuários: {usuarios.Count}");
}
```

> **Leitura do código**
>
> - **Linhas 1–6:** cria a lista com os usuários atuais, pede um nome e aplica `Trim()` para retirar espaços das pontas antes de validar.
> - **Linhas 8–17:** percorre os nomes cadastrados com `foreach`. `ToLower()` dos dois lados faz a comparação ignorar maiúsculas e minúsculas; `jaCadastrado` guarda o resultado da busca.
> - **Linhas 19–32:** valida tamanho, espaço e duplicidade nessa ordem. O `else if` faz aparecer somente a primeira regra que falhou.
> - **Linhas 33–38:** só chega ao `Add` quando todas as regras passaram; depois mostra a lista atualizada com `Count`.

#### Caminho 2 — `foreach` nas letras, for com `break` e `string.Equals`

```csharp
// A lista guarda os usuários existentes para comparação.
List<string> usuarios = new List<string> { "lia.souza", "noah.lima", "davi.rocha" };

Console.Write("Nome de usuário: ");
// Remove espaços no início e no fim antes dos testes.
string usuario = (Console.ReadLine() ?? "").Trim();

// A busca pelas letras marca se encontrar um espaço.
bool temEspaco = false;
// O foreach examina cada caractere do nome.
foreach (char letra in usuario)
{
    if (letra == ' ')
    {
        temEspaco = true;
    }
}

// -1 significa que o usuário ainda não foi encontrado.
int posicao = -1;
for (int i = 0; i < usuarios.Count; i++)
{
    // A comparação ignora caixa alta e baixa sem criar cópias dos textos.
    if (string.Equals(usuarios[i], usuario, StringComparison.OrdinalIgnoreCase))
    {
        posicao = i;
        // Interrompe a busca assim que encontra o primeiro resultado.
        break;
    }
}

// Valida as regras na ordem pedida.
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

> **Leitura do código**
>
> - **Linhas 1–6:** prepara os usuários e limpa as pontas do nome recebido.
> - **Linhas 8–17:** o `foreach` examina cada `char` para detectar espaços. Esse laço é adequado porque precisamos visitar as letras, sem precisar saber antecipadamente onde está um espaço.
> - **Linhas 19–30:** `posicao` começa em `-1` para representar “não encontrado”. O `for` percorre a lista por índice; `string.Equals` ignora diferenças entre maiúsculas e minúsculas e `break` encerra a busca no primeiro resultado.
> - **Linhas 32–49:** aplica as três validações em ordem e só acrescenta o nome quando ele é válido e ainda não existe.

Compare: uma `string` é uma sequência de `char`, então o `foreach` passa por cada letra. Um `char` fica entre aspas simples: ' '. O `foreach` com `bool` só diz se o usuário existe. O for com -1 também diz em que posição ele está, e o `break` para a busca no primeiro igual. O else if garante que só a primeira regra quebrada aparece, e que o Add só acontece quando todas passam.


### Recapitulando os conceitos

Uma `List<string>` guarda uma quantidade variável de nomes e permite acrescentar um usuário com `Add()`. `Count` informa quantos itens estão na lista. A leitura do console pode resultar em `null`; `?? ""` fornece um texto vazio, e `Trim()` remove espaços somente no início e no fim.

As duas soluções fazem uma busca, mas usam ferramentas diferentes. `foreach` percorre cada usuário ou cada caractere sem exigir que o programa controle a posição. `for` oferece o índice `i`, útil para saber onde o usuário foi encontrado. A posição `-1` funciona como marca de “não encontrado”, e `break` encerra a busca assim que há resultado.

A comparação precisa ignorar maiúsculas e minúsculas. O primeiro caminho converte ambos os nomes com `ToLower()`; o segundo usa `string.Equals` com `OrdinalIgnoreCase`. Depois da busca, as regras são verificadas numa ordem definida. O `else if` garante uma única mensagem de erro, e a inclusão só ocorre quando todas as regras passam.
