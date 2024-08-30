# MBA - Engenharia de Dados Mackenzie.
## Data Collection & Storage

Este repositório vai abrigar um projeto de modelagem de dados. Tarefa obrigatória para obtenção do grau de MBA em Data Engineer.

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

A empresa, o **_Colégio Godai de Ensino_**, pretende criar um banco de dados onde contenha os dados de seus alunos, professores, disciplinas e notas dos alunos.
Deve ser também criada uma tabela fato para reunir as dimensões.

## 1. Pense no nome do Domínio de Informação e da Sigla

**Domínio da Informação:** Educational
**Sigla:** EDU

## 2. Pense no modelo de negócio e crie os campos com nomes lógicos e físicos

### Alunos

| Lógico                      | Físico             | Chave |
|-----------------------------|--------------------|-------|
| Código do Aluno             | `ID_Aluno`         | PK    |
| Nome do Aluno               | `Nome_Aluno`       |       |
| Data de Nascimento do Aluno | `Data_Nascimento`  |       |
| Gênero do Aluno             | `Genero`           |       |
| Endereço do Aluno           | `Endereco`         |       |
| Telefone do Aluno           | `Telefone_Contato` |       |
| Email do Aluno              | `Email_Contato`    |       |

### Professores

| Lógico                          | Físico             | Chave |
|---------------------------------|--------------------|-------|
| Código do Professor             | `ID_Professor`     | PK    |
| Nome do Professor               | `Nome_Professor`   |       |
| Data de Nascimento do Professor | `Data_Nascimento`  |       |
| Gênero do Professor             | `Genero`           |       |
| Endereço do Professor           | `Endereco`         |       |
| Telefone do Professor           | `Telefone_Contato` |       |
| Email do Professor              | `Email_Contato`    |       |

### Disciplinas

| Lógico                  | Físico            | Chave |
|-------------------------|-------------------|-------|
| Código da Disciplina    | `ID_Disciplina`   | PK    |
| Nome da Disciplina      | `Nome_Disciplina` |       |
| Descrição da Disciplina | `Descricao`       |       |
| Carga Horária           | `Carga_Horaria`   |       |
| Código do Professor     | `Endereco`        | FK    |

### Notas

| Lógico               | Físico          | Chave |
|----------------------|-----------------|-------|
| Código da Nota       | `ID_Nota`       | PK    |
| Código do Aluno      | `ID_Aluno`      | FK    |
| Código da Disciplina | `ID_Disciplina` | FK    |
| Nota do Aluno        | `Nota`          |       |
| Data da Avaliação    | `Endereco`      |       |

### Turmas

| Lógico              | Físico                    | Chave |
|---------------------|---------------------------|-------|
| Código da Turma     | `ID_Turma`                | PK    |
| Nome da Turma       | `Nome_Turma`              |       |
| Ano Letivo          | `Ano_Letivo`              |       |
| Código do Professor | `ID_Professor_Orientador` | FK    |

