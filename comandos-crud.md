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

```sql
-- Definindo gêneros da tabela
INSERT INTO generos(nome) VALUES('Ação'), ('Terror'), ('Ficção Científica');

-- Definindo conteúdo do filme
INSERT INTO filmes(titulo, lancamento, fabricante_id)
VALUES(
  'Vingadores: Ultimato',
  '2019-04-25',
  1 -- id do gênero Ação / fk
),
(
  'Avatar: O Caminho da Água',
  '2022-12-16',
  3 -- id do gênero Ficcção Cientifica / fk
),
(
  'Invocação do Mal',
  '2013-09-13',
  2 -- id do gênero Terror / fk
),

-- Definindo conteúdo dos detalhes
INSERT INTO detalhes(duracao, sinopse, bilheteria, orcamento, filme_id)
VALUES
(
  192,
  'Ambientado mais de uma década após os eventos do primeiro filme, "Avatar: O Caminho da Água" acompanha a família Sully enquanto enfrentam novos desafios e exploram as regiões aquáticas de Pandora',
  2320000000.00,
  250000000.00,
  2 -- id do filme avatar / fk
),
(
  110,
  'Os investigadores paranormais Ed e Lorraine Warren trabalham para ajudar a família aterrorizada por uma entidade demoníaca em sua fazenda.',
  319494638.00,
  356000000.00,
  3 -- id do filme invocação / fk
),

SELECT * FROM `filmes`;
SELECT * FROM `detalhes` WHERE duracao <= 120;

UPDATE filmes SET titulo = 'Invocação do Mal' WHERE generos_id != 1 AND generos_id != 3;

DELETE FROM generos WHERE id = 3;

```
