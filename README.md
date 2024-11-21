# Estacionamento-ton

# Documentação: Desenvolvimento do Sistema de Estacionamento

## 1. Desenvolvimento do Backend

### 1.1 Configuração do Projeto Node.js com MySQL

1. Crie uma pasta para o projeto backend e inicialize o projeto:

    ```bash
    mkdir backend-estacionamento
    cd backend-estacionamento
    npm init -y
    ```

2. Instale os pacotes necessários:

    ```bash
    npm install express mysql body-parser cors nodemon
    ```

3. Crie os arquivos principais: `server.js`, `routes.js`

---

### 1.2 Estrutura de Banco de Dados

Criação das tabelas no MySQL:

```sql
CREATE DATABASE estacionamento;

USE estacionamento;

CREATE TABLE proprietario (
    id_proprietario INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(11) NOT NULL
);

CREATE TABLE veiculo (
    id_veiculo INT AUTO_INCREMENT PRIMARY KEY,
    modelo VARCHAR(100) NOT NULL,
    placa VARCHAR(7) NOT NULL,
    id_proprietario INT,
    FOREIGN KEY (id_proprietario) REFERENCES proprietario(id_proprietario)
);
