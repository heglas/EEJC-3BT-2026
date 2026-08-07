# Modelagem ER e Fundamentos de SQL — Atividade Prática

**Disciplina:** Banco de Dados e Computação em Nuvem (BDCN)
**Turma:** EEJC-3BT · Ano letivo 2026
**Professor:** Heglas Oliveira

---

## Objetivos de aprendizagem

Ao final desta atividade você deverá ser capaz de:

- Identificar entidades, atributos e relacionamentos a partir de um cenário descrito em linguagem natural
- Definir chaves primárias, incluindo chaves compostas e chaves parciais de entidades fracas
- Determinar cardinalidades (1:1, 1:N, N:N) e resolver relacionamentos N:N no modelo relacional
- Reconhecer atributos de relacionamento e posicioná-los corretamente
- Aplicar generalização/especialização e modelar auto-relacionamentos
- Revisar conceitos fundamentais de SQL: chaves, normalização, JOINs, agregação e tratamento de NULL

---

## Como entregar

1. Faça os diagramas em [dbdiagram.io](https://dbdiagram.io) ou [draw.io](https://app.diagrams.net) — ou à mão, fotografando com nitidez
2. Escreva também o **mapeamento relacional** em texto, no formato `TABELA(pk, atributo, fk*)`
3. **Justifique por escrito** as decisões de projeto pedidas em cada exercício — a justificativa vale nota
4. Envie um único PDF pelo Google Classroom

### Como você será avaliado

| Critério | Peso |
|---|---|
| Entidades corretamente identificadas | 25% |
| Chaves primárias adequadas | 20% |
| Cardinalidades corretas | 25% |
| Atributos no lugar certo | 20% |
| Justificativa escrita das decisões | 10% |

> Os exercícios 1 e 2 são individuais. Os exercícios 3 e 4 podem ser feitos em duplas. O exercício 5 é um desafio opcional, com pontuação extra.

---

## Parte 1 — Exercícios de Modelagem ER

### Convenções adotadas

- **PK** = chave primária · **FK** = chave estrangeira
- Cardinalidade em notação (min, max) ou 1:1 / 1:N / N:N
- Atributos derivados entre parênteses, multivalorados marcados como tal
- Notação textual: `ENTIDADE(pk, atributo, atributo, fk*)`

---

### Exercício 1 — Biblioteca Escolar (Nível: Básico)

**Cenário**

A biblioteca da escola quer informatizar seu controle de acervo. Cada **livro** tem título, ISBN, ano de publicação e número de páginas. Cada livro pertence a uma única **editora** (nome, cidade, CNPJ). Cada livro pode ter vários **exemplares** físicos, identificados por um número de tombo, com estado de conservação e data de aquisição. Os **alunos** (RA, nome, série, e-mail) realizam **empréstimos** de exemplares, registrando data de retirada, data prevista de devolução e data efetiva de devolução.

**Pede-se:**
1. Identifique entidades, atributos e chaves primárias.
2. Defina os relacionamentos e suas cardinalidades.
3. Desenhe o DER e faça o mapeamento para o modelo relacional.

**Tempo estimado:** 10 min

---

### Exercício 2 — Escola Técnica: Alunos, Cursos e Notas (Nível: Básico/Intermediário)

**Cenário**

Uma escola técnica precisa registrar suas turmas. Um **curso** (código, nome, carga horária) é composto por várias **disciplinas** (código, nome, carga horária). Uma mesma disciplina pode aparecer em mais de um curso. Cada disciplina é ministrada por um ou mais **professores** (matrícula, nome, titulação). Os **alunos** se matriculam em disciplinas e, ao final, recebem **nota** e **frequência** (%) em cada uma. Um aluno pode cursar a mesma disciplina mais de uma vez, em **semestres letivos** diferentes (ex.: 2026.1, 2026.2).

**Pede-se:**
1. Modele o DER completo.
2. Justifique onde os atributos `nota` e `frequência` devem ser armazenados.
3. Explique como o semestre letivo afeta a chave primária da matrícula.

**Tempo estimado:** 12 min

---

### Exercício 3 — E-commerce (Nível: Intermediário)

**Cenário**

Uma loja virtual precisa de um modelo de dados. **Clientes** (CPF, nome, e-mail, telefone) podem cadastrar **vários endereços** de entrega (logradouro, número, CEP, cidade, UF, apelido do endereço). Cada **pedido** é feito por um cliente, tem data/hora, status (`pendente`, `pago`, `enviado`, `entregue`, `cancelado`) e é enviado para **um** dos endereços do cliente. Um pedido contém vários **produtos**, e cada item registra a **quantidade** e o **preço unitário praticado no momento da compra**. Cada produto (SKU, nome, descrição, preço atual, estoque) pertence a uma **categoria**, e as categorias podem ter **subcategorias** (hierarquia). Cada pedido gera **um** pagamento (forma, valor, data, código de autorização).

**Pede-se:**
1. Construa o DER com todas as cardinalidades.
2. Explique por que `preço unitário` aparece no item do pedido e não apenas no produto.
3. Modele a hierarquia de categorias.
4. Faça o mapeamento relacional com PKs e FKs.

**Tempo estimado:** 15 min

---

### Exercício 4 — Clínica Médica com Especialização (Nível: Avançado)

**Cenário**

Uma clínica quer um sistema unificado. Toda **pessoa** cadastrada tem CPF, nome, data de nascimento e telefone. Uma pessoa pode ser **paciente** (número do convênio, plano de saúde) ou **funcionário** (matrícula, data de admissão, salário) — e um funcionário pode ser **médico** (CRM, especialidade) ou **atendente** (turno). Uma pessoa pode ser paciente e funcionário ao mesmo tempo.

**Consultas** são agendadas entre um paciente e um médico, com data/hora, sala e status. Em cada consulta pode ser emitida uma **prescrição**, que lista vários **medicamentos** com dosagem e duração do tratamento. Cada consulta pode solicitar vários **exames** (tipo, data de realização, resultado, laboratório).

**Pede-se:**
1. Modele usando **generalização/especialização**, indicando se é total ou parcial, exclusiva ou sobreposta.
2. Justifique a escolha entre as estratégias de mapeamento da hierarquia para tabelas.
3. Modele a prescrição — entidade forte ou fraca? Justifique.

**Tempo estimado:** 18 min

---

### Exercício 5 — Plataforma de Streaming e Auto-relacionamento (Nível: Avançado / Desafio)

**Cenário**

Uma plataforma de streaming precisa modelar seu catálogo e engajamento. Uma **conta** (e-mail, senha, plano, data de assinatura) possui até 5 **perfis** (nome, avatar, idade, classificação máxima permitida). O catálogo tem **títulos** (id, nome, ano, sinopse, classificação indicativa) que podem ser **filmes** (duração) ou **séries**. Uma série tem **temporadas**, e cada temporada tem **episódios** (número, nome, duração).

**Pessoas** (atores/diretores) participam de títulos exercendo um **papel** (`ator`, `diretor`, `roteirista`) — a mesma pessoa pode ter mais de um papel no mesmo título. Perfis registram **visualizações** com timestamp, minuto de parada e dispositivo. Perfis também podem **seguir** outros perfis da plataforma. Cada título pode ser **recomendado** por conta de similaridade com outro título, com um grau de similaridade (0 a 1).

**Pede-se:**
1. Modele entidades fracas (temporada/episódio) com chaves parciais.
2. Modele os dois **auto-relacionamentos** (perfil segue perfil; título similar a título).
3. Modele o relacionamento N:N com atributo `papel` e explique por que ele entra na chave.
4. Aponte pelo menos **duas** decisões de projeto onde havia mais de uma solução válida.

**Tempo estimado:** 20 min

---

## Parte 2 — Quiz de Revisão: Fundamentos de BD e SQL

> Quiz aplicado em aula. Marque sua resposta e aguarde a correção comentada. Use-o também como roteiro de estudo para a avaliação bimestral.

---

**Q1.** Qual a diferença fundamental entre chave primária e chave única (UNIQUE)?

A) Não há diferença, são sinônimos
B) A chave primária não aceita NULL e há apenas uma por tabela; UNIQUE aceita NULL e pode haver várias
C) UNIQUE não aceita valores repetidos, a chave primária aceita
D) A chave primária só pode ser numérica

