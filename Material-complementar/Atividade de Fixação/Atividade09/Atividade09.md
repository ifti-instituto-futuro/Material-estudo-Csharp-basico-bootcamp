#### Programa A — Cadastro de produtos (while, switch, Strings, Lista aninhada, Busca)

**Situação.** A Papelaria Ponto Final quer cadastrar seus produtos sem repetir nomes. Cada produto tem um nome e uma categoria: Papelaria (1) ou Informática (2).

- Menu com 1 (cadastrar), 2 (listar) e 0 (sair).
- Remover espaços extras do nome. Recusar nomes com menos de 3 caracteres, nomes repetidos (sem diferenciar maiúsculas) e categorias inválidas.
- Listar no formato `nome | categoria`, ou mostrar `Nenhum produto cadastrado.`
- **Caminho 1:** `switch` para a categoria e `foreach` com `bool` para a busca. **Caminho 2:** `if / else if` para a categoria e `for` com `break` para a busca.
- **Teste:** cadastre `  Caderno  `. Depois tente `caderno`, `ab` e a categoria `9`. Os 3 devem ser recusados.
