# cafeteriaon-line

DER
Clientes (id_cliente PK, nome, email, telefone)
Produtos (id_produto PK, nome, preco, categoria)
Pedidos (id_pedido PK, id_cliente FK, data_pedido)
Itens_Pedido (id_pedido FK, id_produto FK, quantidade)


# 🍵 Sistema de Banco de Dados - Cafeteria Online

Este projeto foi desenvolvido como parte de uma atividade prática para integrar **modelagem e manipulação de banco de dados** com o uso de **controle de versão (Git/GitHub)**.  
O sistema simula o funcionamento básico de uma **cafeteria**, armazenando informações sobre **clientes**, **produtos** e **pedidos**.

---

## 📌 Estrutura do Banco de Dados

O banco de dados contém as seguintes entidades:

1. **Clientes**
   - `id_cliente` (PK, auto incremento)
   - `nome`
   - `email` (único)
   - `telefone`

2. **Produtos**
   - `id_produto` (PK, auto incremento)
   - `nome`
   - `preco`
   - `categoria`

3. **Pedidos**
   - `id_pedido` (PK, auto incremento)
   - `id_cliente` (FK → Clientes)
   - `data_pedido`

4. **Itens_Pedido**
   - `id_pedido` (FK → Pedidos)
   - `id_produto` (FK → Produtos)
   - `quantidade`

🔗 Relacionamentos:
- Um **cliente** pode fazer vários **pedidos** (1:N).
- Um **pedido** pode conter vários **produtos** → relação **N:N** implementada com a tabela `itens_pedido`.

---

### sql
CREATE TABLE clientes (
    id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    telefone VARCHAR(20)
);

CREATE TABLE produtos (
    id_produto INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    preco DECIMAL(10,2) NOT NULL,
    categoria VARCHAR(50)
);

CREATE TABLE pedidos (
    id_pedido INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT NOT NULL,
    data_pedido DATE NOT NULL,
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
);

CREATE TABLE itens_pedido (
    id_pedido INT NOT NULL,
    id_produto INT NOT NULL,
    quantidade INT NOT NULL,
    PRIMARY KEY (id_pedido, id_produto),
    FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido),
    FOREIGN KEY (id_produto) REFERENCES produtos(id_produto)
);
