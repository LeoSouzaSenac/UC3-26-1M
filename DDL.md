# DDL - Como começar a trabalhar com o banco usando comandos

## DDL significa `Data Definition Language`, que em português significa `Linguagem de Definição de Dados`, ou seja, são os comandos que CRIAM o nosso banco.

### Passo 1 - Entrando no Workbench
Primeiro, antes de tudo, abra o MySQL Workbench. É nele que vamos inserir nossos comandos.
Em MySQL Connections, clique em Local Instance e digite a senha (a senha padrão é `root`).

### Passo 2 - Criando um novo banco
Para criar um novo banco de dados, você deve usar o comando `CREATE DATABASE nome_do_banco;`.
> NÃO ESQUEÇA: O PONTO E VÍRGULA NO FINAL (;) É OBRIGATÓRIO!

Para rodar o comando, selecione toda a linha que você digitou e aperte `ctrl` + `enter`, ou selecione o botão com o símbolo de um raio.
Você saberá que o comando foi executado com sucesso se aparecer uma mensagem com um ✅.
Para ver o banco criado, procure pelo símbolo que é um círculo feito por duas setas. Clique nele e ele atualiza a visualização dos bancos.

> Para fazer cometários usamos `-- Seu comentário`

## Passo 3 - Criando as nossas tabelas
Agora que já criamos o banco, precisamos criar as tabelas dentro dele. Para isso, primeiro precisamos informar ao workbench em qual banco vamos trabalhar (pois podem haver vários).

Você pode fazer isso clicando duas vezes rapidamente no nome do banco até ele ficar em **negrito** ou colocar, na primeira linha dos seus comandos isto aqui: `USE nome_do_banco;`, que indica qual banco está sendo usado.

Para criarmos uma tabela, usamos o comando 

```sql
    CREATE TABLE IF NOT EXISTS bicicletas(
        -- cria uma coluna chamada 'id_bicicleta'
        -- o TIPO dela é INT (pois é um número inteiro)
        -- ela é a CHAVE PRIMÁRIA desta tabela (por isso o PRIMARY KEY)
        -- ela vai ser criada automaticamente pelo banco (por isso o AUTO_INCREMENT)
        id_bicicleta INT PRIMARY KEY AUTO_INCREMENT,
        -- VARCHAR(50) cria uma coluna de texto que pode ter ATÉ 50 caracteres (pode ir até 255)
        modelo VARCHAR(50) NOT NULL,
        preco DECIMAL(10,2) NOT NULL
    );
```

Isso se traduz para *criar tabela chamada 'nome_da_tabela' se ela já não existir*


### Tente você mesmo(a): Crie a tabela de clientes da loja de bicicletas. Use o mesmo tipo de comando que aprendemos agora (CREATE TABLE etc etc) com as colunas de acordo com o que já havíamos planejado. O nome da tabela deve ser 'clientes'. Não se esqueça: use o mesmo padrão de nomeação que usamos para a tabela 'bicicletas': por exemplo, não use apenas 'id'. Use 'id_cliente'.

```sql
    CREATE TABLE IF NOT EXISTS clientes (
        id_cliente INT PRIMARY KEY AUTO_INCREMENT,
        nome VARCHAR(100) NOT NULL,
        telefone VARCHAR(11),
        endereco VARCHAR(50)
    )
```

### PASSO 4 - Tabelas com CHAVES ESTRANGEIRAS
Para criarmos uma chave estrangeira (FOREIGN KEY) precisamos de um comando específico.
Vamos então criar a tabela 'vendas', que liga com 'clientes', deste modo:

```sql
    CREATE TABLE IF NOT EXISTS vendas(
        id_venda INT PRIMARY KEY AUTO_INCREMENT,
        id_cliente INT NOT NULL,
        FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
    );
```
No exemplo acima, logo após criarmos a coluna `id_cliente`, usamos o comando `FOREIGN KEY`. O `(id_cliente)` indica qual a coluna que é nossa chave estrangeira. O `REFERENCES clientes(id_clientes)` indica com qual tabela (clientes) e em qual coluna desta tabela (id_clientes) estamos fazendo a ligação. Sempre crie todas as colunas primeiro e só final crie todas as foreign keys.

