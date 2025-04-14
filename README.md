# Biblioteca
Criação de um Banco de Dados tipo Biblioteca no MySql

-- Criação do banco de dados
CREATE DATABASE Biblioteca;
USE Biblioteca;

-- Tabela: Usuario
CREATE TABLE tb_usuario (
    usuario_id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100),
    email VARCHAR(100),
    tipo VARCHAR(50), -- aluno, professor, etc.
    data_cadastro DATE
);

-- Tabela: Autor
CREATE TABLE tb_autor (
    autor_id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100)
);

-- Tabela: Editora
CREATE TABLE tb_editora (
    editora_id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100)
);

-- Tabela: Categoria
CREATE TABLE tb_categoria (
    categoria_id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100)
);

-- Tabela: Livro (Obras)
CREATE TABLE tb_obras (
    livro_id INT PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(200),
    autor_id INT,
    editora_id INT,
    categoria_id INT,
    isbn VARCHAR(20),
    ano_publicacao INT,
    quantidade_total INT,
    FOREIGN KEY (autor_id) REFERENCES tb_autor(autor_id),
    FOREIGN KEY (editora_id) REFERENCES tb_editora(editora_id),
    FOREIGN KEY (id_categoria) REFERENCES tb_categoria(id_categoria)
);

-- Tabela: Emprestimo
CREATE TABLE tb_emprestimo (
    emprestimo_id INT PRIMARY KEY AUTO_INCREMENT,
    usuario_id INT,
    data_emprestimo DATE,
    data_devolucao_prevista DATE,
    data_devolucao_real DATE,
    FOREIGN KEY (usuario_id) REFERENCES tb_usuario(usuario_id)
);

-- Tabela: ItemEmprestimo
CREATE TABLE tb_itemEmprestimo (
    item_id INT PRIMARY KEY AUTO_INCREMENT,
    emprestimo_id INT,
    livro_id INT,
    quantidade INT,
    FOREIGN KEY (emprestimo_id) REFERENCES tb_emprestimo(emprestimo_id),
    FOREIGN KEY (livro_id) REFERENCES tb_obras(livro_id)
);
---------------------------------------------------------------------------------------------------------------------------------------------------
Inserindo Dados:

-- Inserindo usuários
INSERT INTO tb_usuario (nome_usuario, email, tipo, data_cadastro)
VALUES ('Ana Silva', 'anasil@yahoo.com', 'aluna', CURDATE());

-- Inserindo autores
INSERT INTO tb_autor (nome_autor) VALUES ('Machado de Assis');

-- Inserindo editoras
INSERT INTO tb_editora (nome_editora) VALUES ('Companhia das Letras');

-- Inserindo categorias
INSERT INTO tb_categoria (nome_categoria) VALUES ('Romance');

-- Inserindo livros
INSERT INTO tb_obras (titulo_livro, autor_id, editora_id, categoria_id, isbn, ano_publicacao, quantidade_total)
VALUES ('Dom Casmurro', 1, 1, 1, '9781234567897', 1899, 3);

-- Inserindo empréstimo
INSERT INTO tb_emprestimo (usuario_id, data_emprestimo, data_devolucao_prevista)
VALUES (1, CURDATE(), DATE_ADD(CURDATE(), INTERVAL 7 DAY));

-- Inserindo item de empréstimo
INSERT INTO tb_itemEmprestimo (emprestimo_id, livro_id, quantidade_item)
VALUES (1, 1, 1);
--------------------------------------------------------------------------------------------------------------------------------------------------

-- Atualizar a data de devolução real de um empréstimo
UPDATE tb_emprestimo
SET data_devolucao_real = CURDATE()
WHERE emprestimo_id = 1;

-- Excluir um item de empréstimo
DELETE FROM tb_itemEmprestimo
WHERE item_id = 1;

-- Excluir o empréstimo
DELETE FROM tb_emprestimo
WHERE emprestimo_id = 1;
