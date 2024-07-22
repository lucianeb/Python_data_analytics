## Desafios do DIO - Python Data Analytics

# Apresentação do Desafio de Modelagem Dimensional

## Objetivo
O principal objetivo deste desafio era criar um modelo de dados em formato de Star Schema focado na análise de dados de professores. 

## Descrição do Trabalho
O desafio envolvia a montagem de um esquema em estrela onde a tabela fato reflete diversas informações sobre os professores, os cursos ministrados e o departamento ao qual cada professor pertence. Além disso, foi necessário criar tabelas de dimensão que detalham os cursos, as disciplinas oferecidas, os departamentos e as datas relacionadas aos cursos.
A implementação foi realizada utilizando as ferramentas SQL no Azure e Power BI em modo PowerQuery para visualização e análise.

## Link da entrega: https://github.com/lucianeb/Python_data_analytics/blob/main/desafio_diagrama_dimensional.pbix

### Estrutura de Tabelas Criadas
- **Departamento**: Contém informações dos departamentos incluindo um identificador único, nome do departamento e ID do coordenador.
- **Datas**: Armazena as datas de início e fim dos cursos, além de datas permitidas para matrícula.
- **Disciplina**: Detalha cada disciplina oferecida, incluindo pré-requisitos.
- **Curso**: Relaciona cada curso ao seu respectivo departamento.
- **CursoDisciplina**: Associa cursos a disciplinas, permitindo identificar quais disciplinas fazem parte de cada curso.
- **Professores**: Tabela fato que relaciona professores com cursos, disciplinas, e datas, incluindo também o departamento a que pertencem.

### Relacionamentos Estabelecidos
- Cada tabela de dimensão está relacionada à tabela fato `Professores` através de chaves estrangeiras correspondentes.
- Os cursos são relacionados às disciplinas através da tabela `CursoDisciplina`.

## Script de criação executado no Azure Data Studio
``` 
-- Removendo as tabelas existentes, se necessário
DROP TABLE IF EXISTS Professores;
DROP TABLE IF EXISTS ProfessorDisciplina;
DROP TABLE IF EXISTS CursoDisciplina;
DROP TABLE IF EXISTS Curso;
DROP TABLE IF EXISTS Disciplina;
DROP TABLE IF EXISTS Departamento;
DROP TABLE IF EXISTS Datas;

-- Criando as tabelas com os relacionamentos necessários
CREATE TABLE Departamento (
    ID_Departamento INT PRIMARY KEY,
    NomeDept VARCHAR(255),
    ID_Coordenador INT
);

CREATE TABLE Datas (
    ID_Data INT PRIMARY KEY,
    DataInicio DATE,
    DataFim DATE,
    DataPermitidaMatricula DATE
);

CREATE TABLE Disciplina (
    ID_Disciplina INT PRIMARY KEY,
    NomeDisciplina VARCHAR(255),
    PreRequisitos VARCHAR(255)
);

CREATE TABLE Curso (
    ID_Curso INT PRIMARY KEY,
    NomeCurso VARCHAR(255),
    DepartamentoID INT,
    FOREIGN KEY (DepartamentoID) REFERENCES Departamento(ID_Departamento)
);

CREATE TABLE CursoDisciplina (
    ID_Curso INT,
    ID_Disciplina INT,
    PRIMARY KEY (ID_Curso, ID_Disciplina),
    FOREIGN KEY (ID_Curso) REFERENCES Curso(ID_Curso),
    FOREIGN KEY (ID_Disciplina) REFERENCES Disciplina(ID_Disciplina)
);

CREATE TABLE Professores (
    ID_Professor INT PRIMARY KEY,
    Nome_Professor VARCHAR(255),
    ID_Departamento INT,
    FOREIGN KEY (ID_Departamento) REFERENCES Departamento(ID_Departamento)
);

CREATE TABLE ProfessorDisciplina (
    ID_Professor INT,
    ID_Disciplina INT,
    PRIMARY KEY (ID_Professor, ID_Disciplina),
    FOREIGN KEY (ID_Professor) REFERENCES Professores(ID_Professor),
    FOREIGN KEY (ID_Disciplina) REFERENCES Disciplina(ID_Disciplina)
);

-- Inserções para garantir os dados de entrada
INSERT INTO Departamento VALUES
(1, 'Politecnica', 101),
(2, 'Ciencias Exatas', 102),
(3, 'Ciencia da Computacao', 103);

INSERT INTO Curso VALUES
(1, 'Estatistica', 1),
(2, 'Matematica', 2),
(3, 'Computacao', 3);

INSERT INTO Disciplina VALUES
(1, 'Matematica Avancada', 'Calculo Diferencial e Integral'),
(2, 'Algoritimos', 'Linguagem Python'),
(3, 'Introducao a Estatistica', NULL),
(4, 'Algebra Linear', 'Matematica Avancada'),
(5, 'Calculo Diferencial e Integral', NULL),
(6, 'Bancos de Dados Relacionais', NULL),
(7, 'Linguagem Python', NULL),
(8, 'Analise Multivariada', 'Estatistica com R'),
(9, 'Estatistica com R', NULL);

INSERT INTO CursoDisciplina VALUES
(2, 1), (2, 4), (2, 5),  -- Matematica
(1, 3), (1, 8), (1, 9),  -- Estatistica
(3, 2), (3, 6), (3, 7);  -- Computacao

INSERT INTO Professores VALUES
(127, 'Antonio Silva', 1),
(238, 'Carlos Jacob', 2),
(345, 'Andrea Kish', 3);

INSERT INTO ProfessorDisciplina VALUES
(127, 3),  -- Antonio Silva, Introducao a Estatistica
(238, 4),  -- Carlos Jacob, Algebra Linear
(345, 7);  -- Andrea Kish, Linguagem Python

-- Inserir dados para Datas
INSERT INTO Datas VALUES
(1, '2025-03-20', '2025-12-15', '2025-02-15'),
(2, '2025-03-26', '2025-12-20', '2025-01-30'),
(3, '2025-03-06', '2025-12-07', '2025-02-10'); 
```


## Conclusão
O desafio foi concluído com sucesso, implementando um modelo de dados no SQL Azure e criando visualizações informativas no Power BI que permitem análises detalhadas sobre a atuação dos professores e a estrutura dos cursos oferecidos pela instituição.


