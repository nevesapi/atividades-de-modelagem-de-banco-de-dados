# Comandos para operações CRUD no Banco de Dados

## Resumo

- C -> *C*REATE = **INSERT**: Inserir dados/registros na tabela
- R -> *R*EAD = **SELECT**: Consultar/ler dados/registros na tabela
- U -> *U*PDATE = **UPDATE**: Atualizar dados/registros na tabela
- D -> *D*ELETE = **DELETE**: Excluir dados/registros na tabela

---

## INSERT(Fabricantes)

```sql

INSERT INTO fabricantes(nome) VALUES('Asus');

INSERT INTO fabricantes(nome) VALUES('Dell');

INSERT INTO fabricantes(nome) VALUES('Apple');

INSERT INTO fabricantes(nome) VALUES('LG'), ('Samsung'), ('Brastemp');
```

## SELECT(Fabricantes)

```sql

SELECT * FROM `fabricantes`;

```

---

## INSERT(produtos)

```sql

INSERT INTO produtos(nome, descricao, preco, quantidade, fabricante_id)
VALUES(
  'Ultrabook',
  'Equipamento de última geração, cheio de recursos',
  4123.12,
  8,
  2 -- id do fabricante Dell / fk
);

INSERT INTO produtos(nome, descricao, preco, quantidade, fabricante_id)
VALUES(
  'Tablet Android',
  'Tablet com android 14.0 128GB rom e 32GB ram.',
  2123.12,
  5,
  5 -- id do fabricante Samsung / fk
);

--multi-inserções
INSERT INTO produtos(nome, descricao, preco, quantidade, fabricante_id)
VALUES(
  'Geladeira',
  'Refrigerador frost-free com acesso à internet',
  5000,
  12,
  6 -- id do fabricante Brastemp / fk
),
(
  'Iphone 18 pro Max',
  'Smartphone Apple cheio de frufru',
  9666.26,
  3,
  3 -- id do fabricante Apple / fk
),
(
  'iPad Mini',-- Nome
  'iPad com tela retina display', -- descrição
  6666.26, --preco
  5, --quantidade
  3 -- id do fabricante Apple / fk
);

```

## SELECT(produtos)

```sql

SELECT * FROM `produtos`;

```

## Exercicio 3

INSERT INTO fabricantes(nome) VALUES('Positivo'), ('Microsoft');

INSERT INTO produtos(nome, descricao, preco, quantidade, fabricante_id)
VALUES(
'Xbox Series S',
'Velocidade e desempenho de última geração.',
1997.00,
5,
8 -- id do fabricante Microsoft / fk
),
(
'Notebook Motion',
'Intel Dual Core 4GB de RAM, 128GB SSD e Tela 14,1 polegadas.',
1213.65,
8,
7 -- id do fabricante Positivo / fk
);

```sql

SELECT * FROM produtos;
SELECT nome, preco FROM produtos;
SELECT preco, nome FROM produtos;

-- Mostrar nome, preco e quantidade
SELECT nome, preco, quantidade FROM produtos WHERE preco < 5000;

-- Mostre nome e descrição somente dos produtos da apple
SELECT nome, descricao FROM produtos WHERE fabricante_id = 3;
```

### Operadores Lógicos: E, OU e NÃO

#### E (AND)

```sql

-- Exibir nome e preco dos produtos que custam entre 2000 e 6000

SELECT nome, preco FROM produtos
WHERE preco >= 2000 AND preco <= 6000;

```

#### OU (OR)

```sql

-- Exibir nome e preco dos produtos que custam entre 2000 e 6000

SELECT nome, descricao FROM produtos
WHERE fabricante_id = 2 OR fabricante_id = 3;
WHERE fabricante_id = 2 || fabricante_id = 3;
WHERE fabricante_id IN(2, 3);

```

#### NÃO (NOT)