---

**Q2.** Uma tabela `FUNCIONARIO(matricula, nome, cod_depto, nome_depto)` onde `nome_depto` depende de `cod_depto`, que não é chave. Qual forma normal está violada?

A) 1FN
B) 2FN
C) 3FN
D) Nenhuma, a tabela está normalizada

---

**Q3.** Qual o resultado de `SELECT COUNT(*), COUNT(comissao) FROM VENDEDOR;` numa tabela com 10 linhas, onde 4 vendedores têm `comissao` NULL?

A) 10, 10
B) 10, 6
C) 6, 6
D) 10, 4

---

**Q4.** Um `INNER JOIN` entre CLIENTE e PEDIDO retorna:

A) Todos os clientes, com ou sem pedidos
B) Todos os pedidos, mesmo os sem cliente
C) Apenas clientes que possuem ao menos um pedido
D) Todos os clientes e todos os pedidos combinados

---

**Q5.** Qual cláusula filtra o resultado **depois** de um agrupamento com `GROUP BY`?

A) WHERE
B) HAVING
C) ORDER BY
D) LIMIT

---

**Q6.** Uma relação N:N entre ALUNO e DISCIPLINA no modelo relacional é implementada como:

A) Uma FK em ALUNO apontando para DISCIPLINA
B) Uma FK em DISCIPLINA apontando para ALUNO
C) Uma tabela associativa com FKs para as duas tabelas
D) Um campo multivalorado na tabela ALUNO

