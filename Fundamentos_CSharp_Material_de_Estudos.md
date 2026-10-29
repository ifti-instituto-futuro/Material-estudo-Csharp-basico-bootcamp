# Fundamentos de C# — Material de Estudos

Atualizado em 29/10/2026

## Como usar este material

Este material ensina os fundamentos de C# para programas de console, em 10 capítulos curtos. Ele é para quem está começando e já sabe usar o terminal e o editor de código.

- Leia os capítulos na ordem. Cada capítulo usa o que o capítulo anterior ensinou.
- Digite cada exemplo e execute. Não copie e cole: digitar fixa a sintaxe.
- Faça o "Pratique" no fim de cada capítulo antes de ir para o próximo.
- No fim, resolva as questões pelos 2 caminhos e marque o checklist de autoavaliação. O gabarito fica no fim do material.

Todos os exemplos foram testados com o .NET 10.

## Capítulo 1 — Ambiente e execução

Um programa de console em C# é criado e executado com 3 comandos do .NET SDK.

```bash
dotnet --version
dotnet new console -n AulaCSharp
cd AulaCSharp
dotnet new gitignore
dotnet run
```

- `dotnet --version` mostra a versão instalada. Se der erro, o SDK não está instalado.
- `dotnet new console -n AulaCSharp` cria a pasta `AulaCSharp` com um projeto de console.
- `cd AulaCSharp` entra na pasta do projeto.
- `dotnet new gitignore` cria o arquivo `.gitignore` na pasta do projeto. Esse arquivo diz ao Git quais arquivos não devem ir para o repositório, como as pastas `bin` e `obj`. O .NET gera essas pastas de novo a cada compilação, então elas não precisam ser versionadas. Rode este comando uma vez, logo depois de criar o projeto.
- `dotnet run` compila o código e executa o programa.

**O arquivo `Program.cs`.** O código fica neste arquivo. Nas versões atuais do .NET, você escreve as instruções direto no arquivo, sem `class` nem `Main`. O programa executa as linhas de cima para baixo.

```csharp
Console.WriteLine("Olá, mundo!");
```

**Compilar e executar.** Compilar é traduzir o código para uma forma que o computador executa. Se o código tem um erro de sintaxe, a compilação falha e o programa não roda.

Exemplo de erro de compilação (falta o `;`):

```text
Program.cs(1,34): error CS1002: ; expected
```

Como ler a mensagem: `(1,34)` é linha 1, coluna 34. `CS1002` é o código do erro. O texto diz o que falta.

**Pratique.** Crie o projeto, troque a mensagem do `WriteLine` e rode de novo. Depois apague um `;`, rode e leia o erro.

## Capítulo 2 — Tipos, variáveis e saída

Uma variável é um nome que guarda um valor. O tipo define que valores cabem nela. Em C#, você declara o tipo antes do nome.

```csharp
string nome = "Lia";
char inicial = 'L';
int idade = 21;
long populacao = 8000000000;
double altura = 1.68;
decimal saldo = 135.75m;
bool matriculada = true;
```

| Tipo | Guarda | Exemplo de valor | Quando usar |
| --- | --- | --- | --- |
| `string` | Texto | `"Lia Souza"` | Nomes, descrições, códigos com letras |
| `char` | Um único caractere | `'L'` | Uma letra ou símbolo |
| `int` | Inteiro até cerca de 2,1 bilhões | `21` | Idade, quantidade, opção de menu |
| `long` | Inteiro maior | `8000000000` | Valores acima de 2,1 bilhões |
| `double` | Número com parte decimal, aproximado | `1.68` | Medidas, cálculos científicos |
| `decimal` | Número com parte decimal, exato | `135.75m` | Dinheiro, preços, porcentagens de desconto |
| `bool` | `true` ou `false` | `true` | Sim/não, encontrado/não encontrado |

**Regras de escrita no código.**

- Texto fica entre aspas duplas: `"Lia"`. Um caractere fica entre aspas simples: `'L'`.
- No código, o separador decimal é o ponto: `1.68`. A vírgula separa itens, não decimais.
- Um `decimal` escrito no código precisa do sufixo `m`: `135.75m`. Sem o `m`, o C# entende `double` e dá erro de compilação.
- C# diferencia maiúsculas de minúsculas. `nome` e `Nome` são variáveis diferentes.

**Por que `decimal` para dinheiro.** O `double` guarda uma aproximação do número. Por isso, `0.1 + 0.2` em `double` dá `0.30000000000000004`. Em `decimal`, `0.1m + 0.2m` dá exatamente `0.3`.

**Mostrar valores no console.**

```csharp
Console.WriteLine("Pula linha no fim.");
Console.Write("Não pula linha. ");
Console.WriteLine($"{nome} tem {idade} anos.");
```

O `$` antes das aspas ativa a interpolação. Tudo que está entre `{ }` é trocado pelo valor da variável. A saída é `Lia tem 21 anos.`

Entre as `{ }` também cabe uma operação. O C# calcula o resultado e coloca o valor no texto.

```csharp
int a = 3;
int b = 4;
Console.WriteLine($"Soma: {1 + 1}");           // Soma: 2
Console.WriteLine($"{a} + {b} = {a + b}");    // 3 + 4 = 7
```

**Pratique.** Para cada dado, escolha o tipo e diga o motivo: nome de uma cidade, número de alunos de uma turma, preço de um livro, a letra de uma turma, se um aluno está ativo. Depois declare as 5 variáveis e mostre todas em uma frase com interpolação.

## Capítulo 3 — Entrada de dados e conversão

`Console.ReadLine()` sempre devolve texto. Para calcular com o valor digitado, você converte o texto para um tipo numérico.

**Ler um texto.**

```csharp
Console.Write("Digite seu nome: ");
string nome = Console.ReadLine() ?? "";
```

O `?? ""` diz: se `ReadLine` não devolver nada (`null`), use texto vazio. Assim a variável nunca fica `null`, e o compilador não mostra aviso.

**Converter com `Parse`.**

```csharp
int numero = int.Parse("42");
double medida = double.Parse("1,75");
decimal preco = decimal.Parse("135,75");
```

Escolha o `Parse` do tipo que você precisa: `int.Parse`, `double.Parse` ou `decimal.Parse`.

Se o texto não representa um número, o `Parse` gera um erro em tempo de execução e o programa termina:

```text
Unhandled exception. System.FormatException: The input string 'dezoito' was not in a correct format.
```

**Converter sem quebrar o programa com `TryParse`.** O `TryParse` tenta converter. Ele devolve `true` se conseguiu e `false` se não conseguiu. O número convertido vai para a variável depois de `out`.

```csharp
Console.Write("Digite sua idade: ");
string texto = Console.ReadLine() ?? "";

if (int.TryParse(texto, out int idade))
{
    Console.WriteLine($"Ano que vem você terá {idade + 1} anos.");
}
else
{
    Console.WriteLine("Digite um número válido para continuar.");
}
```

| Entrada | `int.Parse` | `int.TryParse` |
| --- | --- | --- |
| `"19"` | Devolve `19` | Devolve `true`, `idade` = `19` |
| `"dezoito"` | Erro, o programa termina | Devolve `false`, o programa continua |
| `""` (vazio) | Erro, o programa termina | Devolve `false`, o programa continua |

**Alternativa sem conversão.** Se o número só serve para escolher uma opção (1, 2, 3), você não precisa convertê-lo. Compare o texto direto, com `switch` ou `==`. Um texto inválido cai no caso "opção inválida" e nada quebra. O Capítulo 4 mostra como.

**Cultura: vírgula ou ponto.** `Parse` e `TryParse` usam a configuração regional do computador. Em português do Brasil, a vírgula separa decimais e o ponto separa milhares.

| Texto digitado | Resultado em pt-BR |
| --- | --- |
| `10,5` | `10,5` |
| `10.5` | `105` (o ponto foi lido como separador de milhar) |

