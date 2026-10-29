# Bootcamp C# — Questões com 2 Caminhos

_28 de out. de 2026 · @Someone_

## Como usar

São 4 questões, da mais simples para a mais completa. Cada questão junta várias aulas e pode ser resolvida por 2 caminhos. Os 2 caminhos devem dar a mesma saída no console. O gabarito de cada questão aparece logo após o enunciado.

| Questão | Situação | Conceitos |
| --- | --- | --- |
| 1 | Eleição do representante de turma | Tipagem, Operadores, `while`, `switch`, if/else |
| 2 | Cadastro de usuários da biblioteca digital | Strings, List, `foreach`, Operadores lógicos, if/else |
| 3 | Pães da padaria | `while`, Entrada e conversão, Strings, List, for e `foreach`, `decimal` |
| 4 | Boletim da turma | Lista aninhada, for e `foreach`, Entrada e conversão, `decimal`, if/else |

### Como trabalhar cada questão

1. Leia a situação e liste os dados que o programa recebe e o que ele mostra.
2. Resolva pelo caminho 1. Execute todos os testes da tabela.
3. Resolva pelo caminho 2. Os testes devem dar a mesma saída.
4. Responda: qual caminho ficou mais fácil de ler? Depois confira no gabarito.

## Questão 1 — Eleição do representante de turma (Tipagem, Operadores, `while`, `switch`, if/else)

**Situação.** A turma do 3º ano B vai eleger seu representante. As candidatas são Ana (número 1) e Bruno (número 2). O computador da sala fica aberto e cada aluno digita seu voto, um por vez. Qualquer valor diferente de 1 ou 2, inclusive letras, conta como voto nulo. Quando a professora digita 0, a votação termina e o programa mostra o resultado.

**O que o programa deve fazer.**

- Repetir a leitura de votos até alguém digitar 0. O 0 não conta como voto.
- Contar os votos de Ana, de Bruno e os nulos em 3 variáveis `int`.
- No fim, mostrar a contagem e o vencedor, ou Empate.

**Dois caminhos de solução.**

- Caminho 1: `while` que testa o voto na condição (`while (voto != "0")`) e `switch` para contar o voto.
- Caminho 2: `while` controlado por uma variável `bool` (`while (votacaoAberta)`) e if / else if para contar o voto. Quando alguém digita 0, a variável passa a ser `false` e o laço termina.

**Testes.**

| Votos digitados | Saída esperada |
| --- | --- |
| 1, 2, 1, x, 0 | Ana: 2 \| Bruno: 1 \| Nulos: 1 e Vencedora: Ana |
| 1, 2, 0 | Ana: 1 \| Bruno: 1 \| Nulos: 0 e Empate |

### Gabarito

Os 2 caminhos de cada questão dão a mesma saída. Todos foram executados e testados com as entradas das tabelas. Se a sua resposta é diferente, mas a saída está certa, ela também vale.

#### Caminho 1 — `while` e `switch`

```csharp
int votosAna = 0;
int votosBruno = 0;
int nulos = 0;
string voto = "";

while (voto != "0")
{
    Console.Write("Voto (1 Ana, 2 Bruno, 0 encerra): ");
    voto = Console.ReadLine() ?? "";

    switch (voto)
    {
        case "1": votosAna++; break;
        case "2": votosBruno++; break;
        case "0": break;
        default: nulos++; break;
    }
}

Console.WriteLine($"Ana: {votosAna} | Bruno: {votosBruno} | Nulos: {nulos}");

if (votosAna > votosBruno)
{
    Console.WriteLine("Vencedora: Ana");
}
else if (votosBruno > votosAna)
{
    Console.WriteLine("Vencedor: Bruno");
}
else
{
    Console.WriteLine("Empate");
}
```

#### Caminho 2 — `while` com variável `bool` e if / else if

