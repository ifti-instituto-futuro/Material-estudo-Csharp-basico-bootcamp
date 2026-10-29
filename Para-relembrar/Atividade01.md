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
// Os contadores guardam votos de cada opção; voto é texto porque vem do teclado.
int votosAna = 0;
int votosBruno = 0;
int nulos = 0;
string voto = "";

// O laço continua até a entrada ser exatamente "0".
while (voto != "0")
{
    Console.Write("Voto (1 Ana, 2 Bruno, 0 encerra): ");
    voto = Console.ReadLine() ?? "";

    // O switch encaminha cada código para a contagem correspondente.
    switch (voto)
    {
        case "1": votosAna++; break;
        case "2": votosBruno++; break;
        // O zero encerra sem aumentar nenhum contador.
        case "0": break;
        default: nulos++; break;
    }
}

// Mostra o resumo e, abaixo, compara as contagens.
Console.WriteLine($"Ana: {votosAna} | Bruno: {votosBruno} | Nulos: {nulos}");

// As condições determinam quem venceu ou se houve empate.
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

> **Leitura do código**
>
> - **Linhas 1–5:** criam os três contadores e a variável `voto`. Os contadores começam em zero; `voto` começa vazio para que o `while` entre na primeira vez.
> - **Linhas 7–11:** o `while` foi escolhido porque não sabemos quantos alunos votarão. Ele repete a leitura até receber `"0"`, que funciona como valor de encerramento.
> - **Linhas 13–22:** o `switch` traduz cada texto digitado em uma ação: contar Ana, contar Bruno, encerrar sem contar ou registrar um nulo.
> - **Linhas 24–39:** imprime as contagens e compara os votos. As duas primeiras condições identificam um vencedor; o `else` cobre o empate.

#### Caminho 2 — `while` com variável `bool` e if / else if

```csharp
int votosAna = 0;
int votosBruno = 0;
int nulos = 0;
// Esta variável booleana controla quando o laço deve terminar.
bool votacaoAberta = true;

// O laço segue enquanto a votação estiver aberta.
while (votacaoAberta)
{
    Console.Write("Voto (1 Ana, 2 Bruno, 0 encerra): ");
    string voto = Console.ReadLine() ?? "";

    // O zero fecha a votação antes de qualquer outra classificação.
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
    // Qualquer texto diferente de 0, 1 ou 2 conta como voto nulo.
    else
    {
        nulos++;
    }
}

// Depois do laço, mostra o resumo e calcula o vencedor.
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

> **Leitura do código**
>
> - **Linhas 1–5:** inicializam os contadores e definem `votacaoAberta` como `true`, permitindo que a votação comece.
> - **Linhas 7–17:** o `while` mantém a leitura enquanto `votacaoAberta` for verdadeira. Ao digitar `"0"`, a variável vira `false` e o laço termina. `while` funciona bem porque as entradas continuam até aparecer esse sinal de parada.
> - **Linhas 18–30:** a cadeia `if / else if / else` classifica cada voto restante. Como o zero foi tratado primeiro, letras e outros códigos acabam como nulos.
> - **Linhas 33–47:** mostra o resumo e usa comparações para decidir entre Ana, Bruno e empate.

Compare: no caminho 1, o case "0" existe só para o 0 não cair no default e virar nulo. No caminho 2, o 0 é testado primeiro e só muda votacaoAberta para `false`. Assim, ele nunca chega ao else dos nulos. No caminho 2, voto pode ser declarada dentro do `while`, porque a condição do laço não usa voto. A variável `bool` de controle também serve quando o laço tem mais de um motivo para parar.


### Recapitulando os conceitos

O console sempre entrega o que foi digitado como texto. Por isso `voto` é uma `string`, e o código compara com valores como `"1"` e `"0"`. As três contagens são `int`, pois só podem aumentar em números inteiros. O operador `++` soma um voto ao contador.

O `while` é indicado quando não se sabe quantas vezes a repetição será necessária. Aqui, cada voto válido ou inválido provoca outra leitura; o código `0` é o sentinela que encerra. No primeiro caminho, a própria condição verifica o último voto. No segundo, um `bool` representa o estado da votação. Ambos dependem de testar o encerramento antes de contar um nulo.

O `switch` organiza alternativas fixas para os códigos conhecidos e usa `default` para tudo que não corresponde a eles. A cadeia `if / else if / else` faz a mesma classificação em ordem. No final, operadores `>` comparam as contagens; se nenhuma candidata tiver mais votos que a outra, resta o empate.
