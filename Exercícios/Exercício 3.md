# Exercício 3 — Modelo Entidade-Relacionamento (MER)

## Contexto

Uma pequena **biblioteca** deseja informatizar o controle de seus livros e empréstimos. Atualmente, todas as informações são registradas em fichas e cadernos, o que dificulta saber quais livros estão disponíveis, quem realizou cada empréstimo e quais livros ainda não foram devolvidos.

Você foi contratado para criar o **Modelo Entidade-Relacionamento (MER)** do sistema. O objetivo é representar visualmente as entidades, seus atributos, os relacionamentos e as cardinalidades.

---

# Requisitos Funcionais

O sistema deverá ser capaz de:

1. Cadastrar leitores.
2. Cadastrar livros.
3. Registrar os empréstimos realizados.
4. Registrar a data do empréstimo.
5. Registrar a data prevista para devolução.
6. Permitir que um leitor realize nenhum, um ou vários empréstimos.
7. Permitir que um empréstimo contenha um ou vários livros.
8. Permitir que um livro nunca tenha sido emprestado ou participe de vários empréstimos ao longo do tempo.
9. Consultar quais livros estão emprestados.
10. Consultar o histórico de empréstimos de cada leitor.

---

# Sua tarefa

Crie o **Modelo Entidade-Relacionamento (MER)** do sistema da biblioteca.

O diagrama deverá representar:

* As entidades necessárias;
* Os atributos de cada entidade;
* As chaves primárias;
* Os relacionamentos entre as entidades;
* As cardinalidades mínima e máxima de cada relacionamento.

---

# Entidades mínimas

Seu modelo deverá conter, no mínimo, as seguintes entidades:

* **Leitor**
* **Livro**
* **Empréstimo**

Você poderá adicionar outras entidades caso considere necessário.

---

# Atributos

Cada entidade deverá possuir:

* Uma chave primária;
* Pelo menos dois atributos além da chave primária.

Exemplo:

| Entidade   | Possíveis atributos                                     |
| ---------- | ------------------------------------------------------- |
| Leitor     | id_leitor, nome, telefone, email                        |
| Livro      | id_livro, título, autor, ano_publicacao                 |
| Empréstimo | id_emprestimo, data_emprestimo, data_prevista_devolucao |

> **Observação:** Os atributos apresentados são apenas sugestões. Você poderá utilizar outros campos, desde que façam sentido para o sistema.

---

# Relacionamentos

Os relacionamentos deverão possuir nomes que indiquem claramente a ação realizada.

Exemplos:

* Um leitor **realiza** empréstimos.
* Um empréstimo **contém** livros.

Para cada relacionamento, informe corretamente as cardinalidades.

---

# Cardinalidades

Antes de definir as cardinalidades, analise as regras do sistema:

* Um leitor pode nunca ter realizado um empréstimo ou pode realizar vários.
* Cada empréstimo deve ser realizado por um único leitor.
* Um empréstimo deve conter pelo menos um livro e pode conter vários.
* Um livro pode nunca ter sido emprestado ou pode participar de vários empréstimos ao longo do tempo.

---

# Ferramenta

O diagrama poderá ser criado utilizando:

* brModelo;
* diagrams.net;
* Lucidchart;
* outra qualquer outra ferramenta que te permita desenhar o diagrama.

---

# Entrega

* Exporte o diagrama em formato **PNG** ou **PDF**.
* Publique o arquivo ou o link nas **Discussões do repositório da turma**, conforme orientado em aula.
* Identifique a publicação com o seu nome.
