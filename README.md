# MBA - Engenharia de Dados Mackenzie.
## Data Collection & Storage

Este repositório vai abrigar um projeto de modelagem de dados de um database. Tarefa obrigatória para obtenção do grau de MBA em Data Engineer.

# Projeto 

Pense em uma empresa, desenhe as tabelas Relacionais e Multidimensionais

1. Pense no nome do Domínio de informação e da Sigla
2. Pense no modelo de negócio e crie os campos com nomes lógicos e físicos
3. Crie o Glossário de Dados
4. Desenhe as tabelas físicas e lógicas Relacionais com as (Chave _PK_ e campos)
5. Crie as tabelas Fato e Dimensão
6. Crie o Script SQL para criar a tabela FATO (_Extract_/_Data Collection_)

Para essa atividade pode ser utilizado o **Draw.io** para criar os desenhos das tabelas.

## Case

A empresa, o colégio Godai de Ensino, pretende criar um banco de dados onde contenha os dados de seus alunos, professores, disciplinas e notas dos alunos.
Deve ser também criada uma tabela fato para reunir as dimensões.

## 1. Pense no nome do Domínio de Informação e da Sigla

**Domínio da Informação:** Educational
**Sigla:** EDU

## 2. Pense no modelo de negócio e crie os campos com nomes lógicos e físicos

### Alunos

| Lógico             | Físico             | Chave |
|--------------------|--------------------|-------|
| Código do Aluno    | `ID_Aluno`         | PK    |
| Nome do Aluno      | `Nome_Aluno`       |       |
| Data de Nascimento | `Data_Nascimento`  |       |
| Gênero             | `Genero`           |       |
| Endereço do Aluno  | `Endereco`         |       |
| Telefone do Aluno  | `Telefone_Contato` |       |
| Email do Aluno     | `Email_Contato`    |       |
