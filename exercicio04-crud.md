## Exercicio 04

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
