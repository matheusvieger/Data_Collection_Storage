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

<img src="Godai_Logo.webp" alt="Logo do Colégio Godai de Ensino" width="30%"/>

A empresa, o **_Colégio Godai de Ensino_**, pretende criar um banco de dados onde contenha os dados de seus alunos, professores, disciplinas dos alunos.
Deve ser também criada uma tabela fato para reunir as dimensões, apresentando as notas dos alunos.

## 1. Pense no nome do Domínio de Informação e da Sigla

**Domínio da Informação:** Educational
**Sigla:** EDU

## 2. Pense no modelo de negócio e crie os campos com nomes lógicos e físicos

### Alunos

| Campo           | Tipo          | Atributos                        | Descrição                              |
|-----------------|---------------|----------------------------------|----------------------------------------|
| `aluno_id`      | INT           | PRIMARY KEY, AUTO_INCREMENT       | Identificador único do aluno.          |
| `nome`          | VARCHAR(100)  | NOT NULL                           | Nome completo do aluno.                |
| `data_nascimento` | DATE        | NOT NULL                           | Data de nascimento do aluno.           |
| `ano_matricula` | INT           | NOT NULL                           | Ano em que o aluno foi matriculado.    |
| `turma_id`      | INT           | FOREIGN KEY                        | Referência para a tabela `Turmas`.     |


### Responsáveis

| Campo           | Tipo          | Atributos                          | Descrição                                  |
|-----------------|---------------|------------------------------------|--------------------------------------------|
| `responsavel_id`| INT           | PRIMARY KEY, AUTO_INCREMENT        | Identificador único do pai/mãe/responsável.|
| `nome`          | VARCHAR(100)  | NOT NULL                           | Nome completo do pai/mãe.                  |
| `aluno_id`      | INT           | FOREIGN KEY                        | Referência para a tabela `Alunos`.         |


### Pesquisas de Satisfação
| Campo                       | Tipo          | Atributos                          | Descrição                                         |
|-----------------------------|---------------|------------------------------------|---------------------------------------------------|
| `pesquisa_id`               | INT           | PRIMARY KEY, AUTO_INCREMENT        | Identificador único da pesquisa.                  |
| `data_pesquisa`             | DATE          | NOT NULL                           | Data em que a pesquisa foi realizada.             |
| `aluno_id`                  | INT           | FOREIGN KEY                        | Referência para a tabela `Alunos`.                |
| `responsavel_id`            | INT           | FOREIGN KEY                        | Referência para a tabela `Responsáveis`.          |
| `satisfacao_geral`          | INT           | NOT NULL                           | Nota de satisfação geral (1 a 10).                |
| `satisfacao_ensino`         | INT           | NOT NULL                           | Nota de satisfação com o ensino (1 a 10).         |
| `satisfacao_infraestrutura` | INT           | NOT NULL                           | Nota de satisfação com a infraestrutura (1 a 10). |
| `satisfacao_comunicacao`    | INT           | NOT NULL                           | Nota de satisfação com a comunicação (1 a 10).    |
| `comentarios`               | TEXT          | NULLABLE                           | Feedback qualitativo sobre a pesquisa.            |


### Exames

| Campo          | Tipo          | Atributos                        | Descrição                              |
|----------------|---------------|----------------------------------|----------------------------------------|
| `exame_id`     | INT           | PRIMARY KEY, AUTO_INCREMENT       | Identificador único do exame.          |
| `data_exame`   | DATE          | NOT NULL                           | Data em que o exame foi realizado.     |
| `tipo_exame`   | VARCHAR(50)   | NOT NULL                           | Tipo do exame (nacional, internacional, etc.). |
| `ano`          | INT           | NOT NULL                           | Ano em que o exame foi realizado.      |

### Desempenho_Alunos

| Campo           | Tipo          | Atributos                        | Descrição                              |
|-----------------|---------------|----------------------------------|----------------------------------------|
| `desempenho_id` | INT           | PRIMARY KEY, AUTO_INCREMENT       | Identificador único do desempenho.     |
| `aluno_id`      | INT           | FOREIGN KEY                        | Referência para a tabela `Alunos`.     |
| `exame_id`      | INT           | FOREIGN KEY                        | Referência para a tabela `Exames`.     |
| `nota`          | DECIMAL(5, 2) | NOT NULL                           | Nota obtida no exame.                  |

#### Atividades_Extracurriculares

