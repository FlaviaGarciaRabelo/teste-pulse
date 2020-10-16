### Questão 2

Dadas as tabelas abaixo, monte as consultas SQL solicitadas:

Tabela 1 - ```autores```  possui mais de 1 milhão de linhas, 
aqui estão as 6 primeiras linhas

| id_autor   | nome_autor |
|------------|------------|
| 123        | autor_1    |
| 124        | autor_2    |
| 125        | autor_3    |
| 126        | autor_4    |
| 127        | autor_5    |
| 128        | autor_6    |
| ...        | ...        |


Tabela 2 - ```livros``` possui mais de 1 milhão de linhas, 
aqui estão as 6 primeiras linhas

| id_livro   | id_autor | copias_vendidas | data_lancamento |
|------------|----------|-----------------|-----------------|
| livro_1    | 123      | 1000            | 29/01/1996      |
| livro_2    | 124      | 300             | 07/01/2001      | 
| livro_3    | 124      | 900             | 19/01/2017      |
| livro_3    | 125      | 1200            | 12/01/2003      |
| livro_3    | 126      | 750             | 22/01/2010      |
| livro_3    | 126      | 3500            | 01/01/1998      |
| ...        | ...      | ...             | ...             |


1. Listar o livro que mais vendeu cópias
	SELECT id_livro 
	FROM livros
	WHERE copias_vendidas = (SELECT MAX(copias_vendidas) 
				 FROM livros)

2. Listar todos os autores com um ou mais livros que venderam mais de 10.000 cópias
	SELECT nome_autor 
	FROM autores JOIN livros
	ON autores.id_autor = livros.id_autor
	WHERE copias_vendidas >= 10000

3. Listar os 3 livros com menor volume de cópias vendidas
	SELECT id_livro
	FROM livros
	ORDER BY copias_vendidas
	LIMIT 3

4. Listar todos os livros publicados entre os anos de 2000 e 2010
	SELECT id_livro
	FROM livros
	WHERE data_lamcamento 
	BETWEEN '2000-01-01'
	AND '2010-12-31'

5. Listar os 3 autores com mais copias vendidas e a quantidade de cópias que cada um vendeu (somando todos seus livros)
	SELECT nome_autor, SUM(copias_vendidas) 
	FROM autores JOIN livros
	ON autores.id_autor = livros.id_autor
	GROUP BY nome_autor
	ORDER BY copias_vendidas DESC
	LIMIT 3