Resumo: no código você escreve `10.5m`. O usuário digita `10,5`.

**Pratique.**

1. Leia um número inteiro com `int.Parse` e mostre o dobro.
2. Troque para `int.TryParse` e mostre uma mensagem quando o texto for inválido.
3. Leia um preço com `decimal.TryParse`. Teste `10,5` e `10.5` e compare os resultados.

## Capítulo 4 — Operadores, if/else e switch

Operadores calculam e comparam valores. `if/else` e `switch` usam o resultado para escolher qual código executar.

**Operadores aritméticos.**

| Operador | Faz | Exemplo | Resultado |
| --- | --- | --- | --- |
| `+` | Soma | `7 + 2` | `9` |
| `-` | Subtração | `7 - 2` | `5` |
| `*` | Multiplicação | `7 * 2` | `14` |
| `/` | Divisão | `7 / 2` | `3` (entre `int`, a parte decimal é descartada) |
| `/` | Divisão | `7m / 2` | `3.5` (com `decimal`, a parte decimal fica) |
| `%` | Resto da divisão | `7 % 2` | `1` |

Use `%` para saber se um número é par: `numero % 2 == 0`.

**Operadores de comparação.** Eles sempre devolvem `bool`.

| Operador | Pergunta | Exemplo verdadeiro |
| --- | --- | --- |
| `==` | É igual? | `5 == 5` |
| `!=` | É diferente? | `5 != 3` |
| `>` / `<` | É maior? / É menor? | `5 > 3` |
| `>=` / `<=` | É maior ou igual? / É menor ou igual? | `5 >= 5` |

Atenção: `=` guarda um valor na variável. `==` compara dois valores.

**Operadores lógicos.** Eles juntam condições.

- `&&` (e): verdadeiro só se as duas condições são verdadeiras.
- `||` (ou): verdadeiro se pelo menos uma condição é verdadeira.
- `!` (não): inverte o valor. `!encontrado` é verdadeiro quando `encontrado` é `false`.

```csharp
int idade = 20;
bool temIngresso = true;
bool podeEntrar = idade >= 18 && temIngresso;   // true
```

**if, else if, else.** O programa testa as condições de cima para baixo. Ele executa o primeiro bloco com condição verdadeira e ignora o resto.

```csharp
int nota = 7;

if (nota >= 9)
{
    Console.WriteLine("Excelente");
}
else if (nota >= 6)
{
    Console.WriteLine("Aprovado");
}
else
{
    Console.WriteLine("Reprovado");
}
```

A ordem importa. Se `nota >= 6` viesse primeiro, uma nota 10 mostraria "Aprovado".

**Validar e sair cedo.** Quando uma entrada é inválida, mostre a mensagem e não faça o resto. Isso evita alterar dados com um valor errado.

```csharp
if (texto.Length < 3)
{
    Console.WriteLine("O texto precisa ter pelo menos 3 caracteres.");
}
else
{
    // só aqui o valor é usado
}
```

**switch.** Use `switch` quando uma variável tem várias opções fixas. Cada `case` é uma opção. O `default` pega qualquer outro valor. O `break` encerra o `case`.

```csharp
Console.Write("Operação (+, - ou *): ");
string operacao = Console.ReadLine() ?? "";
int a = 8, b = 3;

switch (operacao)
{
    case "+":
        Console.WriteLine(a + b);
        break;
    case "-":
        Console.WriteLine(a - b);
        break;
    case "*":
        Console.WriteLine(a * b);
        break;
    default:
        Console.WriteLine("Operação inválida.");
        break;
}
```

**switch para traduzir um código em valores.** Um padrão comum: o usuário digita um código, e o `switch` define o nome e o valor correspondentes. Uma variável `bool` marca se o código era válido.

```csharp
Console.Write("Tamanho (1, 2 ou 3): ");
string codigo = Console.ReadLine() ?? "";

string tamanho = "";
decimal preco = 0m;
bool codigoValido = true;

switch (codigo)
{
    case "1": tamanho = "Pequeno"; preco = 12.00m; break;
    case "2": tamanho = "Médio";   preco = 18.00m; break;
    case "3": tamanho = "Grande";  preco = 24.00m; break;
    default:  codigoValido = false; break;
}

if (codigoValido)
{
    Console.WriteLine($"{tamanho}: R$ {preco:F2}");
}
else
{
    Console.WriteLine("Código inválido.");
}
```

O `switch` compara texto com texto. Se a pessoa digitar `abc`, o valor cai no `default` e o programa continua. Não há `Parse`, então não há erro de conversão.

**Pratique.**

1. Acrescente a divisão ao `switch` da calculadora. Mostre uma mensagem se `b` for zero.
2. Leia um número e mostre se ele é positivo, negativo ou zero.
3. Leia um código de 1 a 3 que representa um tipo de ingresso (inteira, meia, cortesia) e mostre o nome e o preço.

## Capítulo 5 — while e menu repetido

O `while` repete um bloco enquanto a condição é verdadeira. Ele testa a condição antes de cada repetição.

```csharp
int contador = 1;

while (contador <= 3)
{
    Console.WriteLine($"Volta {contador}");
    contador++;   // o mesmo que contador = contador + 1
}
```

Saída: `Volta 1`, `Volta 2`, `Volta 3`. Se você esquecer o `contador++`, a condição nunca fica falsa e o laço não termina (laço infinito). Para parar o programa no terminal, use `Ctrl + C`.

**do-while.** O `do-while` testa a condição depois do bloco. Por isso, o bloco executa pelo menos 1 vez.

```csharp
string resposta;
do
{
    Console.Write("Digite 'sair' para terminar: ");
    resposta = Console.ReadLine() ?? "";
} while (resposta != "sair");
```

**Menu com while e switch.** Este é o esqueleto de quase todo programa de console com opções. O menu aparece, a pessoa escolhe, o programa executa a ação e volta ao menu. O programa só termina quando a pessoa escolhe `0`.

