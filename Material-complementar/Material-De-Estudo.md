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
