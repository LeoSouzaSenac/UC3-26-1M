# O que é normalização?

Depois de planejarmos o banco de dados e desenharmos o **Modelo Entidade-Relacionamento (MER)**, chega o momento de organizar as tabelas da melhor forma possível. Esse processo é chamado de **normalização**.

Normalizar significa **reduzir a repetição desnecessária de dados**, evitar inconsistências e facilitar a manutenção do banco de dados. Em outras palavras, é uma forma de garantir que cada informação seja armazenada **no lugar certo**.

Imagine que o telefone de um cliente apareça repetido em dezenas de pedidos. Se esse cliente trocar de telefone, será necessário atualizar todas essas linhas. Além de gerar trabalho, basta esquecer uma delas para que o banco passe a ter informações diferentes para a mesma pessoa.

A normalização procura justamente evitar esse tipo de problema, organizando os dados em tabelas separadas e definindo corretamente seus relacionamentos.

Para isso, existem algumas regras conhecidas como **formas normais**. Nesta aula veremos as três primeiras, que são as mais importantes e as mais utilizadas na prática:

* **1ª Forma Normal (1FN):** elimina grupos de valores repetidos e garante que cada campo armazene apenas um único valor.
* **2ª Forma Normal (2FN):** garante que todos os atributos dependam da chave primária inteira.
* **3ª Forma Normal (3FN):** elimina dependências entre atributos que não fazem parte da chave primária.

Ao final do processo, teremos um banco de dados mais organizado, mais fácil de manter e menos sujeito a erros e inconsistências.


# Situação

Uma loja vende produtos.

Você cria esta tabela:

| id_pedido | cliente | telefone | produto | preço |
| --------- | ------- | -------- | ------- | ----- |
| 1         | Ana     | 9999     | Mouse   | 45    |
| 1         | Ana     | 9999     | Teclado | 120   |
| 2         | João    | 8888     | Monitor | 800   |

Até aqui parece tudo bem.

Mas perceba:

* o nome da Ana aparece duas vezes;
* o telefone aparece duas vezes.

Se ela trocar de telefone, você precisa alterar duas linhas.

Isso é redundância.

---

# 1ª Forma Normal (1FN)

A primeira forma normal fala apenas de **uma coisa**:

> Cada campo deve guardar apenas um valor.

Errado:

| cliente | telefones  |
| ------- | ---------- |
| Ana     | 9999, 8888 |

Tem dois telefones na mesma célula.

Correto:

**Cliente**

| id | nome |
| -- | ---- |
| 1  | Ana  |

**Telefone**

| id | id_cliente | telefone |
| -- | ---------- | -------- |
| 1  | 1          | 9999     |
| 2  | 1          | 8888     |

Agora cada célula possui apenas um valor.

Só isso.

Nada mais.

---

# Agora vem a 2FN

Aqui aparece a tal da **chave composta**.

## O que é uma chave composta?

É quando **dois campos juntos** identificam uma linha.

Por exemplo:

Um pedido pode ter vários produtos.

| id_pedido | id_produto |
| --------- | ---------- |
| 1         | 3          |
| 1         | 8          |
| 1         | 10         |

Nenhum dos dois sozinho identifica uma linha.

Veja:

id_pedido = 1

Aparece três vezes.

id_produto = 3

Também pode aparecer em outros pedidos.

Mas o par

```
(1,3)
```

é único.

Então a chave primária é

```
(id_pedido, id_produto)
```

Isso é uma chave composta.

---

## Onde aparece o problema?

Imagine esta tabela:

| id_pedido | id_produto | nome_produto |
| --------- | ---------- | ------------ |
| 1         | 10         | Mouse        |
| 2         | 10         | Mouse        |
| 3         | 10         | Mouse        |

Perceba:

O nome do produto depende de quê?

Do pedido?

Não.

O Mouse continua sendo Mouse independentemente do pedido.

Ele depende apenas de

```
id_produto
```

Mas a chave da tabela é

```
(id_pedido,id_produto)
```

Ou seja...

o atributo depende só de metade da chave.

Isso viola a 2FN.

---

A solução:

**Produto**

| id_produto | nome  |
| ---------- | ----- |
| 10         | Mouse |

e a tabela de itens fica

| id_pedido | id_produto |
| --------- | ---------- |
| 1         | 10         |
| 2         | 10         |
| 3         | 10         |

Agora está correto.

---

# A 3FN

Aqui o problema é outro.

Imagine esta tabela.

| id_aluno | nome   | id_cidade | cidade        |
| -------- | ------ | --------- | ------------- |
| 1        | Carlos | 15        | Novo Hamburgo |
| 2        | Maria  | 15        | Novo Hamburgo |

A pergunta é:

De onde vem "Novo Hamburgo"?

Do aluno?

Não.

Vem do id da cidade.

```
id_cidade = 15

↓

Novo Hamburgo
```

Então o banco ficou assim:

```
id_aluno
      ↓
id_cidade
      ↓
nome_cidade
```

É uma dependência em cadeia.

Por isso chamamos de **dependência transitiva**.

---

A solução é separar.

**Aluno**

| id_aluno | nome   | id_cidade |
| -------- | ------ | --------- |
| 1        | Carlos | 15        |
| 2        | Maria  | 15        |

**Cidade**

| id_cidade | nome          |
| --------- | ------------- |
| 15        | Novo Hamburgo |

Agora, se a cidade mudar de nome, altera apenas uma linha.

---

# Uma forma fácil de lembrar

* **1FN** → uma célula = um valor.
* **2FN** → se existe chave composta, todos os atributos devem depender da chave inteira.
* **3FN** → um atributo nunca deve depender de outro atributo; todos devem depender diretamente da chave primária.
