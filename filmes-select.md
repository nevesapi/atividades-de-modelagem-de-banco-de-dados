## Consultas com ORDER BY, JOIN, SELECT, GROUP BY

```sql
-- mostrar Filme e o Gênero do Filme
SELECT
  filmes.titulo AS Titulo,
  generos.nome AS Genero
FROM filmes JOIN generos
ON filmes.generos_id = generos.id
ORDER BY Titulo;

-- mostrar Filme e o Detalhe do Filme
SELECT
  filmes.titulo AS Titulo,
  detalhes.sinopse AS sinopse,
  detalhes.duracao AS Duração
FROM detalhes JOIN filmes
ON detalhes.filme_id = filmes.id
ORDER BY Duração DESC;

-- mostrar Filme Gênero e Detalhe do Filme
SELECT
  filmes.titulo AS Titulo,
  detalhes.sinopse AS sinopse,
  detalhes.duracao AS Duração,
  generos.nome AS Genero
FROM detalhes
JOIN filmes ON detalhes.filme_id = filmes.id
RIGHT JOIN generos ON filmes.generos_id = generos.id
ORDER BY Duração DESC;
```