| Campo            | Tipo          | Atributos                        | Descrição                              |
|------------------|---------------|----------------------------------|----------------------------------------|
| `atividade_id`   | INT           | PRIMARY KEY, AUTO_INCREMENT       | Identificador único da atividade.      |
| `nome_atividade` | VARCHAR(100)  | NOT NULL                           | Nome da atividade extracurricular.     |
| `descricao`      | TEXT          | NULLABLE                           | Descrição da atividade.                |

#### Participacao_Atividades

| Campo                | Tipo          | Atributos                        | Descrição                              |
|----------------------|---------------|----------------------------------|----------------------------------------|
| `participacao_id`    | INT           | PRIMARY KEY, AUTO_INCREMENT       | Identificador único da participação.   |
| `aluno_id`           | INT           | FOREIGN KEY                        | Referência para a tabela `Alunos`.     |
| `atividade_id`       | INT           | FOREIGN KEY                        | Referência para a tabela `Atividades_Extracurriculares`. |
| `data_participacao`  | DATE          | NOT NULL                           | Data da participação na atividade.     |

#### Turmas

| Campo          | Tipo          | Atributos                        | Descrição                              |
|----------------|---------------|----------------------------------|----------------------------------------|
| `turma_id`     | INT           | PRIMARY KEY, AUTO_INCREMENT       | Identificador único da turma.          |
| `ano`          | INT           | NOT NULL                           | Ano letivo da turma.                   |
| `descricao`    | VARCHAR(50)   | NOT NULL                           | Descrição da turma (ex.: 1º ano, 2º ano). |


## 3. Crie o Glossário de Dados

| Tabela                      | Campo                       | Tipo            | Atributos                        | Descrição                                                        | Tipo de Tabela  |
|-----------------------------|-----------------------------|-----------------|----------------------------------|------------------------------------------------------------------|-----------------|
| **Alunos**                  | `aluno_id`                  | INT             | PRIMARY KEY, AUTO_INCREMENT       | Identificador único do aluno.                                    | Dimensão        |
|                             | `nome`                      | VARCHAR(100)    | NOT NULL                           | Nome completo do aluno.                                          | Dimensão        |
|                             | `data_nascimento`           | DATE            | NOT NULL                           | Data de nascimento do aluno.                                     | Dimensão        |
|                             | `ano_matricula`             | INT             | NOT NULL                           | Ano em que o aluno foi matriculado.                              | Dimensão        |
|                             | `turma_id`                  | INT             | FOREIGN KEY                        | Referência para a tabela `Turmas`.                               | Dimensão        |
| **Responsáveis**        | `responsavel_id`                    | INT             | PRIMARY KEY, AUTO_INCREMENT       | Identificador único do pai/mãe.                                  | Dimensão        |
|                             | `nome`                      | VARCHAR(100)    | NOT NULL                           | Nome completo do pai/mãe.                                        | Dimensão        |
|                             | `aluno_id`                  | INT             | FOREIGN KEY                        | Referência para a tabela `Alunos`.                               | Dimensão        |
| **Pesquisas_Satisfacao**    | `pesquisa_id`               | INT             | PRIMARY KEY, AUTO_INCREMENT       | Identificador único da pesquisa.                                 | Fato            |
|                             | `data_pesquisa`             | DATE            | NOT NULL                           | Data em que a pesquisa foi realizada.                            | Fato            |
|                             | `aluno_id`                  | INT             | FOREIGN KEY                        | Referência para a tabela `Alunos`.                               | Fato            |
|                             | `responsavel_id`                    | INT             | FOREIGN KEY                        | Referência para a tabela `Responsáveis`.                                 | Fato            |
|                             | `satisfacao_geral`          | INT             | NOT NULL                           | Nota de satisfação geral (1 a 10).                               | Fato            |
|                             | `satisfacao_ensino`         | INT             | NOT NULL                           | Nota de satisfação com o ensino (1 a 10).                        | Fato            |
|                             | `satisfacao_infraestrutura` | INT             | NOT NULL                           | Nota de satisfação com a infraestrutura (1 a 10).                 | Fato            |
|                             | `satisfacao_comunicacao`    | INT             | NOT NULL                           | Nota de satisfação com a comunicação (1 a 10).                   | Fato            |
|                             | `comentarios`               | TEXT            | NULLABLE                           | Feedback qualitativo sobre a pesquisa.                           | Fato            |
| **Exames**                  | `exame_id`                  | INT             | PRIMARY KEY, AUTO_INCREMENT       | Identificador único do exame.                                    | Dimensão        |
|                             | `data_exame`                | DATE            | NOT NULL                           | Data em que o exame foi realizado.                               | Dimensão        |
|                             | `tipo_exame`                | VARCHAR(50)     | NOT NULL                           | Tipo do exame (nacional, internacional, etc.).                   | Dimensão        |
|                             | `ano`                       | INT             | NOT NULL                           | Ano em que o exame foi realizado.                                | Dimensão        |
| **Desempenho_Alunos**       | `desempenho_id`            | INT             | PRIMARY KEY, AUTO_INCREMENT       | Identificador único do desempenho.                               | Fato            |
|                             | `aluno_id`                 | INT             | FOREIGN KEY                        | Referência para a tabela `Alunos`.                               | Fato            |
|                             | `exame_id`                 | INT             | FOREIGN KEY                        | Referência para a tabela `Exames`.                               | Fato            |
|                             | `nota`                     | DECIMAL(5, 2)   | NOT NULL                           | Nota obtida no exame.                                            | Fato            |
| **Atividades_Extracurriculares** | `atividade_id`        | INT             | PRIMARY KEY, AUTO_INCREMENT       | Identificador único da atividade.                                | Dimensão        |
|                             | `nome_atividade`            | VARCHAR(100)    | NOT NULL                           | Nome da atividade extracurricular.                               | Dimensão        |
|                             | `descricao`                 | TEXT            | NULLABLE                           | Descrição da atividade.                                          | Dimensão        |
| **Participacao_Atividades** | `participacao_id`           | INT             | PRIMARY KEY, AUTO_INCREMENT       | Identificador único da participação.                             | Fato            |
|                             | `aluno_id`                  | INT             | FOREIGN KEY                        | Referência para a tabela `Alunos`.                               | Fato            |
|                             | `atividade_id`             | INT             | FOREIGN KEY                        | Referência para a tabela `Atividades_Extracurriculares`.         | Fato            |
|                             | `data_participacao`         | DATE            | NOT NULL                           | Data da participação na atividade.                               | Fato            |
| **Turmas**                  | `turma_id`                  | INT             | PRIMARY KEY, AUTO_INCREMENT       | Identificador único da turma.                                    | Dimensão        |
|                             | `ano`                       | INT             | NOT NULL                           | Ano letivo da turma.                                             | Dimensão        |
|                             | `descricao`                | VARCHAR(50)     | NOT NULL                           | Descrição da turma (ex.: 1º ano, 2º ano).                        | Dimensão        |

