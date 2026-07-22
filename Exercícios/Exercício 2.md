# Exercício 2 — Planejamento Conceitual de um Banco de Dados

## Contexto

Uma pequena **pet shop** deseja informatizar seu atendimento. Atualmente, todas as informações são registradas em cadernos, o que dificulta encontrar dados sobre clientes, animais e serviços realizados.

Você foi contratado para realizar o **planejamento inicial do banco de dados**. O objetivo é organizar as informações que serão armazenadas, preparando a estrutura que será utilizada nas próximas aulas.

---

# Requisitos Funcionais

O sistema deverá ser capaz de:

1. Cadastrar clientes.
2. Cadastrar os animais de cada cliente.
3. Registrar os serviços realizados (banho, tosa, consulta etc.).
4. Registrar a data e o valor de cada atendimento.
5. Consultar o histórico de atendimentos de cada animal.
6. Identificar quais animais possuem atendimentos agendados.

---

# Sua tarefa

Crie uma planilha no **Excel** contendo as seguintes abas:

## Aba 1 — Requisitos Funcionais

Copie os requisitos apresentados acima em uma tabela.

|  Nº | Requisito Funcional |
| :-: | ------------------- |
|  1  | Cadastrar clientes  |
|  2  | ...                 |

---

## Aba 2 — Possíveis Tabelas

Com base nos requisitos, identifique quais tabelas serão necessárias para armazenar as informações do sistema.

Utilize a estrutura abaixo como modelo:

| Tabela  | Descrição                      |
| ------- | ------------------------------ |
| Cliente | Pessoa responsável pelo animal |
| ...     | ...                            |

---

## Aba 3 — Dicionário de Dados

Para cada tabela identificada, liste os campos que ela deverá possuir.

Utilize o modelo abaixo:

| Tabela  | Campo | Tipo  | Tamanho | Descrição                |
| ------- | ----- | ----- | :-----: | ------------------------ |
| Cliente | nome  | Texto |   100   | Nome completo do cliente |

> **Observação:** Não existe uma única resposta correta. O importante é que os campos façam sentido para o sistema proposto.

---

## Aba 4 em diante — Tabelas

Com base no planejamento realizado, crie uma aba para cada tabela identificada.

Cada aba deve conter:

* Os nomes das colunas (campos);
* Pelo menos **5 registros fictícios**, preenchidos com dados coerentes.

Exemplo:

| id_usuario | nome            | email                                       | senha  |
| ---------- | --------------- | ------------------------------------------- | ------ |
| 1          | Fulano de Souza | [fulano@gmail.com](mailto:fulano@gmail.com) | 123456 |
| 2          | Maria Oliveira  | [maria@gmail.com](mailto:maria@gmail.com)   | 654321 |

---

# Entrega

* Publique o arquivo ou o link nas **Discussões do repositório da turma**, conforme orientado em aula, com o seu nome.
