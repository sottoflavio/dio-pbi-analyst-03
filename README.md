
## Passo 01 – Criação da instância Azure DB

Para persistir os dados do BD “Company”, foi instanciado o banco de dados “desafio-projeto-company” na plataforma Azure. Em seguida, foi baixado o certificado SSL para uso de conexão com o MySQL Workbench, e por fim, estabelecida conexão da Azure com o Power BI e coleta dos dados.


## Passo 02 – Formatando os Dados

_Tabela company departament_

  - Remoção das colunas: company.dept_locations, company.employee e company.project;
  - Formatação da coluna Dnumber de número para texto, por tratar-se de uma chave.

_Tabela company dependent_

  - Remoção da coluna: company.employee;
  - Substituição de valores da coluna “Sex” de M = “Male” e F = “Female”.

_Tabela company dept_location_

  - Remoção da coluna: company.departament;
  - Formatação da coluna Dnumber de número para texto, por tratar-se de uma chave.
  
_Tabela company employee_

  - Remoção das colunas: company.departament, company.dependent, company.employee(Ssn), company.employee(Super_ssn) e company.works_on;
  - Formatação da coluna Dno de número para texto, por tratar-se de um chave;
  - Substituição de valores da coluna “Sex” de M = “Male” e F = “Female”;
  - Colunas Fname, Minit e Lname, mescladas pelo delimitador “espaço” para uma única coluna “Nome completo”.

_Tabela company project_

  - Remoção das colunas: company.departament e company.works_on;
  - Formatação das colunas Dnum e Pnumber de número para texto, por tratar-se de uma chave.

_Tabela company works_on_

  - Remoção das colunas: company.employee e company.project;
  - Formatação da coluna Pno de número para texto, por tratar-se de uma chave.

## Passo 03 – Transformando Tabelas

_Tabela company employee_

Coluna “Super_ssn” possui um registro nulo, indicando que há um empregado sem gerente.
  ->	James S Wallace
  

_Tabela company departament_

Todos os departamentos possuem um gerente associado, datas de início da gestão e criação do departamento.


_Tabela company project_

Plocation removido, pois possui chave referencial em dept_locations.


_Tabela company works_on_

Coluna “Pno” e “Essn” formatado de número para texto, pois trata-se de uma chave;
“Hours” formatado como decimal.

## Passo 04 – Criando Novas Tabelas
**Obs.: Todas as funções abaixo foram utilizadas no próprio Power Query.**

_Empregados / Departamentos_

Mesclar consultas employee e departament para criar uma tabela employee com o nome dos departamentos associados aos colaboradores.
  ->	Foi utilizado um outter left join à tabela employee e a chave Dno com a tabela departament e chave Dnumber;
  ->	Foi utilizado um outter left Join na coluna Super_ssn para recuperar o nome completo dos gerentes de cada departamento;
  ->	Por fim, as colunas Ssn, Super_ssn, Dno, company departament.Dnumber, company departament.Mgr_ssn, foram removidas.
  

_Departamentos / Localização_
Mescle os nomes de departamentos e localização. Isso fará que cada combinação departamento-local seja único.
  ->	Foi utilizado um outter left Join à tabela departament e a chave Dnumber com a tabela dept_location e a chave Dnumber;
  ->	Nas informações recuperadas, foi expandida apenas a informação Dlocation que teve o nome da coluna alterada para Localização;
  ->	As colunas Dnumber e Mgr_ssn foram apagadas.
  
 