```csharp
int votosAna = 0;
int votosBruno = 0;
int nulos = 0;
bool votacaoAberta = true;

while (votacaoAberta)
{
    Console.Write("Voto (1 Ana, 2 Bruno, 0 encerra): ");
    string voto = Console.ReadLine() ?? "";

    if (voto == "0")
    {
        votacaoAberta = false;
    }
    else if (voto == "1")
    {
        votosAna++;
    }
    else if (voto == "2")
    {
        votosBruno++;
    }
    else
    {
        nulos++;
    }
}

Console.WriteLine($"Ana: {votosAna} | Bruno: {votosBruno} | Nulos: {nulos}");

if (votosAna > votosBruno)
{
    Console.WriteLine("Vencedora: Ana");
}
else if (votosBruno > votosAna)
{
    Console.WriteLine("Vencedor: Bruno");
}
else
{
    Console.WriteLine("Empate");
}
```

Compare: no caminho 1, o case "0" existe só para o 0 não cair no default e virar nulo. No caminho 2, o 0 é testado primeiro e só muda votacaoAberta para `false`. Assim, ele nunca chega ao else dos nulos. No caminho 2, voto pode ser declarada dentro do `while`, porque a condição do laço não usa voto. A variável `bool` de controle também serve quando o laço tem mais de um motivo para parar.

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

#### Caminho 2 — `foreach` nas letras, for com `break` e `string.Equals`

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

Compare: uma `string` é uma sequência de `char`, então o `foreach` passa por cada letra. Um `char` fica entre aspas simples: ' '. O `foreach` com `bool` só diz se o usuário existe. O for com -1 também diz em que posição ele está, e o `break` para a busca no primeiro igual. O else if garante que só a primeira regra quebrada aparece, e que o Add só acontece quando todas passam.

## Questão 3 — Pães da padaria (`while`, Entrada e conversão, Strings, List, for e `foreach`, `decimal`)

**Situação.** Toda sexta à noite, o gerente da Padaria Pão Quente digita quantos pães franceses vendeu em cada dia útil da semana. Às vezes ele erra: aperta uma letra, deixa o campo vazio ou digita um sinal de menos. O programa não pode fechar nem pular o dia quando isso acontece. Ele avisa e pede o mesmo dia de novo. No fim, o gerente quer o total da semana, a média por dia e o dia com mais vendas.

**O que o programa deve fazer.**

- Guardar os dias (Segunda a Sexta) em uma `List<string>` e as quantidades em uma `List<int>`.
- Pedir a quantidade de cada dia com `while`. Só aceitar um texto que não seja vazio e tenha apenas dígitos de 0 a 9. Só então converter com `int.Parse`.
- Com valor inválido, mostrar Digite só números. Tente de novo. e pedir o mesmo dia.
- Mostrar o total, a média com 2 casas decimais e o dia com mais vendas.

**Dois caminhos de solução.**

- Caminho 1: conferir os caracteres com `foreach`. Fazer o resumo com for, guardando a posição do dia com mais vendas.
- Caminho 2: conferir os caracteres com for e `texto[i]`. Fazer o resumo com `foreach` e um contador de posição.

**Dicas para os 2 caminhos:**

- Use `int` dia = 0 como posição do dia atual. O `while (dia < dias.Count)` só termina quando os 5 dias forem preenchidos. Some 1 em dia apenas quando o valor for válido.
- Um caractere é dígito quando está entre '0' e '9'. Então ele é inválido quando letra < '0' || letra > '9'.
- Para a média ter casas decimais, guarde o total em uma variável `decimal`.

**Teste.** Digite em sequência: 120, abc, 95, 150, -10, 110, (vazio), 178.

```text
Segunda - pães vendidos: 120
Terça - pães vendidos: abc
Digite só números. Tente de novo.
Terça - pães vendidos: 95
Quarta - pães vendidos: 150
Quinta - pães vendidos: -10
Digite só números. Tente de novo.
Quinta - pães vendidos: 110
Sexta - pães vendidos:
Digite só números. Tente de novo.
Sexta - pães vendidos: 178
Total da semana: 653 pães
Média por dia: 130,60 pães
Dia com mais vendas: Sexta (178 pães)
```

### Gabarito

#### Caminho 1 — validação com `foreach` e resumo com for

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

#### Caminho 2 — validação com for e resumo com `foreach`

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

