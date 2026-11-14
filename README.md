# SQL_BANCO_DE_DADOS_CONSULTÓRIO 
create database consultorio;
use consultorio;

DROP TABLE IF EXISTS consulta;
DROP TABLE IF EXISTS medicos;
DROP TABLE IF EXISTS clientes;

CREATE TABLE medicos (
    id INT NOT NULL,
    medico VARCHAR(80) NOT NULL,
    especialidade VARCHAR(30) NOT NULL,
    valor_consulta DECIMAL(7,2) NOT NULL,
    CONSTRAINT pk_medicos PRIMARY KEY (id)
);

CREATE TABLE clientes (
    id INT NOT NULL,
    nome VARCHAR(80) NOT NULL,
    dt_cadastro DATE NOT NULL,
    CONSTRAINT pk_clientes PRIMARY KEY (id)
);

CREATE TABLE consulta (
    id INT NOT NULL,
    medico_id INT NOT NULL,
    cliente_id INT NOT NULL,
    dia_hora DATETIME NOT NULL,
    pgto CHAR(1) NULL,
    CONSTRAINT pk_consulta PRIMARY KEY (id),
    CONSTRAINT fk_medico 
        FOREIGN KEY (medico_id) REFERENCES medicos(id),
    CONSTRAINT fk_cliente 
        FOREIGN KEY (cliente_id) REFERENCES clientes(id)  
);

insert into medicos(id, medico, especialidade, valor_consulta)
values (1, 'Gaspar da Silva', 'cirurgia plástica', 500.00);

insert into medicos(id, medico, especialidade, valor_consulta)
values (2, 'José Alencar', 'ortopedia', 300.00);

insert into medicos(id, medico, especialidade, valor_consulta)
values (3, 'Aline Santiago', 'gastrologia', 300.00);

insert into medicos(id, medico, especialidade, valor_consulta)
values (4, 'Penelope Félix', 'dermatologista', 400.00);

insert into medicos(id, medico, especialidade, valor_consulta)
values (5, 'Matusalém Borges', 'geriatria', 300.00);

insert into clientes(id, nome, dt_cadastro)
values (1, 'José da Silva', to_date('13/03/2023', 'dd/mm/yyyy'));

insert into clientes(id, nome, dt_cadastro)
values (2, 'Mariana Teles', to_date('02/04/2020', 'dd/mm/yyyy'));

insert into clientes(id, nome, dt_cadastro)
values (3, 'Rosangela Guedes', to_date('01/05/2020', 'dd/mm/yyyy'));

insert into clientes(id, nome, dt_cadastro)
values (4, 'Aline Santos', to_date('03/07/2015', 'dd/mm/yyyy'));

insert into clientes(id, nome, dt_cadastro)
values (5, 'João Santos de Souza', to_date('04/03/2019', 'dd/mm/yyyy'));

insert into consulta values (1, 1, 2, 
    to_date('12/04/2023 14:15', 'dd/mm/yyyy hh24:mi'), 'S');

insert into consulta values (2, 3, 1, 
    to_date('13/03/2023 10:00', 'dd/mm/yyyy hh24:mi'), 'S');

insert into consulta values (3, 3, 4, 
    to_date('13/03/2023 12:00', 'dd/mm/yyyy hh24:mi'), 'S');

insert into consulta values (4, 2, 5, 
    to_date('20/04/2023 11:00', 'dd/mm/yyyy hh24:mi'), null);

insert into consulta values (5, 4, 4, 
    to_date('01/04/2023 07:00', 'dd/mm/yyyy hh24:mi'), 'S');

describe medicos;

select * from consulta
left outer join medicos
  on (consulta.medico_id = medicos.id);
  
  select * from consulta
inner join medicos
  on (consulta.medico_id = medicos.id);
  
  select * from consulta, medicos;
  
  describe medicos;
select medico, especialidade, valor_consulta from medicos where id = 1;
select * from clientes where id = 2;

select id, medico, especialidade, valor_consulta from medicos;

select * from medicos where id = 1;
select * from clientes where id = 2;

select * from consulta c
join medicos m
  on (c.medico_id = m.id);
