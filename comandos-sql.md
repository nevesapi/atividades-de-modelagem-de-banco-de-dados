# Comandos SQL - Documentação

## Modelagem física

Neste arquivo está a referência de comandos usando a estruturação do banco de dados MySQL/MariaDB.

### Criar banco de dados

```sql
CREATE DATABSE nomeDoBanco CHARACTER SET utf8mb4;
```

### Criar tabela de Fabricante

```sql
CREATE TABLE nomeDaTabela(
  id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(50) NOT NULL,
);
```

### Visualizar detalhes estruturais da tabela

```sql
DESC nomeDaTabela;
```

### Criar tabela de Produtos

```sql
CREATE TABLE nomeDaTabela(
  id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(50) NOT NULL,
  descricao TEXT(500) NULL,
  preco DECIMAL(6,2) NOT NULL,
  fabricante_id INT NOT NULL -- SERÁ CHAVE ESTRANGEIRA
);
```

### Criar relacionamento entre as tableas e configurar a chave estrangeira

```sql
ALTER TABLE nomeDaTabela
-- Adicionando uma restrição indicando o nome do relacionamento
  ADD CONSTRAINT fk_produtos_fabricantes

  -- Criando a chave-estrangeira (fabricante_id) que
  -- aponta para a chave-primaria (id) de outra tabela (fabricantes)
  FOREIGN KEY (fabricante_id) REFERENCES fabricantes(id);
```

### Exemplo de alterações estruturais em tabelas

#### Adicionar coluna

```sql
ALTER TABLE produtos ADD quantidade INT NULL AFTER preco;
```

#### Renomear tabela

```sql
ALTER TABLE fabricantes RENAME TO fornecedores;
```

#### Renomear coluna

```sql
ALTER TABLE fabricantes CHANGE descricao detalhes TEXT(500) NULL;
```