```csharp
string opcao = "";

while (opcao != "0")
{
    Console.WriteLine();
    Console.WriteLine("=== Menu ===");
    Console.WriteLine("1 - Cadastrar");
    Console.WriteLine("2 - Listar");
    Console.WriteLine("0 - Sair");
    Console.Write("Escolha uma opção: ");

    opcao = Console.ReadLine() ?? "";

    switch (opcao)
    {
        case "1":
            Console.WriteLine("Cadastrar selecionado.");
            break;
        case "2":
            Console.WriteLine("Listar selecionado.");
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

O fluxo, passo a passo:

1. `opcao` começa vazia. A condição `opcao != "0"` é verdadeira, então o laço começa.
2. O programa mostra o menu e lê a escolha.
3. O `switch` executa o `case` da escolha. Uma escolha desconhecida, como `9` ou `abc`, cai no `default`.
4. O bloco termina. O `while` testa a condição de novo.
5. Se a escolha foi `0`, a condição fica falsa e o laço termina.

O `break` dentro do `switch` encerra só o `case`. Ele não encerra o `while`.

**Organizar cada opção.** Quando o código de uma opção fica grande, o menu fica difícil de ler. Nesta fase, mantenha cada `case` curto e coloque comentários que separam as partes. Um bloco `{ }` dentro do `case` permite declarar variáveis locais sem conflito de nomes:

```csharp
case "1":
{
    Console.Write("Nome: ");
    string nome = (Console.ReadLine() ?? "").Trim();
    // ... valida e guarda
    break;
}
```

**Pratique.**

1. Mostre os números de 10 até 1 com `while`.
2. Monte um menu com 3 opções e a opção 0. Teste cada opção, uma opção inválida, uma letra e o 0.
3. Faça o programa contar quantas opções válidas a pessoa escolheu e mostre o total ao sair.

## Capítulo 6 — Trabalhar com texto

O texto digitado quase nunca chega limpo. Antes de guardar ou comparar um texto, remova os espaços extras e padronize as letras.

**Métodos de string mais usados.** Um método de string devolve um texto novo. O texto original não muda.

| Método ou propriedade | Faz | Exemplo | Resultado |
| --- | --- | --- | --- |
| `Trim()` | Remove espaços no início e no fim | `"  Lia Souza ".Trim()` | `"Lia Souza"` |
| `Length` | Conta os caracteres | `"Lia Souza".Length` | `9` |
| `ToLower()` | Converte para minúsculas | `"LIA".ToLower()` | `"lia"` |
| `ToUpper()` | Converte para maiúsculas | `"lia".ToUpper()` | `"LIA"` |
| `Contains(x)` | Verifica se contém o trecho | `"Lia Souza".Contains("Sou")` | `true` |
| `Replace(a, b)` | Troca um trecho por outro | `"Lia Souza".Replace(" ", "")` | `"LiaSouza"` |
| `[i]` | Pega o caractere na posição `i` | `"Lia"[0]` | `'L'` |
| `string.IsNullOrWhiteSpace(x)` | Verifica se está vazio ou só tem espaços | `string.IsNullOrWhiteSpace("   ")` | `true` |

`Length` é uma propriedade, não um método. Por isso não tem parênteses.

**Erro comum: esquecer de guardar o resultado.**

```csharp
string nome = "  Lia  ";
nome.Trim();             // o resultado é descartado; nome continua "  Lia  "
nome = nome.Trim();      // correto: nome agora é "Lia"
```

**Limpar na leitura.** Você pode limpar o texto na mesma linha em que lê:

```csharp
string nome = (Console.ReadLine() ?? "").Trim();
```

**Validar o tamanho mínimo.** Faça o `Trim()` antes de contar. Assim, `"  a  "` conta 1 caractere, não 5.

```csharp
if (nome.Length < 3)
{
    Console.WriteLine("O nome precisa ter pelo menos 3 caracteres.");
}
```

**Comparar sem diferenciar maiúsculas de minúsculas.** Para o C#, `"Lia" == "lia"` é `false`. Para comparar sem diferenciar, converta os dois lados para minúsculas:

```csharp
string digitado = "  LIA souza ";
string guardado = "Lia Souza";

bool iguais = digitado.Trim().ToLower() == guardado.Trim().ToLower();   // true
```

A forma completa do C# faz o mesmo sem criar textos novos:

```csharp
bool iguais = string.Equals(digitado.Trim(), guardado, StringComparison.OrdinalIgnoreCase);
```

As duas formas funcionam. Escolha uma e use sempre a mesma no programa.

**Acentos.** `ToLower()` não remove acentos. `"Básico".ToLower()` é `"básico"`, que é diferente de `"basico"`. Quando a entrada tem opções com acento, é mais seguro pedir um código numérico (1, 2, 3) e usar `switch`, como no Capítulo 4.

**Pratique.**

1. Leia um nome, remova os espaços extras e mostre quantos caracteres ele tem.
2. Recuse nomes com menos de 3 caracteres.
3. Leia dois nomes e diga se são iguais, sem diferenciar maiúsculas de minúsculas. Teste `"Ana"` com `"  ANA "`.

## Capítulo 7 — List: guardar vários valores

Uma `List` guarda vários valores do mesmo tipo, em ordem. Ela cresce e diminui enquanto o programa roda. A primeira posição é o índice `0`.

```csharp
List<string> nomes = new List<string>();
nomes.Add("Lia");
nomes.Add("Noah");
nomes.Add("Davi");

Console.WriteLine(nomes[0]);      // Lia
Console.WriteLine(nomes.Count);   // 3
```

**Operações principais.** Os exemplos partem da lista `["Lia", "Noah", "Davi"]`.

| Operação | Faz | Exemplo | Lista depois |
| --- | --- | --- | --- |
| `Add(x)` | Acrescenta no fim | `nomes.Add("Eva")` | `Lia, Noah, Davi, Eva` |
| `Count` | Conta os itens | `nomes.Count` | (devolve `3`) |
| `[i]` | Lê ou troca o item na posição `i` | `nomes[1] = "Noa"` | `Lia, Noa, Davi` |
| `Insert(i, x)` | Insere na posição `i` | `nomes.Insert(0, "Ana")` | `Ana, Lia, Noah, Davi` |
| `RemoveAt(i)` | Remove o item da posição `i` | `nomes.RemoveAt(0)` | `Noah, Davi` |
| `Remove(x)` | Remove a primeira ocorrência de `x` | `nomes.Remove("Davi")` | `Lia, Noah` |
| `Contains(x)` | Verifica se `x` está na lista | `nomes.Contains("Lia")` | (devolve `true`) |
| `Clear()` | Remove todos os itens | `nomes.Clear()` | vazia |

Com `Count` itens, os índices válidos vão de `0` até `Count - 1`. Um índice fora disso gera o erro `ArgumentOutOfRangeException`.

**Percorrer com foreach.** Use `foreach` quando você só precisa ler cada item.

```csharp
foreach (string nome in nomes)
{
    Console.WriteLine(nome);
}
```

**Percorrer com for.** Use `for` quando você precisa da posição. Para mostrar posições a partir de 1, some 1 ao índice.

```csharp
for (int i = 0; i < nomes.Count; i++)
{
    Console.WriteLine($"{i + 1} {nomes[i]}");
}
```

Aqui o `for` e o `foreach` aparecem só no básico, para percorrer uma lista. O Capítulo 9 explica a sintaxe dos dois em detalhe: o que cada parte faz e quando usar cada um.

**Lista vazia.** Antes de mostrar ou acessar itens, confira se a lista tem algum item.

```csharp
if (nomes.Count == 0)
{
    Console.WriteLine("A lista está vazia.");
}
```

**A lista como ordem de chegada.** Uma `List` pode representar uma ordem de atendimento. Esta regra se chama FIFO (*first in, first out*): o primeiro que entra é o primeiro que sai. Exemplo com documentos que esperam para imprimir:

| Ação | Código | Efeito |
| --- | --- | --- |
| Entrar no fim | `impressao.Add("relatorio.pdf")` | O item fica na última posição |
| Ver o próximo | `impressao[0]` | Lê o primeiro, sem remover |
| Tirar o próximo | `impressao.RemoveAt(0)` | Remove o primeiro; os outros sobem 1 posição |

```csharp
List<string> impressao = new List<string>();
impressao.Add("relatorio.pdf");
impressao.Add("foto.png");
impressao.Add("relatorio.pdf");   // o mesmo valor pode aparecer de novo