---

**Q7.** No ACID, o que garante a propriedade **Atomicidade**?

A) Que os dados nunca se perdem após uma falha de energia
B) Que transações concorrentes não interferem entre si
C) Que uma transação é executada por completo ou não é executada de forma alguma
D) Que as restrições de integridade são sempre respeitadas

---

**Q8.** Qual comando remove todas as linhas de uma tabela mantendo sua estrutura, sem gerar log linha a linha?

A) DELETE FROM tabela
B) DROP TABLE tabela
C) TRUNCATE TABLE tabela
D) ALTER TABLE tabela

---

**Q9.** Numa entidade fraca, a chave primária é formada por:

A) Apenas seu próprio atributo identificador
B) A chave da entidade proprietária combinada com sua chave parcial
C) Um número sequencial gerado automaticamente
D) Nenhum atributo — entidades fracas não têm chave

---

**Q10.** Qual das consultas abaixo retorna corretamente os clientes que **nunca** fizeram pedidos?

A) `SELECT * FROM cliente c INNER JOIN pedido p ON c.id = p.cliente_id;`
B) `SELECT * FROM cliente WHERE id != (SELECT cliente_id FROM pedido);`
C) `SELECT c.* FROM cliente c LEFT JOIN pedido p ON c.id = p.cliente_id WHERE p.id IS NULL;`
D) `SELECT * FROM cliente WHERE id NOT IN (SELECT * FROM pedido);`

---


---

## Para estudar mais

- **Diagramar online:** [dbdiagram.io](https://dbdiagram.io) — escreve o DER em código e gera o diagrama
- **Praticar SQL no navegador:** [SQLite Online](https://sqliteonline.com) e [DB Fiddle](https://www.db-fiddle.com)
- **Documentação PostgreSQL em português:** [postgresql.org/docs](https://www.postgresql.org/docs/current/tutorial-sql.html)
- **Supabase** — usado em aula para a parte de computação em nuvem: [supabase.com/docs](https://supabase.com/docs)

### Checklist de autoavaliação antes de entregar

- [ ] Toda entidade tem uma chave primária definida?
- [ ] Nenhum atributo multivalorado ficou dentro de uma tabela (violação da 1FN)?
- [ ] Todo relacionamento N:N foi transformado em tabela associativa?
- [ ] Os atributos de relacionamento (nota, quantidade, preço, papel) estão na tabela associativa, e não nas entidades?
- [ ] As cardinalidades estão marcadas nos dois lados de cada relacionamento?
- [ ] Escrevi as justificativas pedidas em cada exercício?

---

*Dúvidas: traga na próxima aula ou registre no mural do Google Classroom.*
