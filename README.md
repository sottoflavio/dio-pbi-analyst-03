##Etapa 1 – Criação da Instância Azure DB
Para assegurar a persistência dos dados da base de dados "Company", foi provisionado o banco de dados "desafio-projeto-company" na plataforma Azure. Subsequentemente, o certificado SSL foi baixado para possibilitar a conexão com o MySQL Workbench. Por fim, estabeleceu-se uma ligação entre a Azure e o Power BI, permitindo a recolha dos dados.

##Etapa 2 – Formatação dos Dados
Tabela "company department"
Eliminação das colunas: company.dept_locations, company.employee e company.project;
Conversão da coluna Dnumber de número para texto, devido à sua natureza enquanto chave.
Tabela "company dependent"
Eliminação da coluna: company.employee;
Substituição dos valores na coluna "Sex": M por "Male" e F por "Female".
Tabela "company dept_location"
Eliminação da coluna: company.department;
Conversão da coluna Dnumber de número para texto, devido à sua natureza enquanto chave.
Tabela "company employee"
Eliminação das colunas: company.department, company.dependent, company.employee (Ssn), company.employee (Super_ssn) e company.works_on;
Conversão da coluna Dno de número para texto, devido à sua natureza enquanto chave;
Substituição dos valores na coluna "Sex": M por "Male" e F por "Female";
Fusão das colunas Fname, Minit e Lname, separadas por espaços, numa única coluna "Nome completo".
Tabela "company project"
Eliminação das colunas: company.department e company.works_on;
Conversão das colunas Dnum e Pnumber de número para texto, devido à sua natureza enquanto chave.
Tabela "company works_on"
Eliminação das colunas: company.employee e company.project;
Conversão da coluna Pno de número para texto, devido à sua natureza enquanto chave.


##Etapa 3 – Transformação de Tabelas
Tabela "company employee"
A coluna "Super_ssn" contém um registro nulo, indicando um funcionário sem gerente.

James S Wallace
Tabela "company department"
Todos os departamentos possuem um gerente associado, bem como datas de início de gestão e criação do departamento.

Tabela "company project"
A coluna "Plocation" foi removida, pois possui uma chave referencial em "dept_locations".

Tabela "company works_on"
As colunas "Pno" e "Essn" foram convertidas de número para texto, uma vez que representam chaves;
A coluna "Hours" foi formatada como decimal.

##Etapa 4 – Criação de Novas Tabelas
Observação: Todas as operações abaixo foram realizadas utilizando o Power Query.

Funcionários / Departamentos
A mesclagem das consultas "employee" e "department" resultou numa nova tabela "employee" que inclui os nomes dos departamentos associados a cada colaborador.

Utilizou-se um "outer left join" entre a tabela "employee" e a chave Dno com a tabela "department" e a chave Dnumber;
Utilizou-se um "outer left join" na coluna "Super_ssn" para recuperar os nomes completos dos gerentes de cada departamento;
Por fim, as colunas Ssn, Super_ssn, Dno, company department.Dnumber e company department.Mgr_ssn foram eliminadas.
Departamentos / Localizações
A combinação dos nomes dos departamentos com as localizações garante que cada par departamento-localização seja único.

Realizou-se um "outer left join" entre a tabela "department" e a chave Dnumber com a tabela "dept_location" e a chave Dnumber;
Das informações recuperadas, apenas a informação Dlocation foi expandida e a sua coluna foi renomeada para "Localização";
As colunas Dnumber e Mgr_ssn foram descartadas.