if (impressao.Count == 0)
{
    Console.WriteLine("Nada para imprimir.");
}
else
{
    string proximo = impressao[0];   // 1. lê o primeiro
    impressao.RemoveAt(0);           // 2. remove o primeiro
    Console.WriteLine($"Imprimindo {proximo}. Restam {impressao.Count}.");
}
```

Saída: `Imprimindo relatorio.pdf. Restam 2.`

Dois cuidados:

- Leia o item **antes** do `RemoveAt(0)`. Depois de remover, `impressao[0]` já é o próximo item.
- Só remova quando a ação deu certo. Se uma validação falhar, não chame `RemoveAt`. Assim o item continua na primeira posição.

O C# também tem a coleção `Queue<T>`, feita só para filas. A `List` é suficiente aqui e permite listar com posição.

**Pratique.**

1. Crie uma lista com 3 cidades e mostre a segunda.
2. Mostre todas as cidades numeradas a partir de 1.
3. Simule uma ordem de chegada: acrescente 3 nomes, atenda 2 (mostre e remova o primeiro) e mostre quem sobrou.

## Capítulo 8 — Listas aninhadas: linhas e campos

Uma lista aninhada é uma lista em que cada item também é uma lista. Pense nela como uma tabela: a lista externa guarda as linhas, e cada lista interna guarda os campos de uma linha.

```csharp
List<List<string>> livros = new List<List<string>>();
livros.Add(new List<string> { "Dom Casmurro", "Machado de Assis", "Romance" });
livros.Add(new List<string> { "O Cortiço", "Aluísio Azevedo", "Naturalismo" });
```

A tabela que essa lista representa:

| Linha | Campo `[0]` — título | Campo `[1]` — autor | Campo `[2]` — gênero |
| --- | --- | --- | --- |
| `livros[0]` | Dom Casmurro | Machado de Assis | Romance |
| `livros[1]` | O Cortiço | Aluísio Azevedo | Naturalismo |

**Ler e alterar um campo.** O primeiro índice escolhe a linha. O segundo índice escolhe o campo dentro da linha.

```csharp
Console.WriteLine(livros[0][0]);   // Dom Casmurro
Console.WriteLine(livros[1][1]);   // Aluísio Azevedo
livros[0][2] = "Realismo";         // troca o gênero da primeira linha
```

**Contar.**

- `livros.Count` conta as linhas. Aqui, `2`.
- `livros[0].Count` conta os campos da linha 0. Aqui, `3`.

**Montar uma linha com dados digitados.** Crie a lista interna, preencha os campos na ordem certa e acrescente a linha na lista externa.

```csharp
List<string> novoLivro = new List<string>();
novoLivro.Add(titulo);    // campo 0
novoLivro.Add(autor);     // campo 1
novoLivro.Add(genero);    // campo 2
livros.Add(novoLivro);
```

**A regra mais importante: a ordem dos campos.** Todas as linhas precisam ter os campos na mesma ordem. Se uma linha guarda o autor no campo 0 e outra guarda o título no campo 0, as buscas e as listagens ficam erradas. Escreva um comentário no topo do programa com o significado de cada campo:

```csharp
// livros: [0] título, [1] autor, [2] gênero
```

**Números dentro da lista.** Uma `List<string>` só guarda texto. Você tem duas opções para um valor numérico:

1. Guardar uma informação que leva ao número e calcular o número quando precisar. Exemplo: guardar a categoria `"Romance"` e usar um `switch` para achar o preço da categoria.
2. Guardar o número como texto e converter na hora de calcular: `decimal.Parse(produtos[0][1])`. Guarde o texto no formato da cultura do computador (por exemplo, `"15,90"` em pt-BR). Senão, a conversão dá erro ou um valor errado (Capítulo 3).

A opção 1 é mais segura, porque não depende da cultura.

**Pratique.**

1. Desenhe no papel uma tabela com 2 linhas e 3 campos. Numere os índices de cada célula.
2. Crie essa tabela como `List<List<string>>`.
3. Mostre o segundo campo da primeira linha e altere o terceiro campo da segunda linha.
4. Acesse `livros[2]` em uma lista de 2 linhas. Leia o erro e corrija o índice.

## Capítulo 9 — Percorrer, buscar e atualizar

Quase toda operação com uma lista de registros segue 3 padrões: percorrer todas as linhas, buscar uma linha e atualizar ou remover a linha encontrada.

Antes dos padrões, veja em detalhe como o `for` e o `foreach` funcionam.

### A sintaxe do for

O `for` repete um bloco usando um contador. Ele recebe 3 partes entre parênteses, separadas por `;`.

```csharp
for (inicialização; condição; passo)
{
    // corpo: o código que repete
}
```

| Parte | Exemplo | Quando executa | O que faz |
| --- | --- | --- | --- |
| Inicialização | `int i = 0` | Uma vez, antes da primeira volta | Cria o contador e dá o valor inicial |
| Condição | `i < 3` | Antes de cada volta | Se for `true`, executa o corpo. Se for `false`, o `for` termina |
| Passo | `i++` | No fim de cada volta | Muda o contador. `i++` soma 1 |

**Passo a passo.** Este `for` mostra 0, 1 e 2:

```csharp
for (int i = 0; i < 3; i++)
{
    Console.WriteLine(i);
}
```

| Momento | Valor de `i` | `i < 3`? | O que acontece |
| --- | --- | --- | --- |
| Início | 0 | sim | Mostra `0`. O passo faz `i` valer 1 |
| Volta 2 | 1 | sim | Mostra `1`. O passo faz `i` valer 2 |
| Volta 3 | 2 | sim | Mostra `2`. O passo faz `i` valer 3 |
| Fim | 3 | não | O `for` termina sem executar o corpo |

**Variações.** Mudando as 3 partes, o mesmo `for` faz contagens diferentes.

| Objetivo | Código | Saída |
| --- | --- | --- |
| Contar de trás para frente | `for (int i = 5; i >= 1; i--)` | 5 4 3 2 1 |
| Contar de 2 em 2 | `for (int i = 0; i <= 10; i += 2)` | 0 2 4 6 8 10 |
| Percorrer uma lista | `for (int i = 0; i < lista.Count; i++)` | Uma volta por item, com `i` de 0 até `Count - 1` |

`i--` diminui 1. `i += 2` é o mesmo que `i = i + 2`.

**Cuidados com o for.**

- Para percorrer uma lista, use `i < lista.Count`. Com `i <= lista.Count`, a última volta acessa uma posição que não existe e gera `ArgumentOutOfRangeException`.
- Se o passo nunca leva a condição a `false`, o laço não termina.
- O contador só existe dentro do `for`. Usar `i` depois do bloco dá o erro `CS0103: The name 'i' does not exist in the current context`.

### A sintaxe do foreach

O `foreach` passa por cada item de uma coleção, do primeiro ao último. Ele não usa contador.

```csharp
foreach (tipo nomeDoItem in colecao)
{
    // corpo: usa nomeDoItem
}
```

| Parte | Exemplo | O que significa |
| --- | --- | --- |
| Tipo | `string` | O tipo de cada item. Precisa combinar com a coleção |
| Nome do item | `fruta` | Uma variável que você escolhe. A cada volta, ela recebe o próximo item |
| `in` | `in` | Palavra fixa: "em" |
| Coleção | `frutas` | A lista ou o texto que será percorrido |

```csharp
List<string> frutas = new List<string> { "Maçã", "Banana", "Uva" };

foreach (string fruta in frutas)
{
    Console.WriteLine(fruta);
}
```

Na 1ª volta, `fruta` vale `"Maçã"`. Na 2ª, `"Banana"`. Na 3ª, `"Uva"`. Depois do último item, o `foreach` termina sozinho.

**Qual tipo usar.** O tipo do item depende da coleção:

| Coleção | Cada item é | foreach |
| --- | --- | --- |
| `List<string>` | um texto | `foreach (string nome in nomes)` |
| `List<int>` | um número inteiro | `foreach (int quantidade in quantidades)` |
| `List<List<string>>` | uma linha (uma lista) | `foreach (List<string> linha in tabela)` |
| `string` | um caractere | `foreach (char letra in texto)` |

Use um nome no singular para o item e no plural para a coleção: `fruta` em `frutas`. Assim, o código se lê como uma frase.

**Cuidados com o foreach.**

- A variável do item é só para leitura. `fruta = "Uva";` dentro do `foreach` dá o erro `CS1656: Cannot assign to 'fruta' because it is a 'foreach iteration variable'`.
- Não acrescente nem remova itens da lista dentro do `foreach`. O programa termina com `InvalidOperationException: Collection was modified`.
- O `foreach` não dá a posição do item. Se você precisar dela, use `for` ou crie um contador manual.

### for ou foreach?

| Situação | Use |
| --- | --- |
| Só ler cada item da lista | `foreach` |
| Mostrar a posição (1, 2, 3...) | `for` |
| Alterar ou remover o item encontrado | `for`, porque você precisa do índice |
| Repetir um número fixo de vezes, sem lista | `for` |
| Percorrer as letras de um texto | Os dois funcionam: `foreach (char letra in texto)` ou `for` com `texto[i]` |

### Padrões com listas

**Percorrer todas as linhas e todos os campos.** O `foreach` externo passa por cada linha. O `foreach` interno passa por cada campo da linha atual.

```csharp
foreach (List<string> linha in livros)
{
    foreach (string campo in linha)
    {
        Console.Write(campo + " | ");
    }
    Console.WriteLine();
}
```

**Percorrer e mostrar campos escolhidos.** Normalmente você sabe quais campos quer mostrar. Então basta um `foreach`:

```csharp
foreach (List<string> livro in livros)
{
    Console.WriteLine($"{livro[0]} | {livro[1]} | {livro[2]}");
}
```

**Buscar uma linha pela posição.** Use `for`, porque você precisa saber em que posição a linha está. Comece com `-1`, que significa "não encontrado". O `break` para o `for` quando a linha é encontrada.

```csharp
string busca = "  o cortiço ";
int posicaoEncontrada = -1;

