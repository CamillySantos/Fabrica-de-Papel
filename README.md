# Fabrica-de-Papel

Registo das atividades do curso que estou realizando sobre SQL é relacionado a uma fábrica de papel onde estou aprendendo sobre diferentes formas de fazer pesquisas em Bancos de dados.


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

