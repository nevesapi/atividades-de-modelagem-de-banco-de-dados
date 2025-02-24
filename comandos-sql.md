# Comandos SQL - Documentação

## Modela física

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
