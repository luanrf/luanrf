drop database if exists campeonato_futebol;

create database if not exists campeonato_futebol
default character set utf8
default collate utf8_general_ci;

use campeonato_futebol;

CREATE TABLE IF NOT EXISTS clube (
    id_clube INT NOT NULL,
    nome VARCHAR(150) NOT NULL,
	mascote VARCHAR(50) NOT NULL,
    endereco VARCHAR(200),
    cidade VARCHAR(50),
    cep CHAR(9),
    uf CHAR(2),
    PRIMARY KEY (id_clube)
);

CREATE TABLE IF NOT EXISTS jogador(
	id_jogador INT NOT NULL,
    nome VARCHAR(100) NOT NULL,
    posicao VARCHAR(50),
    data_nascimento varchar(50) NOT NULL,
    pais VARCHAR(200),
	PRIMARY KEY (id_jogador)
);

CREATE TABLE IF NOT EXISTS clube_jogador(
	FOREIGN KEY (id_clube_fk) REFERENCES clube (id_clube),
    FOREIGN KEY (id_jogador_fk) REFERENCES jogador (id_jogador)
);

CREATE TABLE IF NOT EXISTS jogo (
	id_jogo INT NOT NULL,
    data_jogo DATE NOT NULL,
    hora_jogo FLOAT NOT NULL,
    local_jogo VARCHAR(150) NOT NULL,
    mandante VARCHAR(150) NOT NULL,
    visitante VARCHAR(150) NOT NULL,
    placar INT NOT NULL,
	PRIMARY KEY (id_jogo)
);

CREATE TABLE IF NOT EXISTS jogadores_jogos(
	gols INT,
    cartao_amarelo INT,
    cartao_vermelho INT,
    FOREIGN KEY (id_jogo_fk) REFERENCES jogo (id_jogo),
    FOREIGN KEY (id_jogador_fk) REFERENCES jogador (id_jogador)
);

CREATE TABLE IF NOT EXISTS campeonato (
	id_campeonato INT NOT NULL,
    nome VARCHAR(150) NOT NULL,
    data_inicio DATE NOT NULL,
    data_final DATE NOT NULL,
    PRIMARY KEY (id_campeonato)
);

CREATE TABLE IF NOT EXISTS campeonato_clube (
	pontuacao INT NOT NULL,
    vitorias INT NOT NULL,
    derrota INT NOT NULL,
    empate INT NOT NULL,
    gols_pro INT NOT NULL,
    gols_contra INT NOT NULL,
    FOREIGN KEY (id_campeonato_fk) REFERENCES campeonato (id_campeonato),
    FOREIGN KEY (clube_fk) REFERENCES clube (nome)
);

INSERT INTO clube VALUES
("001","C.R. FLAMENGO", "URUBU", "Gavea, Av. Borges de Medeiros, 997", "RIO DE JANEIRO", "22430-041", "RJ"),
("002", "C.R. VASCO DA GAMA", "ALMIRANTE", "Rua Gal AlmÃ©rio de Moura, 131", "RIO DE JANEIRO", "20921-060", "RJ"),
("003", "FLUMINENCE F.C.","GUERRERINHO", "Rua Ã�lvaro Chaves, 41", "RIO DE JANEIRO", "22231-220", "RJ"),
("004", "BOTAFOGO F.R.", "MANEQUINHO", "Avenida Venceslau BrÃ¡s, 72", "RIO DE JANEIRO", "22290-140", "RJ");

INSERT INTO jogador VALUES
("001", "DIEGO ALVES", "GOLEIRO", "24/06/1985", "BRASIL"),
("002", "GABRIEL BATISTA", "GOLEIRO", "03/06/1998", "BRASIL"),
("003", "RODRIGO CAIO", "ZAGUEIRO", "17/08/1993", "BRASIL"),
("004", "DAVID LUIZ", "ZAGUEIRO", "22/04/1987", "BRASIL"),
("005", "ISLA", "LATERAL DIREITO", "12/06/1988", "CHILE"),
("006", "FILIPE LUÃ�S", "LATERAL ESQUERDO", "09/08/1985", "BRASIL");

INSERT INTO clube_jogador VALUES
("001", "001"),
("001", "002"),
("001", "003"),
("001", "004");

INSERT INTO jogadores_jogos VALUES
("3", "0", "0", "001", "003"),
("0", "1", "0", "001", "001"),
("2", "0", "0", "001", "002");

INSERT INTO campeonato VALUES
("001", "BRASILEIRAO", "29/04/2021", "05/12/2021");

INSERT INTO campeonato_clube VALUES
("3","1", "0", "0", "3", "0", "001", "001"),
("0","0", "1", "0", "3", "0", "001", "004"),
("1","0", "0", "1", "1", "1", "001", "002"),
("1","0", "0", "1", "1", "1", "001", "003");