for (int i = 0; i < livros.Count; i++)
{
    if (livros[i][0].ToLower() == busca.Trim().ToLower())
    {
        posicaoEncontrada = i;
        break;
    }
}

if (posicaoEncontrada == -1)
{
    Console.WriteLine("Livro não encontrado.");
}
else
{
    Console.WriteLine($"Autor: {livros[posicaoEncontrada][1]}");
}
```

Aqui o `break` está dentro de um `for`, não de um `switch`. Por isso ele encerra o `for`.

**Verificar se já existe.** Quando você só precisa de sim ou não, use uma variável `bool`:

```csharp
bool jaExiste = false;

foreach (List<string> livro in livros)
{
    if (livro[0].ToLower() == tituloNovo.Trim().ToLower())
    {
        jaExiste = true;
    }
}

if (jaExiste)
{
    Console.WriteLine("Este título já está cadastrado.");
}
else
{
    // só aqui a nova linha é acrescentada
}
```

Este padrão impede registros repetidos. A comparação com `Trim()` e `ToLower()` faz `"  IRACEMA "` ser igual a `"Iracema"`.

**Atualizar ou remover a linha encontrada.** Use a posição encontrada pela busca.

```csharp
livros[posicaoEncontrada][2] = "Clássico";   // atualiza um campo
livros.RemoveAt(posicaoEncontrada);         // remove a linha inteira
```

Só use a posição quando ela for diferente de `-1`. Com `-1`, o C# gera erro de índice.

**Buscar em uma lista e usar o resultado em outra.** Um programa pode ter mais de uma lista. Exemplo: uma lista de livros e uma lista de empréstimos que guarda só os títulos. Para mostrar o autor de um empréstimo, pegue o título na lista de empréstimos e busque esse título na lista de livros, com o mesmo `for` acima.

**Pratique.**

1. Mostre todos os livros com os dois `foreach`.
2. Leia um título e mostre o autor. Se não existir, mostre "Livro não encontrado."
3. Antes de cadastrar um livro, recuse o título se ele já existir, sem diferenciar maiúsculas de minúsculas.
4. Crie uma lista de empréstimos (`List<string>` com títulos). Mostre cada empréstimo com o autor do livro.

## Capítulo 10 — Cálculos com decimal, porcentagem e formatação

Para aplicar um desconto percentual, calcule o valor do desconto e subtraia do preço. Use `decimal` em todos os valores de dinheiro e mostre o resultado com 2 casas decimais.

**A fórmula.**

```latex
\text{valor final} = \text{preço} - \text{preço} \times \frac{\text{percentual}}{100}
```

Exemplo: um produto de R$ 80,00 com 15% de desconto. O desconto é 80 × 15 / 100 = 12. O valor final é 80 − 12 = R$ 68,00.

```csharp
decimal precoBase = 80.00m;
decimal percentual = 15m;

decimal desconto = precoBase * percentual / 100;
decimal valorFinal = precoBase - desconto;

Console.WriteLine($"Valor: R$ {valorFinal:F2}");   // Valor: R$ 68,00
```

**Duas formas de guardar a porcentagem.** As duas dão o mesmo resultado. Escolha uma e use sempre a mesma.

| Forma | Valor guardado para 15% | Cálculo | Para mostrar |
| --- | --- | --- | --- |
| Número inteiro | `15m` | `precoBase * percentual / 100` | `$"{percentual}%"` → `15%` |
| Fração | `0.15m` | `precoBase * taxa` | `$"{taxa:P0}"` → `15%` |

**Armadilha: divisão entre inteiros.** Se o percentual for `int`, `15 / 100` dá `0`, porque a divisão entre inteiros descarta a parte decimal. O desconto fica zero sem nenhum erro.

```csharp
int pct = 15;
Console.WriteLine(80 * (pct / 100));    // 0  — errado
Console.WriteLine(80m * pct / 100);     // 12 — correto: 80m é decimal
```

Regra prática: em cálculos de dinheiro, garanta que o primeiro valor da conta é `decimal`.

**Mostrar com 2 casas decimais.** O formato `F2` dentro das chaves mostra sempre 2 casas.

| Valor | `{valor:F2}` em pt-BR |
| --- | --- |
| `12m` | `12,00` |
| `12.5m` | `12,50` |
| `12.345m` | `12,35` |

`F2` só muda a apresentação. O valor guardado na variável continua o mesmo.

**Vírgula ou ponto na saída.** Assim como o `Parse`, o `F2` usa a cultura do computador. Em pt-BR, `68.00m` aparece como `68,00`. Em um computador em inglês (en-US), aparece como `68.00`.

Para garantir a vírgula em qualquer computador, defina a cultura no início do programa:

```csharp
using System.Globalization;

