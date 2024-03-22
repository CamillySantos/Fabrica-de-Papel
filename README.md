# Módulo 1 - Fábrica de Papel

Registo das atividades do curso que estou realizando sobre SQL é relacionado a uma fábrica de papel onde estou aprendendo sobre diferentes formas de fazer pesquisas em Bancos de dados e essas são as atividades do primeiro módulo.


## Material de aula

O material disponibilizado pelo curso para entendermos sobre Banco de Dados e começar as pesquisas conforme as aulas.

[Fabrica de papel](https://github.com/CamillySantos/Fabrica-de-Papel/blob/main/PostgreSQL.sql)


## 1. SELECT e FROM

Tente escrever sua própria consulta para selecionar apenas as colunas `id`, `account_id` e `occurred_at` para todos os pedidos na tabela de `orders` (pedidos).

```
SELECT id, account_id, occurred_at
FROM orders;
```


## 2. LIMIT

Tente usar `LIMIT`, escrevendo uma consulta que exibe todos os dados nas colunas `occurred_at`, `account_id` e `channel` da tabela `web_events` e limita a saída apenas às primeiras `15 linhas`.

```
SELECT occurred_at, account_id, channel
FROM web_events
LIMIT 15;
```

## 3. ORDER BY

1. Escreva uma consulta para retornar os `10 primeiros pedidos` na tabela de `orders` (pedidos) . Inclua `id`, `occurred_at`, e `total_amt_usd`.

```
SELECT id, occurred_at, total_amt_usd
FROM orders
ORDER BY occurred_at
LIMIT 10;
```

2. Escreva uma consulta para retornar os `5 principais pedidos` em termos do maior `total_amt_usd`. Inclua `id`, `account_id`, e `total_amt_usd`.

```
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC 
LIMIT 5;
```

3. Escreva uma consulta para retornar os `20 pedidos` mais baixos em termos de menor `total_amt_usd`. Inclua `id`, `account_id`, e `total_amt_usd`.

```
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY total_amt_usd
LIMIT 20;
```

## 4. ORDER BY parte ||

1. Escreva uma consulta que exiba o ID do pedido, o ID da conta e o valor total em dólares de todos os pedidos, classificados primeiro pelo ID da conta (em ordem crescente) e depois pelo valor total em dólares (em ordem decrescente).

```
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY account_id, total_amt_usd DESC;
```

2. Agora escreva uma consulta que exiba novamente o ID do pedido, o ID da conta e o valor total em dólares de cada pedido, mas desta vez classificado primeiro pelo valor total em dólares (em ordem decrescente) e depois pelo ID da conta (em ordem crescente).

```
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC, account_id;
```

3. Compare os resultados dessas duas consultas acima. Como os resultados são diferentes quando você alterna a coluna que classifica primeiro?

```
Na consulta nº 1, todos os pedidos para cada ID de conta são agrupados e, em cada um desses agrupamentos, os pedidos aparecem do maior para o menor valor do pedido.
Na consulta nº 2,como você classificou primeiro pelo valor total em dólares, os pedidos aparecem do maior para o menor, independentemente do ID da conta de onde vieram.
Em seguida, eles são classificados por ID da conta.
```

## 5. WHERE

1. Extrai as primeiras 5 linhas e todas as colunas da tabela de `orders`(pedidos) que possuem um valor em dólares `gloss_amt_usd` maior ou igual a 1.000.

```
SELECT *
FROM orders
WHERE gloss_amt_usd >= 1000
LIMIT 5;
```

3. Extrai as primeiras 10 linhas e todas as colunas da tabela de `orders` (pedidos) que tenham `total_amt_usd` menos de 500.

```
SELECT *
FROM orders 
WHERE total_amt_usd < 500
LIMIT 10;
```

## 6. WHERE com não números

Filtre a tabela de contas para incluir a empresa `name`, `website` e o principal ponto de contato `(primary_poc)` apenas da empresa Exxon Mobil na tabela `accounts`(contas).

```
SELECT name, website, primary_poc
FROM accounts
WHERE name = 'Exxon Mobil';
```

## 7. Operadores Aritméticos + Colunas Derivadas

1. Crie uma coluna que divida por `standard_amt_usd` para `standard_qty` encontrar o preço unitário do papel padrão para cada pedido. Limite os resultados aos primeiros 10 pedidos e inclua os campos `id` e `account_id`.

```
SELECT id, account_id, standard_amt_usd/standard_qty AS valor_padrao
FROM orders
LIMIT 10;
```

2. Escreva uma consulta que encontre a porcentagem da receita proveniente do papel de poster para cada pedido. Você precisará usar apenas as colunas que terminam com `_usd`. (Tente fazer isso sem usar a `total` coluna.) Exiba também os campos `id` e `account_id`.

```
SELECT id, account_id, poster_amt_usd/(standard_amt_usd + gloss_amt_usd + poster_amt_usd) AS papel_poster
FROM orders
LIMIT 10;
```

## 8. Operadores Lógicos

### LIKE

Use a tabela de `accounts` (contas) para encontrar

1. Todas as empresas cujos nomes começam com 'C'.
   
```
SELECT name
FROM accounts
WHERE name LIKE 'C%';
```

2. Todas as empresas cujos nomes contêm a string `'one'` em algum lugar do nome.

```
SELECT name
FROM accounts
WHERE name LIKE '%one%';
```

3. Todas as empresas cujos nomes terminam com `'s'`.

```
SELECT name
FROM accounts
WHERE name LIKE '%s';
```

### IN

1. Use a tabela de `acconunts` (contas) para encontrar a conta `name`, `primary_poc` e `sales_rep_id` para Walmart, Target e Nordstrom

```
SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name IN ('Walmart', 'Target', 'Nordstrom');
```

2. Utilize a tabela `web_events` para encontrar todas as informações sobre indivíduos que foram contatados através do `channel` (canal) de `organic` ou `adwords`.

```
SELECT *
FROM web_events
WHERE channel IN ('organic', 'adwords');
```

### NOT

Podemos extrair todas as linhas que foram excluídas das consultas nos dois conceitos anteriores com nosso novo operador

1. Use a tabela de `acconunts` (contas) para encontrar a conta `name`, `primary_poc` e `sales_rep_id` de todas as lojas, exceto Walmart, Target e Nordstrom.

```
SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name NOT IN ('Walmart', 'Target', 'Nordstrom');
```

2. Use a tabela `web_events` para encontrar todas as informações sobre indivíduos que foram contatados por qualquer método, exceto os métodos `organic` ou `adwords`.

```
SELECT *
FROM web_events
WHERE channel NOT IN ('organic', 'adwords');
```

Use a tabela de `accounts` (contas) para encontrar

1. Todas as empresas cujos nomes não começam com 'C'.
   
```
SELECT name
FROM accounts
WHERE name NOT LIKE 'C%';
```

2. Todas as empresas cujos nomes não contêm a string `'one'` em algum lugar do nome.

```
SELECT name
FROM accounts
WHERE name NOT LIKE '%one%';
```

3. Todas as empresas cujos nomes não terminam com `'s'`.

```
SELECT name
FROM accounts
WHERE name NOT LIKE '%s';
```

### AND e BETWEEN

1. Escreva uma consulta que retorne todos os pedidos `orders` em que `standard_qty` é maior que 1000, `poster_qty` é 0 e `gloss_qty` é 0.

```
SELECT *
FROM orders
WHERE standard_qty > 1000 AND poster_qty = 0 AND gloss_qty = 0;
```

2. Utilizando a tabela de contas `accounts` , encontre todas as empresas cujos nomes não começam com 'C' e terminam com 's'.

```
SELECT *
FROM accounts
WHERE name NOT LIKE 'C%' AND name LIKE '%s';
```

3. Quando você usa o operador BETWEEN em SQL, os resultados incluem os valores dos seus endpoints ou não? Descubra a resposta a esta importante questão escrevendo uma consulta que exiba a data do pedido e `gloss_qty` os dados de todos **os pedidos** em que gloss_qty está entre 24 e 29. Em seguida, observe sua saída para ver se o operador BETWEEN incluiu os valores inicial e final ou não.

```
SELECT occurred_at, gloss_qty
FROM orders
WHERE gloss_qty BETWEEN 24 AND 29;
```

****

4. Use a tabela **web_events** para encontrar todas as informações sobre indivíduos que foram contatados por meio dos canais `organic` ou `adwords` e que iniciaram suas contas em qualquer momento de 2016, classificados do mais recente para o mais antigo.

```
SELECT *
FROM web_events
WHERE channel IN ('organic', 'adwords') AND occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
ORDER BY occurred_at DESC;
```
## OR 

1. Encontre a lista de IDs de `orders` (pedidos) `gloss_qty` em que ou `poster_qty` seja maior que 4.000. Inclua apenas o `id` campo na tabela resultante.

```
SELECT id
FROM orders 
WHERE gloss_qty > 4000 OR poster_qty > 4000;
```

2. Escreva uma consulta que retorne uma lista de `orders` (pedidos) em que the `standard_qty` é zero e ou `gloss_qty` é `poster_qty` maior que 1.000.

```
SELECT * 
FROM orders 
WHERE standard_qty = 0 AND (gloss_qty > 1000 OR poster_qty > 1000);
```

3. Encontre todos os nomes de empresas que começam com 'C' ou 'W' e o contato principal **contém** 'ana' ou 'Ana', mas não contém 'eana'.

```
SELECT * 
FROM accounts 
WHERE (name LIKE 'C%' OR name LIKE 'W%') AND ((primary_poc LIKE '%ana%' OR primary_poc LIKE '%Ana%') AND primary_poc NOT LIKE '%eana%');
```


