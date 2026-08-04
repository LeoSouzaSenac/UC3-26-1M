# Exercício 4 — Modelo Lógico de Banco de Dados

## Contexto

No exercício anterior, você criou o **Modelo Entidade-Relacionamento (MER)** do sistema de uma biblioteca.

Agora, transforme esse modelo conceitual em um **Modelo Lógico**, representando como as informações serão organizadas em tabelas.

---

# Sua tarefa

Com base no MER criado no **Exercício 3**, desenvolva o Modelo Lógico do banco de dados da biblioteca.

O modelo deverá apresentar:

* As tabelas;
* As colunas de cada tabela;
* Os tipos de dados;
* As chaves primárias;
* As chaves estrangeiras;
* Os relacionamentos entre as tabelas.

---

# Regras importantes

Considere que:

* As entidades do MER deverão ser transformadas em tabelas;
* O relacionamento entre **Leitor** e **Empréstimo** deverá ser representado por uma chave estrangeira;
* O relacionamento entre **Empréstimo** e **Livro** é do tipo **N:N**;
* O relacionamento N:N deverá ser resolvido com uma tabela associativa, como `emprestimo_livro` ou `item_emprestimo`;
* Todas as tabelas deverão possuir uma chave primária;
* Os tipos de dados deverão ser adequados para cada coluna.

---

# Tabelas mínimas

O modelo deverá conter, no mínimo:

* `leitor`;
* `livro`;
* `emprestimo`;
* uma tabela associativa entre empréstimos e livros.

---

# Ferramenta

O diagrama poderá ser criado utilizando:

* MySQL Workbench;
* brModelo;
* diagrams.net;
* Lucidchart;
* outra ferramenta semelhante.

---

# Entrega

* Exporte o Modelo Lógico em formato **PNG** ou **PDF**;
* Publique o arquivo ou o link nas **Discussões do repositório da turma**;
* Identifique a publicação com o seu nome.