CultureInfo.CurrentCulture = new CultureInfo("pt-BR");
```

O `using` fica na primeira linha do arquivo. A linha do `CultureInfo` fica antes de qualquer leitura ou saída de números. Ela também faz o `Parse` aceitar a vírgula.

Existe também o formato `C` (moeda): `{valor:C}` mostra `R$ 68,00` em pt-BR. Escrever `R$ {valor:F2}` dá mais controle sobre o texto exato.

**Pratique.**

1. Calcule o valor final de R$ 40,00 com 10% e com 20% de desconto. Confira: R$ 36,00 e R$ 32,00.
2. Calcule R$ 25,00 com 10% de desconto. Confira: R$ 22,50.
3. Faça o cálculo com o percentual em `int` e veja o desconto virar zero. Depois corrija com `m`.
4. Mude a cultura para `"en-US"` e veja a mudança na saída.

## Erros comuns e como corrigir

A maioria dos erros de quem começa em C# se repete. Use esta tabela quando o programa não compila ou dá um resultado estranho.

| Sintoma | Causa provável | Correção |
| --- | --- | --- |
| `error CS1002: ; expected` | Falta `;` no fim da linha | Leia a linha e a coluna da mensagem e acrescente o `;` |
| `error CS0103: The name 'x' does not exist` | Nome digitado errado, ou variável declarada dentro de outro bloco `{ }` | Confira maiúsculas e minúsculas. Declare a variável fora do bloco se ela for usada fora dele |
| `error CS0664` ao escrever `135.75` | `decimal` sem o sufixo `m` | Escreva `135.75m` |
| `FormatException` e o programa termina | `Parse` recebeu um texto que não é número | Use `TryParse` ou compare o texto com `switch` |
| `ArgumentOutOfRangeException` | Índice menor que 0 ou maior que `Count - 1` | Confira `Count` antes de acessar. Lembre que o primeiro índice é 0 |
| O menu nunca para (laço infinito) | A variável da condição do `while` nunca muda | Leia a opção de novo dentro do laço |
| `"Ana"` não é encontrado quando a pessoa digita `"ana "` | Comparação sem `Trim()` e sem `ToLower()` | Limpe e padronize os dois lados antes de comparar |
| `nome.Trim();` não muda o nome | O resultado do método foi descartado | Escreva `nome = nome.Trim();` |
| Desconto sempre zero | Divisão entre inteiros, como `15 / 100` | Use `decimal`: `15m / 100` |
| `10.5` digitado vira `105` | Em pt-BR, o ponto é separador de milhar | Digite `10,5`. Defina a cultura `pt-BR` no programa |
| Item sai da lista mesmo com entrada inválida | `RemoveAt` foi chamado antes da validação | Valide primeiro. Chame `RemoveAt` só quando tudo deu certo |
| Mostra o item errado depois de remover | O item foi lido depois do `RemoveAt(0)` | Guarde `lista[0]` em uma variável antes de remover |
| A opção `0` mostra também "Opção inválida" | Falta `case "0":` no `switch` | Crie o `case "0"` com a mensagem de saída |

**Como ler um erro de execução.** Procure a linha que começa com `at Program` e tem `Program.cs:line N`. O número `N` é a linha do seu código que causou o erro.

## Exercícios

Cada questão junta vários capítulos e tem 2 caminhos de solução. Os conceitos que a questão treina estão no título, entre parênteses. Resolva pelo caminho 1, depois pelo caminho 2. A saída no console deve ser a mesma nos dois. As respostas ficam no **Gabarito**, no fim do material.

| Nível | Questões | Conceitos por questão | Tamanho da resposta |
| --- | --- | --- | --- |
| 1 | 1 a 4 | 3 a 5 | 15 a 45 linhas |
| 2 | 5 a 8 | 5 a 7 | 25 a 110 linhas |
| 3 (opcional) | Programas A, B e C | 6 ou mais | 50 a 90 linhas |

Como estudar cada questão:

1. Leia a situação e liste os dados que o programa recebe e o que ele mostra.
2. Releia os capítulos dos conceitos do título, se precisar.
3. Resolva pelo caminho 1. Execute todos os testes da tabela.
4. Resolva pelo caminho 2. Os testes devem dar a mesma saída.
5. Responda: qual caminho ficou mais fácil de ler? Depois confira no gabarito.

### Nível 1

#### Questão 1 — Eleição do representante de turma (Tipagem, Operadores, while, switch, if/else)

**Situação.** A turma do 3º ano B vai eleger seu representante. As candidatas são Ana (número 1) e Bruno (número 2). O computador da sala fica aberto e cada aluno digita seu voto, um por vez. Qualquer valor diferente de 1 ou 2, inclusive letras, conta como voto nulo. Quando a professora digita 0, a votação termina e o programa mostra o resultado.

**O que o programa deve fazer.**

- Repetir a leitura de votos até alguém digitar `0`. O `0` não conta como voto.
- Contar os votos de Ana, de Bruno e os nulos em 3 variáveis `int`.
- No fim, mostrar a contagem e o vencedor, ou `Empate`.

**Dois caminhos de solução.**

- **Caminho 1:** `while` que testa o voto na condição (`while (voto != "0")`) e `switch` para contar o voto.
- **Caminho 2:** `while` controlado por uma variável `bool` (`while (votacaoAberta)`) e `if / else if` para contar o voto. Quando alguém digita `0`, a variável passa a ser `false` e o laço termina.

**Testes.**

| Votos digitados | Saída esperada |
| --- | --- |
| 1, 2, 1, x, 0 | `Ana: 2 \| Bruno: 1 \| Nulos: 1` e `Vencedora: Ana` |
| 1, 2, 0 | `Ana: 1 \| Bruno: 1 \| Nulos: 0` e `Empate` |

#### Questão 2 — Academia Movimento (Tipagem, Entrada e conversão, if/else, switch, decimal)

**Situação.** A Academia Movimento tem 3 planos mensais: Plano Básico (código 1) por R$ 89,90, Plano Plus (código 2) por R$ 119,90 e Plano Total (código 3) por R$ 149,90. O aluno pode pagar vários meses de uma vez. A recepcionista digita o código do plano e a quantidade de meses. Ela precisa ver o nome do plano e o total a cobrar, para informar o aluno antes de passar o cartão.

**O que o programa deve fazer.**

- Ler o código do plano (texto) e a quantidade de meses (número inteiro).
- Descobrir o nome e o preço mensal do plano.
- Mostrar o total com 2 casas decimais. Um código que não existe mostra `Plano inválido.`
- Escolher o tipo certo para cada dado: `string` para o nome, `decimal` para o preço, `int` para os meses.

**Dois caminhos de solução.**

- **Caminho 1:** use `if / else if` para comparar o código e definir o nome e o preço.
- **Caminho 2:** use `switch` com um `case` para cada código.

**Testes.**

| Entrada | Saída esperada |
| --- | --- |
| Plano 2, 3 meses | `Plano Plus: 3 mês(es) = R$ 359,70` |
| Plano 9, 3 meses | `Plano inválido.` |

#### Questão 3 — Cadastro de usuários da biblioteca digital (Strings, List, foreach, Operadores lógicos, if/else)

**Situação.** A biblioteca digital da escola cria um login para cada aluno. Três alunos já têm login: `lia.souza`, `noah.lima` e `davi.rocha`. O sistema só aceita um novo nome de usuário que siga 3 regras: ter de 4 a 12 caracteres, não ter espaços no meio e não repetir um usuário já cadastrado. A comparação não diferencia maiúsculas de minúsculas: `NOAH.LIMA` é o mesmo usuário que `noah.lima`. Os espaços digitados sem querer no início e no fim devem ser removidos antes das regras. Quando o nome não passa, o aluno precisa saber qual regra quebrou.

**O que o programa deve fazer.**

- Começar com uma `List<string>` com os 3 usuários já cadastrados.
- Ler o nome de usuário e remover os espaços do início e do fim.
- Testar as regras nesta ordem: tamanho, espaços, usuário repetido.
- Mostrar a mensagem da primeira regra que falhou.
- Se o nome passar nas 3 regras, acrescentá-lo na lista e mostrar o total de usuários.

**Dois caminhos de solução.**

- **Caminho 1:** `Contains(" ")` para achar espaços. Um `foreach` na lista, com uma variável `bool` e `ToLower()`, para achar o usuário repetido.
- **Caminho 2:** um `foreach` que passa por cada letra (`char`) do nome para achar espaços. Um `for` na lista, com a posição `-1`, `break` e `string.Equals` com `StringComparison.OrdinalIgnoreCase`, para achar o usuário repetido.

**Testes.**

| Entrada | Saída esperada |
| --- | --- |
| `  Ana.Lima ` | `Usuário Ana.Lima criado. Total de usuários: 4` |
| `ana` | `O usuário precisa ter de 4 a 12 caracteres.` |
| `ana lima` | `O usuário não pode ter espaços.` |
| `NOAH.LIMA` | `Este usuário já está cadastrado.` |

#### Questão 4 — Pães da padaria (while, Entrada e conversão, Strings, List, for e foreach, decimal)

**Situação.** Toda sexta à noite, o gerente da Padaria Pão Quente digita quantos pães franceses vendeu em cada dia útil da semana. Às vezes ele erra: aperta uma letra, deixa o campo vazio ou digita um sinal de menos. O programa não pode fechar nem pular o dia quando isso acontece. Ele avisa e pede o mesmo dia de novo. No fim, o gerente quer o total da semana, a média por dia e o dia com mais vendas.

**O que o programa deve fazer.**

- Guardar os dias (`Segunda` a `Sexta`) em uma `List<string>` e as quantidades em uma `List<int>`.
- Pedir a quantidade de cada dia com `while`. Só aceitar um texto que não seja vazio e tenha apenas dígitos de 0 a 9. Só então converter com `int.Parse`.
- Com valor inválido, mostrar `Digite só números. Tente de novo.` e pedir o mesmo dia.
- Mostrar o total, a média com 2 casas decimais e o dia com mais vendas.

**Dois caminhos de solução.**

- **Caminho 1:** conferir os caracteres com `foreach`. Fazer o resumo com `for`, guardando a posição do dia com mais vendas.
- **Caminho 2:** conferir os caracteres com `for` e `texto[i]`. Fazer o resumo com `foreach` e um contador de posição.

Dicas para os 2 caminhos:

- Use `int dia = 0` como posição do dia atual. O `while (dia < dias.Count)` só termina quando os 5 dias forem preenchidos. Some 1 em `dia` apenas quando o valor for válido.
- Um caractere é dígito quando está entre `'0'` e `'9'`. Então ele é inválido quando `letra < '0' || letra > '9'`.
- Para a média ter casas decimais, guarde o total em uma variável `decimal`.

**Teste.** Digite em sequência: `120`, `abc`, `95`, `150`, `-10`, `110`, (vazio), `178`.

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

### Nível 2

#### Questão 5 — Frete da loja online (Entrada e conversão, Strings, switch, if/else, Operadores, decimal)

**Situação.** A loja online Casa & Cia calcula o frete pela região de entrega e pelo peso do pacote. O frete base é R$ 15,00 para o Nordeste (1), R$ 25,00 para o Sudeste (2), R$ 30,00 para o Sul (3) e R$ 35,00 para o Norte e o Centro-Oeste (4). O frete base cobre até 5 kg. Cada kg acima de 5 custa R$ 2,50 a mais. O atendente digita a região e o peso em kg, arredondado para um número inteiro, e às vezes erra a digitação.

**O que o programa deve fazer.**

- Ler a região. Se for inválida, mostrar `Região inválida.` e não pedir o peso.
- Ler o peso. Só aceitar um texto que não seja vazio e tenha apenas dígitos de 0 a 9. Senão, mostrar `Digite o peso só com números.`
- Converter o peso com `int.Parse` e calcular o frete. Mostrar o valor com 2 casas decimais.

**Dois caminhos de solução.**

- **Caminho 1:** `switch` para a região e `foreach` para conferir os caracteres do peso.
- **Caminho 2:** `if / else if` para a região e `for` com `texto[i]` para conferir os caracteres do peso.

**Testes.**

| Região, peso | Saída esperada |
| --- | --- |
| 2, 8 | `Frete: R$ 32,50` |
| 1, 3 | `Frete: R$ 15,00` |
| 2, abc | `Digite o peso só com números.` |
| 3, 7,5 | `Digite o peso só com números.` |
| 9 | `Região inválida.` |

#### Questão 6 — Lista de convidados do casamento (while, switch, if/else, Strings, List, Busca)

**Situação.** A cerimonialista de um casamento monta a lista de convidados no notebook nas semanas anteriores à festa. No dia do evento, o mesmo programa é usado na portaria. Os nomes são digitados de formas diferentes (`Ana Lima`, `ana lima`, `ANA LIMA`), e ninguém pode entrar duas vezes na lista. Nomes com menos de 3 caracteres são erros de digitação.

**O que o programa deve fazer.**

- Menu com 1 (adicionar), 2 (conferir na portaria), 3 (listar) e 0 (sair), repetido até a opção 0.
- Adicionar: remover espaços extras, recusar nomes curtos e recusar nomes repetidos sem diferenciar maiúsculas de minúsculas.
- Conferir: mostrar `Entrada liberada.` ou `Nome não está na lista.`
- Listar: mostrar os nomes numerados a partir de 1 e o total, ou `Nenhum convidado na lista.`

**Dois caminhos de solução.**

- **Caminho 1:** menu com `switch`. A busca usa `foreach`, uma variável `bool` e `ToLower()`.
- **Caminho 2:** menu com `if / else if`. A busca usa `for`, a posição `-1`, `break` e `string.Equals`. As opções 1 e 2 dividem a mesma busca.

**Teste.** Digite em sequência: 3 → 1 `  Ana Lima ` → 1 `ana lima` → 1 `Bo` → 1 `Davi` → 2 `ANA LIMA` → 2 `Eva` → 3 → 7 → 0. A saída esperada, na ordem:

```text
Nenhum convidado na lista.
Ana Lima adicionado.
ana lima já está na lista.
O nome precisa ter pelo menos 3 caracteres.
Davi adicionado.
Entrada liberada.
Nome não está na lista.
1. Ana Lima
2. Davi
Total: 2
Opção inválida. Escolha uma opção de 0 a 3.
Encerrando.
```

#### Questão 7 — Boletim da turma (Lista aninhada, for e foreach, Entrada e conversão, decimal, if/else)

**Situação.** A coordenação precisa fechar o boletim do bimestre. Cada aluno tem 2 notas inteiras, guardadas como texto em uma tabela: Lia (8 e 6), Noah (5 e 4) e Davi (7 e 4). A média é a soma das 2 notas dividida por 2. Média 7 ou mais é Aprovado, de 5 até menos de 7 é Recuperação, menos de 5 é Reprovado.

**O que o programa deve fazer.**

- Guardar os alunos em uma `List<List<string>>`, com os campos `[0] nome`, `[1] nota 1`, `[2] nota 2`.
- Converter as notas com `int.Parse` e calcular a média em `decimal`. Cuidado: divida por `2m`, não por `2`.
- Mostrar `nome | média | situação` para cada aluno, com a média em 1 casa decimal.

**Dois caminhos de solução.**

- **Caminho 1:** `foreach` nas linhas. Cada linha é um aluno, e o campo é lido com 1 índice: `aluno[1]`.
- **Caminho 2:** `for` com índice. O campo é lido com 2 índices: `alunos[i][1]`.

**Saída esperada.**

```text
Lia | média 7,0 | Aprovado
Noah | média 4,5 | Reprovado
Davi | média 5,5 | Recuperação
```

#### Questão 8 — Caixa da cantina (while, switch, if/else, Operadores, decimal e porcentagem)

**Situação.** A cantina da escola instalou um caixa de autoatendimento. O aluno digita o código de cada produto: 1 Salgado (R$ 6,50), 2 Suco (R$ 5,00) e 3 Bolo (R$ 4,50). Quando termina, ele digita 0. Um código que não existe é ignorado com um aviso, e o caixa continua funcionando. No fim, a cantina dá um desconto progressivo: 10% para compras de R$ 30,00 ou mais, 5% para compras de R$ 20,00 ou mais, e nenhum desconto abaixo disso.

**O que o programa deve fazer.**

- Repetir a leitura de códigos até o aluno digitar `0`.
- Somar o preço de cada produto válido e contar quantos itens entraram.
- Para um código inválido, mostrar `Código inválido. Item ignorado.`
- Mostrar a quantidade de itens, o subtotal, o percentual e o valor do desconto, e o total.

**Dois caminhos de solução.**

- **Caminho 1:** `while (codigo != "0")` e `switch` para somar o produto. O percentual fica guardado como número inteiro (`10m`), e o cálculo é `subtotal * percentual / 100`.
- **Caminho 2:** `while` controlado por uma variável `bool` e `if / else if` para somar o produto. A taxa fica guardada como fração (`0.10m`), e o cálculo é `subtotal * taxa`.

**Testes.**

| Códigos digitados | Saída esperada |
| --- | --- |
| 1, 1, 2, x, 3, 1, 0 | 1 aviso de código inválido. `Itens: 5`, `Subtotal: R$ 29,00`, `Desconto (5%): R$ 1,45`, `Total: R$ 27,55` |
| 1, 1, 1, 1, 1, 0 | `Itens: 5`, `Subtotal: R$ 32,50`, `Desconto (10%): R$ 3,25`, `Total: R$ 29,25` |
| 1, 2, 0 | `Itens: 2`, `Subtotal: R$ 11,50`, `Desconto (0%): R$ 0,00`, `Total: R$ 11,50` |

### Nível 3 — Programas completos (opcional)

Estes programas juntam quase todos os capítulos. Faça-os só depois de resolver as questões 1 a 8 pelos 2 caminhos. O gabarito mostra o caminho 1.

#### Programa A — Cadastro de produtos (while, switch, Strings, Lista aninhada, Busca)

**Situação.** A Papelaria Ponto Final quer cadastrar seus produtos sem repetir nomes. Cada produto tem um nome e uma categoria: Papelaria (1) ou Informática (2).

- Menu com 1 (cadastrar), 2 (listar) e 0 (sair).
- Remover espaços extras do nome. Recusar nomes com menos de 3 caracteres, nomes repetidos (sem diferenciar maiúsculas) e categorias inválidas.
- Listar no formato `nome | categoria`, ou mostrar `Nenhum produto cadastrado.`
- **Caminho 1:** `switch` para a categoria e `foreach` com `bool` para a busca. **Caminho 2:** `if / else if` para a categoria e `for` com `break` para a busca.
- **Teste:** cadastre `  Caderno  `. Depois tente `caderno`, `ab` e a categoria `9`. Os 3 devem ser recusados.

#### Programa B — Fila de impressão (while, switch, Strings, List, Operadores lógicos)

**Situação.** A impressora do escritório imprime os documentos na ordem em que foram enviados. Antes de imprimir, o funcionário informa o número de cópias, de 1 a 5.

- Menu com 1 (enviar documento), 2 (ver fila), 3 (imprimir próximo) e 0 (sair).
- Ver fila mostra a posição a partir de 1, ou `A fila está vazia.`
- Com número de cópias inválido, o documento continua no início da fila.
- **Caminho 1:** validar as cópias com um `switch` com `case "1"` a `case "5"` seguidos. **Caminho 2:** validar as cópias com `if`, conferindo que o texto tem 1 caractere (`copias.Length == 1`) e que ele está entre `'1'` e `'5'`.
- **Teste:** envie `relatorio.pdf` e `foto.png`. Imprima com `abc`: `relatorio.pdf` continua em 1º lugar. Imprima com `2`: `foto.png` passa para o 1º lugar. Imprima com `6`: `foto.png` continua na fila.

#### Programa C — Ingressos do cinema (Tipagem, switch, if/else, decimal e porcentagem)

**Situação.** O Cine Estrela cobra conforme o tipo de ingresso e a sessão. Tipos: Inteira (1, 0% de desconto), Meia (2, 50%) e Estudante (3, 30%). Sessões: Tarde (1, R$ 30,00) e Noite (2, R$ 44,00).

- Ler o tipo e a sessão. Mostrar o tipo, o percentual e o valor final com 2 casas. Mostrar uma mensagem para código inválido.
- **Caminho 1:** dois `switch`. **Caminho 2:** dois blocos de `if / else if`.

| Tipo | Tarde (R$ 30,00) | Noite (R$ 44,00) |
| --- | --- | --- |
| Inteira (0%) | R$ 30,00 | R$ 44,00 |
| Meia (50%) | R$ 15,00 | R$ 22,00 |
| Estudante (30%) | R$ 21,00 | R$ 30,80 |

## Checklist de autoavaliação

Marque cada item que você consegue fazer sem consultar este material. Um item sem marcação indica o capítulo que você deve rever.

- [ ] Criar e executar um projeto de console com `dotnet new console` e `dotnet run` (Capítulo 1)
- [ ] Escolher entre `int`, `decimal`, `string` e `bool` para um dado e explicar o motivo (Capítulo 2)
- [ ] Ler um texto com `Console.ReadLine() ?? ""` (Capítulo 3)
- [ ] Explicar o que acontece quando `int.Parse` recebe letras, e evitar o erro com `TryParse` ou `switch` (Capítulos 3 e 4)
- [ ] Escrever um `if / else if / else` na ordem certa (Capítulo 4)
- [ ] Usar `switch` para traduzir um código em um nome e um valor, com `default` para código inválido (Capítulo 4)
- [ ] Montar um menu que repete até a opção 0 e trata opções inválidas (Capítulo 5)
- [ ] Limpar um texto com `Trim()` e validar o tamanho mínimo (Capítulo 6)
- [ ] Comparar dois textos sem diferenciar maiúsculas de minúsculas (Capítulo 6)
- [ ] Acrescentar, ler, contar e remover itens de uma `List` (Capítulo 7)
- [ ] Mostrar uma lista numerada a partir de 1 e tratar a lista vazia (Capítulo 7)
- [ ] Usar uma `List` como ordem de chegada: ler `[0]`, validar, e só então `RemoveAt(0)` (Capítulo 7)
- [ ] Criar uma `List<List<string>>` e acessar um campo com dois índices (Capítulo 8)
- [ ] Buscar uma linha pelo valor de um campo e impedir registros repetidos (Capítulo 9)
- [ ] Calcular um desconto percentual com `decimal` e mostrar com `F2` (Capítulo 10)
- [ ] Explicar por que `15 / 100` dá `0` em `int` (Capítulo 10)
- [ ] Resolver as questões 1 a 8 pelos 2 caminhos sem olhar o gabarito

## Gabarito

Os 2 caminhos de cada questão dão a mesma saída. Nos programas A, B e C, o gabarito mostra o caminho 1. Todas foram executadas e testadas. Se a sua resposta é diferente, mas a saída está certa, ela também vale.

### Questão 1 — Eleição do representante de turma

**Caminho 1 — `while` e `switch`**

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

**Caminho 2 — `while` com variável `bool` e `if / else if`**

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

**Compare:** no caminho 1, o `case "0"` existe só para o `0` não cair no `default` e virar nulo. No caminho 2, o `0` é testado primeiro e só muda `votacaoAberta` para `false`. Assim, ele nunca chega ao `else` dos nulos. No caminho 2, `voto` pode ser declarada dentro do `while`, porque a condição do laço não usa `voto`. A variável `bool` de controle também serve quando o laço tem mais de um motivo para parar.

### Questão 2 — Academia Movimento

**Caminho 1 — `if / else if`**

```csharp
Console.Write("Código do plano (1 Básico, 2 Plus, 3 Total): ");
string codigo = Console.ReadLine() ?? "";
Console.Write("Quantidade de meses: ");
int meses = int.Parse(Console.ReadLine() ?? "0");

