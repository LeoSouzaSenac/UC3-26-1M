# MER

Este documento descreve o que é o MER e como e porque utilizá-lo.

## O que é o MER?

O MER é a sigla para Modelo Entidade Relacionamento. Ele é, basicamente, um **desenho** representando o nosso banco de dados e como nossas **entidades** (que serão nossas tabelas depois) se ligam e se **relacionam**.

## Porque preciso fazer esse desenho? Não é mais fácil só fazer o banco?

É sim possível criar o banco sem fazer o MER. Porém, o MER faz parte do *planejamento* do nosso banco de dados. É como fazer um prédio sem desenhar a planta antes. É possível, mas garanto que você não ia querer morar nele.

Ao fazer o MER, nós estamos cuidando para que nosso banco saia exatamente como necessário, sem mais nem menos. Assim, evitamos retrabalho lá na frente.

## Onde e como eu posso fazer este desenho?

O MER pode ser feito em qualquer plataforma ou programa que permita desenhar. Existem programas específicos para trabalhar com ele, mas você pode usar até mesmo o Canva, o Photoshop, o Paint ou até mesmo numa folha de papel. No entanto, eu recomendo utilizar os programas específicos como o BrModelo: 

- https://www.brmodeloweb.com/

## Qual o passo a passo para desenharmos?

Antes de fazermos o MER precisamos primeiro ter definido quais as **entidades** (tabelas) e ter feito o **dicionário de dados** (aquela lista que define os campos e os tipos de dados destes campos). Então, podemos começar desenhando as entidades no MER. Elas são representadas por *retângulos* com o nome dentro.

Os **atributos** que nós planejamos anteriormente para estas **entidades** também devem aparecer no desenho (assim sabemos como construir as tabelas depois só de olhar o desenho). Eles são representados por bolinhas sem fundo, ou "brancas".

**ATENÇÃO:** se um atributo for uma **chave primária** ele será representado por uma bolinha preenchida, ou "preta".

Ambas devem estar ligadas às entidades (retângulos) por **linhas**.

## Relacionamentos

Para podermos criar as **chaves estrangeiras**, que são os campos que ligam uma tabela em outra, normalmente pegando emprestado a **chave primária** de outra tabela. Não usamos "bolinhas" para representá-las, e sim **losangos** com linhas ligando as entidades em questão. Dentro deste losango, damos um título para a relação. Por exemplo, um **aluno** *pertence* à uma **turma**, ou então um **cliente** *compra* uma **bicicleta**. 

Um passo importante para entender os relacionamentos é a **cardinalidade**. Ela nos ajuda a entender quantos registros dentro de uma tabela conseguem se relacionar com quantos de outra tabela. Confuso?

Pense só: em quantas vendas uma bicicleta pode estar? Uma só. Note que eu usei a palavra *pode*, pois uma bicicleta pode não ter sido vendida ainda.

Agora, uma venda pode ter quantas bicicletas? Várias, correto? 

Um cliente pode fazer várias compras, quantas ele quiser. Pode também não fazer nenhuma.

### Tipos de cardinalidade

* **(0,1)** - Pode não participar de nenhum relacionamento ou participar de apenas um.
  *Exemplo: Um funcionário pode ou não ter um carro da empresa.*

* **(1,1)** - Deve participar de exatamente um relacionamento.
  *Exemplo: Todo empréstimo deve estar associado a um único cliente.*

* **(0,N)** - Pode não participar de nenhum relacionamento ou participar de vários.
  *Exemplo: Um cliente pode nunca fazer um empréstimo ou fazer vários ao longo do tempo.*

* **(1,N)** - Deve participar de pelo menos um relacionamento, mas pode participar de vários.
  *Exemplo: Um empréstimo deve conter pelo menos uma bicicleta, mas pode conter várias.*

* **(N,N)** - Ambos os lados podem participar de vários relacionamentos. Também é chamado de relacionamento muitos-para-muitos.
  *Exemplo: Um aluno pode cursar várias disciplinas, e uma disciplina pode ter vários alunos.*

### Resumindo

* **0** = opcional (pode não existir)
* **1** = obrigatório (deve existir)
* **N** = muitos (vários)

Então:

* **(0,1)** → opcional e no máximo um.
* **(1,1)** → obrigatório e exatamente um.
* **(0,N)** → opcional e vários.
* **(1,N)** → obrigatório e vários.



## Tabelas auxiliares (ou tabelas de associação)

Em alguns casos, duas entidades podem se relacionar de forma que **vários registros de uma possam estar ligados a vários registros da outra**. Esse tipo de relacionamento é chamado de **muitos-para-muitos (N:N)**.

Porém, bancos de dados relacionais **não implementam diretamente** esse tipo de relacionamento. Para resolver esse problema, criamos uma **tabela auxiliar**, também chamada de **tabela de associação**.

Essa tabela fica entre as duas entidades e guarda as ligações entre elas.

### Exemplo

Imagine um sistema de vendas.

Um **pedido** pode conter vários **produtos**.

Um **produto** pode aparecer em vários **pedidos**.

Perceba que ambos os lados possuem cardinalidade **N** (N,N)

Nesse caso, criamos uma tabela chamada **ItemPedido**.

Ela ficará responsável por dizer quais produtos pertencem a cada pedido.

```
Pedido -------- ItemPedido -------- Produto
```

A tabela **ItemPedido** normalmente possui:

* id_pedido
* id_produto
* quantidade
* valor_unitario
* desconto (se necessário)

Observe que, além de ligar as duas tabelas, ela também pode armazenar informações próprias da relação, como a quantidade comprada de cada produto.

## Como saber quando criar uma tabela auxiliar?

Sempre faça a seguinte pergunta:

> **Os dois lados podem ter vários registros relacionados entre si?**

Se a resposta for **sim**, provavelmente será necessária uma tabela auxiliar.

Veja alguns exemplos.

| Entidade A                 | Entidade B                                                                          | Precisa de tabela auxiliar? |
| -------------------------- | ----------------------------------------------------------------------------------- | --------------------------- |
| Cliente × Pedido           | Não. Um cliente faz vários pedidos, mas cada pedido pertence a um único cliente.    | Não                         |
| Pedido × Produto           | Sim. Um pedido possui vários produtos e um produto pode aparecer em vários pedidos. | Sim                         |
| Aluno × Disciplina         | Sim. Um aluno cursa várias disciplinas e cada disciplina possui vários alunos.      | Sim                         |
| Médico × Paciente          | Sim. Um médico atende vários pacientes e um paciente pode consultar vários médicos. | Sim                         |
| Funcionário × Departamento | Não. Normalmente um funcionário pertence a um único departamento.                   | Não                         |

### Regra prática

Sempre que encontrar uma relação **N:N**, crie uma tabela auxiliar para representá-la.

Ela transformará o relacionamento em dois relacionamentos **1:N**, que podem ser implementados normalmente no banco de dados.

```
Pedido (1) -------- (N) ItemPedido (N) -------- (1) Produto
```

Dessa forma, o banco de dados consegue representar corretamente quais produtos fazem parte de cada pedido, quais alunos cursam cada disciplina e qualquer outro relacionamento muitos-para-muitos.