### Tente você mesmo(a): agora você deve criar a tabela itens_vendas. Utilize o que você aprendeu sobre foreign keys. Lembre-se: nesta tabela são 2 foreign keys diferentes. Crie primeiro as colunas e só depois crie as chaves estrangeiras.


```sql
    CREATE TABLE IF NOT EXISTS itens_vendas (
	id_itens_venda INT PRIMARY KEY AUTO_INCREMENT,
    id_venda INT NOT NULL,
    id_bicicleta INT NOT NULL,
    quantidade INT NOT NULL DEFAULT 1,
    FOREIGN KEY (id_venda) REFERENCES vendas(id_venda),
    FOREIGN KEY (id_bicicleta) REFERENCES bicicletas(id_bicicleta)
);
```

### PASSO 5 - Como alterar tabelas já criadas

Pense só, criamos nossas tabelas mas aí vem o pensamento: "puts, clientes devem ter CPF, mas eu não criei essa coluna. E agora?". Calma, gafanhoto, tem solução, e ela se chama `ALTER TABLE`. Este comando nos permite alterar nossas tabelas. Podemos trocar o nome, criar colunas novas, etc etc.

#### Alterar e adicionar uma coluna nova:
```sql
    ALTER TABLE nome_da_tabela ADD COLUMN nome_da_coluna TIPO;
```

```sql
    ALTER TABLE clientes ADD COLUMN cpf VARCHAR(11) NOT NULL UNIQUE;
```

### Alterar e mudar o tipo e/ou o tamanho de uma coluna
```sql
    ALTER TABLE nome_da_tabela MODIFY COLUMN nome_da_coluna TIPO;
```

```sql
    ALTER TABLE clientes MODIFY COLUMN nome VARCHAR(150);
```

### Alterar e renomear uma coluna
```sql
    ALTER TABLE nome_da_tabela RENAME COLUMN nome_antigo_da_coluna TO nome_novo_da_coluna;
```

```sql
    ALTER TABLE itens_vendas RENAME COLUMN quantidade TO qtd;
```

### Alterar e renomear uma TABELA
```sql
    ALTER TABLE nome_da_tabela RENAME TO nome_novo_da_tabela;
```

```sql
    ALTER TABLE itens_vendas RENAME TO itens;
```

### Alterar e remover uma coluna
```sql
    ALTER TABLE nome_da_tabela DROP COLUMN nome_da_coluna;
```

```sql
    ALTER TABLE clientes DROP COLUMN cpf;
```

> PUTS, ESQUECI DA FOREIGN KEY! E AGORA?

### Alterar e adicionar chaves estrangeiras (foreign keys)
```sql
    ALTER TABLE nome_da_tabela ADD CONSTRAINT nome_da_fk FOREIGN KEY (nome_da_coluna_fk) REFERENCES nome_da_tabela_referenciada(nome_da_coluna_referenciada);
```

```sql
    ALTER TABLE itens_vendas ADD CONSTRAINT fk_vendas FOREIGN KEY (id_venda) REFERENCES vendas(id_venda);
```

## PASSO 6 - Mandando as tabelas de arrasta

Como que fazemos para apagar nossas tabelas? Se criarmos uma tabela que não vamos mais precisar, temos que ter um jeito de mandar ela pro vinagre.

> TEMOS QUE TER CUIDADO, POIS ESTE COMANDO É **IRREVERSÍVEL!**

### Apagar uma tabela inteira:
```sql
    DROP TABLE IF EXISTS nome_da_tabela;
```

```sql
    DROP TABLE IF EXISTS itens;
```

### Apagar um BANCO DE DADOS INTEIRO!:
```sql
    DROP DATABASE IF EXISTS nome_do_coitado;
```

```sql
    DROP DATABASE IF EXISTS loja_bicicleta;
```