Compare: o ponto principal dos 2 caminhos é o dia++ dentro do bloco válido. Com valor inválido, dia não muda, então o `while` pede o mesmo dia de novo. A validação começa com valido = texto != "", que recusa o texto vazio. Depois, qualquer caractere fora de '0' a '9' muda valido para `false`, inclusive letras e o sinal -. Como o texto já foi conferido, o `int.Parse` nunca quebra. O `foreach` dá cada caractere direto. O for usa a posição i e lê o caractere com `texto[i]`. O total é `decimal` para que total / paes.Count mantenha as casas decimais (653 / 5 = 130,60).

## Questão 4 — Boletim da turma (Lista aninhada, for e `foreach`, Entrada e conversão, `decimal`, if/else)

**Situação.** A coordenação precisa fechar o boletim do bimestre. Cada aluno tem 2 notas inteiras, guardadas como texto em uma tabela: Lia (8 e 6), Noah (5 e 4) e Davi (7 e 4). A média é a soma das 2 notas dividida por 2. Média 7 ou mais é Aprovado, de 5 até menos de 7 é Recuperação, menos de 5 é Reprovado.

**O que o programa deve fazer.**

- Guardar os alunos em uma `List<List<string>>`, com os campos [0] nome, [1] nota 1, [2] nota 2.
- Converter as notas com `int.Parse` e calcular a média em `decimal`. Cuidado: divida por 2m, não por 2.
- Mostrar nome | média | situação para cada aluno, com a média em 1 casa decimal.

**Dois caminhos de solução.**

- Caminho 1: `foreach` nas linhas. Cada linha é um aluno, e o campo é lido com 1 índice: `aluno[1]`.
- Caminho 2: for com índice. O campo é lido com 2 índices: `alunos[i][1]`.

**Saída esperada.**

```text
Lia | média 7,0 | Aprovado
Noah | média 4,5 | Reprovado
Davi | média 5,5 | Recuperação
```

### Gabarito

#### Caminho 1 — `foreach`

```csharp
// alunos: [0] nome, [1] nota 1, [2] nota 2
List<List<string>> alunos = new List<List<string>>();
alunos.Add(new List<string> { "Lia", "8", "6" });
alunos.Add(new List<string> { "Noah", "5", "4" });
alunos.Add(new List<string> { "Davi", "7", "4" });

foreach (List<string> aluno in alunos)
{
    int nota1 = int.Parse(aluno[1]);
    int nota2 = int.Parse(aluno[2]);
    decimal media = (nota1 + nota2) / 2m;

    if (media >= 7)
    {
        Console.WriteLine($"{aluno[0]} | média {media:F1} | Aprovado");
    }
    else if (media >= 5)
    {
        Console.WriteLine($"{aluno[0]} | média {media:F1} | Recuperação");
    }
    else
    {
        Console.WriteLine($"{aluno[0]} | média {media:F1} | Reprovado");
    }
}
```

#### Caminho 2 — for com índice

```csharp
// alunos: [0] nome, [1] nota 1, [2] nota 2
List<List<string>> alunos = new List<List<string>>();
alunos.Add(new List<string> { "Lia", "8", "6" });
alunos.Add(new List<string> { "Noah", "5", "4" });
alunos.Add(new List<string> { "Davi", "7", "4" });

for (int i = 0; i < alunos.Count; i++)
{
    int nota1 = int.Parse(alunos[i][1]);
    int nota2 = int.Parse(alunos[i][2]);
    decimal media = (nota1 + nota2) / 2m;

    if (media >= 7)
    {
        Console.WriteLine($"{alunos[i][0]} | média {media:F1} | Aprovado");
    }
    else if (media >= 5)
    {
        Console.WriteLine($"{alunos[i][0]} | média {media:F1} | Recuperação");
    }
    else
    {
        Console.WriteLine($"{alunos[i][0]} | média {media:F1} | Reprovado");
    }
}
```

Compare: no `foreach`, aluno já é a linha, então o campo é `aluno[1]`. No for, a linha é alunos[i], então o campo é `alunos[i][1]`: o primeiro índice escolhe a linha, o segundo escolhe o campo. Se a divisão fosse por 2 (inteiro), Noah teria média 4 em vez de 4,5. F1 mostra 1 casa decimal.
