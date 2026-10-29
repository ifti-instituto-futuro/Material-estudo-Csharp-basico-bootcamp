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
// As listas usam a mesma posição para relacionar dia e quantidade de pães.
List<string> dias = new List<string> { "Segunda", "Terça", "Quarta", "Quinta", "Sexta" };
List<int> paes = new List<int>();

// dia é o índice do dia que está sendo preenchido.
int dia = 0;
while (dia < dias.Count)
{
    Console.Write($"{dias[dia]} - pães vendidos: ");
    string texto = (Console.ReadLine() ?? "").Trim();

    // Texto vazio começa inválido; depois, cada caractere é conferido.
    bool valido = texto != "";
    // O foreach visita cada caractere sem precisar controlar um índice.
    foreach (char letra in texto)
    {
        if (letra < '0' || letra > '9')
        {
            valido = false;
        }
    }

    // Só converte e avança quando toda a entrada é válida.
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

// decimal mantém as casas decimais no cálculo da média.
decimal total = 0m;
int posicaoMaior = 0;

// O índice i percorre as quantidades e identifica a posição do maior valor.
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

> **Leitura do código**
>
> - **Linhas 1–6:** cria duas listas relacionadas pela posição: `dias[0]` corresponde a `paes[0]`. `dia` guarda a posição que está sendo preenchida.
> - **Linhas 7–21:** o `while` continua enquanto faltarem dias válidos. Ele permite repetir o mesmo dia após um erro. O `foreach` percorre os caracteres e rejeita qualquer um fora do intervalo de `0` a `9`.
> - **Linhas 23–33:** apenas uma entrada válida chega a `int.Parse` e é adicionada. `dia++` fica dentro desse bloco; por isso, uma entrada errada não pula para o próximo dia.
> - **Linhas 35–52:** soma as quantidades e guarda o índice do maior valor. Com esse índice, o programa encontra o dia correspondente. `decimal` permite calcular a média com casas decimais.

#### Caminho 2 — validação com for e resumo com `foreach`

```csharp
// As listas mantêm os dias e as quantidades alinhados pela mesma posição.
List<string> dias = new List<string> { "Segunda", "Terça", "Quarta", "Quinta", "Sexta" };
List<int> paes = new List<int>();

// dia é o índice do dia que está sendo preenchido.
int dia = 0;
while (dia < dias.Count)
{
    Console.Write($"{dias[dia]} - pães vendidos: ");
    string texto = (Console.ReadLine() ?? "").Trim();

    // A entrada vazia é rejeitada antes da conversão.
    bool valido = texto != "";
    // O índice i permite examinar cada caractere digitado.
    for (int i = 0; i < texto.Length; i++)
    {
        if (texto[i] < '0' || texto[i] > '9')
        {
            valido = false;
        }
    }

    // Só converte e avança o dia quando todos os caracteres passam.
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

// decimal mantém a parte fracionária do cálculo da média.
decimal total = 0m;
// -1 permite registrar o primeiro dia mesmo quando todas as quantidades são zero.
int maior = -1;
string diaMaior = "";
int posicao = 0;

// posicao acompanha o dia correspondente a cada quantidade.
foreach (int quantidade in paes)
{
    total = total + quantidade;

    // Guarda o maior valor e o dia que ocupa a mesma posição.
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

> **Leitura do código**
>
> - **Linhas 1–6:** monta as listas de dias e pães e inicia o índice do dia atual. As duas listas mantêm os valores associados pela mesma posição.
> - **Linhas 7–21:** o `while` repete até os cinco dias terem entradas válidas. O `for` foi usado para ler cada caractere por `texto[i]` e conferir se é um dígito.
> - **Linhas 23–33:** validação e conversão ficam separadas: só texto válido é convertido e salvo, e só então `dia` avança.
> - **Linhas 35–59:** o `foreach` soma cada quantidade; `posicao` acompanha o dia correspondente. `maior` começa em `-1` para que até valores todos iguais a zero definam um dia. A média usa `decimal`.

Compare: o ponto principal dos 2 caminhos é o dia++ dentro do bloco válido. Com valor inválido, dia não muda, então o `while` pede o mesmo dia de novo. A validação começa com valido = texto != "", que recusa o texto vazio. Depois, qualquer caractere fora de '0' a '9' muda valido para `false`, inclusive letras e o sinal -. Como o texto já foi conferido, o `int.Parse` nunca quebra. O `foreach` dá cada caractere direto. O for usa a posição i e lê o caractere com `texto[i]`. O total é `decimal` para que total / paes.Count mantenha as casas decimais (653 / 5 = 130,60).


### Recapitulando os conceitos

As listas `dias` e `paes` são paralelas: o item na posição `i` de uma corresponde ao item na posição `i` da outra. A variável `dia` indica qual dia está recebendo dados. O `while` repete o pedido até haver cinco respostas válidas; por isso ele também permite tentar novamente sem pular o dia.

A entrada começa como texto. Antes de chamar `int.Parse`, o programa confere que ela não está vazia e que cada caractere está entre `0` e `9`. O primeiro caminho usa `foreach` para receber cada caractere diretamente; o segundo usa `for` e o índice `texto[i]`. Em ambos, a conversão ocorre somente depois da validação. Deixar `dia++` dentro do ramo válido é o que mantém o mesmo dia quando há erro.

No resumo, `decimal` evita perder casas decimais ao calcular a média. Um laço soma os valores e guarda a posição do maior; essa posição também encontra o nome do dia. O primeiro caminho usa `for` e já tem o índice disponível. O segundo usa `foreach`, então mantém uma variável `posicao` para relacionar cada quantidade ao dia. A comparação estrita `>` preserva o primeiro dia em caso de empate.