string plano = "";
decimal precoMensal = 0m;

if (codigo == "1")
{
    plano = "Básico";
    precoMensal = 89.90m;
}
else if (codigo == "2")
{
    plano = "Plus";
    precoMensal = 119.90m;
}
else if (codigo == "3")
{
    plano = "Total";
    precoMensal = 149.90m;
}

if (plano == "")
{
    Console.WriteLine("Plano inválido.");
}
else
{
    decimal total = precoMensal * meses;
    Console.WriteLine($"Plano {plano}: {meses} mês(es) = R$ {total:F2}");
}
```

**Caminho 2 — `switch`**

```csharp
Console.Write("Código do plano (1 Básico, 2 Plus, 3 Total): ");
string codigo = Console.ReadLine() ?? "";
Console.Write("Quantidade de meses: ");
int meses = int.Parse(Console.ReadLine() ?? "0");

string plano = "";
decimal precoMensal = 0m;

switch (codigo)
{
    case "1": plano = "Básico"; precoMensal = 89.90m; break;
    case "2": plano = "Plus"; precoMensal = 119.90m; break;
    case "3": plano = "Total"; precoMensal = 149.90m; break;
}

if (plano == "")
{
    Console.WriteLine("Plano inválido.");
}
else
{
    decimal total = precoMensal * meses;
    Console.WriteLine($"Plano {plano}: {meses} mês(es) = R$ {total:F2}");
}
```

**Compare:** os dois caminhos usam `plano == ""` para saber se o código era válido. Para códigos fixos, o `switch` fica mais curto. `decimal` vezes `int` dá `decimal`, então o total não perde os centavos.

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

### Questão 7 — Boletim da turma

**Caminho 1 — `foreach`**

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

**Caminho 2 — `for` com índice**

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

**Compare:** no `foreach`, `aluno` já é a linha, então o campo é `aluno[1]`. No `for`, a linha é `alunos[i]`, então o campo é `alunos[i][1]`: o primeiro índice escolhe a linha, o segundo escolhe o campo. Se a divisão fosse por `2` (inteiro), Noah teria média 4 em vez de 4,5. `F1` mostra 1 casa decimal.

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