```sql

-- nome,descricao, preco de todos os produtos EXCETO da positivo

SELECT nome, preco, descricao FROM produtos
WHERE NOT fabricante_id = 7;
WHERE fabricante_id != 7;

```

## UPDATE(fabricantes)

```sql
-- Trocar o nome da fabricante Asus para Asus do Brasil
UPDATE fabricantes SET nome = "Asus do Brasil" WHERE id = 1;

-- Alterar a quantidade para 10 dos produtos que custam abaixo de 2000 exceto da microsoft
UPDATE produtos SET quantidade = 10 WHERE preco < 2000 AND fabricante_id != 8;
UPDATE produtos SET quantidade = 10 WHERE preco < 2000 AND NOT fabricante_id = 8;
```

## DELETE(fabricantes)

```sql
DELETE FROM fabricantes WHERE id = 4;

```

## SELECT: outras formas de uso

### Classificação/Ordenação

```sql
SELECT nome, preco FROM produtos ORDER BY nome;
SELECT nome, preco FROM produtos ORDER BY preco; -- ordem ascendente (é o padrão)
SELECT nome, preco FROM produtos ORDER BY preco ASC; -- ordem ascendente
SELECT nome, preco FROM produtos ORDER BY preco DESC; -- ordem decrescente

SELECT nome, preco, quantidade FROM produtos WHERE fabricante_id = 5 ORDER BY quantidade;
```

### Operações e funções de agregação

```sql
SELECT SUM(preco) FROM produtos; -- Somando todos os valores da coluna com os preços
SELECT SUM(preco) AS somaTotal FROM produtos;
SELECT SUM(preco) AS "soma total" FROM produtos;
SELECT FORMAT(SUM(preco), 2) AS "soma total" FROM produtos;
SELECT REPLACE(FORMAT(SUM(preco), 2), ",", ".") AS "soma total" FROM produtos;

-- Função de média: AVG (AVERAGE)
SELECT AVG(preco) AS "Média dos precos" FROM produtos;
SELECT ROUND(AVG(preco), 2) AS "Média dos precos" FROM produtos;

-- Função de contagem: COUNT
SELECT COUNT(id) AS "QTD de produtos" FROM produtos;

--conta a quantidade de fabricantes ignorando as duplicidades
SELECT COUNT(DISTINCT fabricante_id) AS "QTD de fabricantes" FROM produtos;

-- Operações matemáticas
SELECT nome, preco, quantidade, (preco * quantidade) as Total FROM produtos;

SELECT produtos.nome, fabricante.nome
FROM produtos JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id

-- Segmentação/Agrupamento de resultados
SELECT fabricante_id, SUM(preco) AS total FROM produtos
GROUP BY fabricante_id;
```

---

## Consultas (Queries) em duas ou mais tabelas relacionadas (JOIN/JUNÇÂO)

### Exibir o nome do produto e o nome do fabricante do produto

```sql
-- SELECT nomeDaTabela1.nomeDaColuna, nomeDaTabela2.nomeDaColuna
SELECT produtos.nome AS Produto, fabricantes.nome AS Fabricante

-- JOIN permite JUNTAR as tabelas no momento do SELECT
FROM produtos JOIN fabricantes

-- ON tabela1.chave_estrangeira = chave_primária
ON produtos.fabricante_id = fabricantes.id
```

### Nome do produto, preço do produto, nome do fabricante ordenados pelo nome do produto e pelo preço

```sql
SELECT produtos.nome AS Produto, produtos.preco AS Preço, fabricantes.nome AS Fabricante
FROM produtos JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id
ORDER BY Produto ASC, Preço DESC;

```

### Fabricante, soma dos preços, Quantidade de produtos POR Fabricante

```sql
SELECT
  fabricantes.nome AS Fabricante,
  SUM(produtos.preco) AS Total,
  COUNT(produtos.fabricante_id) AS "QTD de produtos"
FROM produtos RIGHT JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id
GROUP BY Fabricante
ORDER BY Total;

```