## 4. Desenhe as tabelas físicas e lógicas Relacionais com as (Chave _PK_ e campos)

![relational](./Representations/tab_logic_keys.png)

## 5. Crie as tabelas Fato e Dimensão

### Fato_Notas

| Lógico                   | Físico           | Chave |
|--------------------------|------------------|-------|
| Código da Nota           | `ID_Nota`        |       |
| Código do Aluno          | `ID_Aluno`       | FK    |
| Código do Professor      | `ID_Professor`   | FK    |
| Código da Disciplina     | `ID_Disciplina`  | FK    |
| Código da Turma          | `ID_Turma`       | FK    |
| Nota obtida pelo aluno   | `Valor_Nota`     |       |
| Data da prova da matéria | `Data_Avaliacao` |       |

![relational](./Representations/Fato.png)

## 6. Crie o Script SQL para criar a tabela FATO (_Extract_/_Data Collection_)

Todo o código SQL pode ser visualizado baixando o arquivo disponibilizado no link:

[!<img src="https://thumbs.dreamstime.com/b/%C3%ADcone-ou-logotipo-do-base-de-dados-na-linha-estilo-moderna-81367896.jpg" alt="Download Projeto_Data_Collection_Storage.db" width="30%"/>](https://github.com/matheusvieger/Data_Collection_Storage/blob/main/Código_SQL_Modelagem.db)

Recomendo o uso do SQLonline para essa consulta, um SGBD gratuito:

[![SQL Online](https://cdn-icons-png.freepik.com/256/4248/4248443.png?semt=ais_hybrid)](https://sqliteonline.com/)

SQL Fato_Notas Schema:
```
CREATE TABLE Fato_Notas (
    ID_Nota INT NOT NULL,
    ID_Aluno INT NOT NULL,   
    ID_Professor INT NOT NULL,    
    ID_Disciplina INT NOT NULL,
    ID_Turma INT NOT NULL,
    Valor_Nota DECIMAL(2, 1) NOT NULL,
    Data_Avaliacao DATE NOT NULL,
    FOREIGN KEY (ID_Aluno) REFERENCES Alunos(ID_Aluno),
    FOREIGN KEY (ID_Professor) REFERENCES Professores(ID_Professor),
    FOREIGN KEY (ID_Disciplina) REFERENCES Disciplinas(ID_Disciplina),
    FOREIGN KEY (ID_Turma) REFERENCES Turmas(ID_Turma)
)
```
