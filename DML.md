# DML - Como inserir, atualizar e deletar informações dentro das tabelas

## DML significa `Data Manipulation Language`, ou `Linguagem de Manipulação de Dados`. Através dela nós conseguimos inserir dados novos, atualizá-los e/ou deletá-los.

### Passo 1 - Como inserir um dado em uma tabela já criada
Para inserir um novo dado, ou seja, uma nova informação, nós usamos o comando INSERT INTO.

```sql
    INSERT INTO nome_da_tabela (nomes_das_colunas) VALUES (valores);
```

```sql
    INSERT INTO livros(titulo, autor, data_lancamento, preco) VALUES (
        "Meu amigo Xablau", "Sir Xablau III", "1999-05-09", 99.99
    );
```

Para criar vários dados de uma vez só, podemos usar o mesmo insert (sem precisar escrever várias vezes):

```sql
    INSERT INTO livros (titulo, autor, data_lancamento, preco) VALUES 
    ("Livro 1", "Autor Tal", "2000-01-12", 110.50),
    ("Livro 2", "Autor Aquele", "1998-01-12", 110.50),
    ("Livro 3", "Autor Qual", "1699-01-12", 110.50);
```

Se uma coluna não estiver marcada com `NOT NULL`, ela é opcional. Por exemplo, `data_lancamento` é opcional e nem todo livro precisa ter uma data quando criarmos ele:

```sql
    INSERT INTO livros (titulo, autor, preco) VALUES (
        "Planeta do Xablau", "Dr. Xablau Lee", 15.45
    );
```

### Passo 2 - Como alterar um dado que já existe (CUIDADO!)
Para alterarmos uma informação que já existe em uma tabela (exemplo: mudar o nome de um livro) nós utilizamos o comando `UPDATE`, sempre junto com a opção `WHERE`.

```sql
    UPDATE nome_da_tabela SET nome_da_coluna = novo_valor WHERE condicao; 
```

```sql
    UPDATE livros SET titulo = "O Inferno de Xablau" WHERE id = 3;
```


