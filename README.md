## Desafios do DIO - Python Data Analytics

# Apresentação do Desafio de Modelagem Dimensional

## Objetivo
O principal objetivo deste desafio era criar um modelo de dados em formato de Star Schema focado na análise de dados de professores. 

## Descrição do Trabalho
O desafio envolvia a montagem de um esquema em estrela onde a tabela fato reflete diversas informações sobre os professores, os cursos ministrados e o departamento ao qual cada professor pertence. Além disso, foi necessário criar tabelas de dimensão que detalham os cursos, as disciplinas oferecidas, os departamentos e as datas relacionadas aos cursos.
A implementação foi realizada utilizando as ferramentas SQL no Azure e Power BI em modo PowerQuery para visualização e análise.

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

## Conclusão
O desafio foi concluído com sucesso, implementando um modelo de dados robusto e flexível no SQL Azure e criando visualizações informativas no Power BI que permitem análises detalhadas sobre a atuação dos professores e a estrutura dos cursos oferecidos pela instituição.

## Link da entrega:
