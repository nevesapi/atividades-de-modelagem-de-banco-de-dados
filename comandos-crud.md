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