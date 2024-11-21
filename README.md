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

1.3 Código Backend
Exemplo de uma rota para listar proprietários:

javascript
Copiar código
const express = require('express');
const mysql = require('mysql');
const app = express();
const cors = require('cors');
app.use(cors());
app.use(express.json());

const db = mysql.createConnection({
    host: "localhost",
    user: "root",
    password: "",
    database: "estacionamento"
});

app.get('/proprietario', (req, res) => {
    db.query("SELECT * FROM proprietario", (err, results) => {
        if (err) return res.json(err);
        return res.json(results);
    });
});

app.listen(8081, () => {
    console.log("Servidor rodando na porta 8081...");
});
2. Desenvolvimento do Frontend
2.1 Inicializando o Projeto React Native
Crie o projeto com Expo:

bash
Copiar código
npx create-expo-app@latest estacionamento-frontend
Instale as dependências adicionais necessárias:

bash
Copiar código
npm install axios @react-navigation/native react-native-screens react-native-safe-area-context react-native-gesture-handler react-native-reanimated react-native-elements react-native-vector-icons
2.2 Estrutura do Projeto
Organize o projeto da seguinte maneira:

css
Copiar código
src/
├── assets/
├── pages/
│   ├── Proprietario/
│   │   ├── ProprietarioForm.js
│   │   ├── ProprietarioEdit.js
│   │   ├── ProprietarioList.js
│   │   ├── Styles.js
│   ├── Veiculo/
│   │   ├── VeiculoForm.js
│   │   ├── VeiculoEdit.js
│   │   ├── VeiculoList.js
│   ├── Home.js
2.3 Tela Principal (Home)
Exemplo de código para a tela principal, que permite navegar para as listas de proprietários e veículos:

javascript
Copiar código
import { View, Image, Text, TouchableOpacity, StyleSheet } from 'react-native';
import React from 'react';

const Home = ({ navigation }) => {
    return (
        <View style={styles.container}>
            <TouchableOpacity onPress={() => navigation.navigate('ProprietarioList')}>
                <Text>Proprietário</Text>
            </TouchableOpacity>
            <TouchableOpacity onPress={() => navigation.navigate('VeiculoList')}>
                <Text>Veículo</Text>
            </TouchableOpacity>
        </View>
    );
};

export default Home;

const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
    },
});
2.4 Tela de Listagem de Proprietários
Código para listar os proprietários que estão cadastrados no banco de dados:

javascript
Copiar código
import { FlatList, View, Text } from 'react-native';
import React, { useEffect, useState } from 'react';
import axios from 'axios';

export default function ProprietarioList() {
    const [proprietarios, setProprietarios] = useState([]);

    useEffect(() => {
        axios.get("http://localhost:8081/proprietario")
            .then(res => setProprietarios(res.data))
            .catch(err => console.log(err));
    }, []);

    return (
        <FlatList
            data={proprietarios}
            renderItem={({ item }) => <Text>{item.nome}</Text>}
        />
    );
}
2.5 Tela de Cadastro de Proprietário
Exemplo de formulário para cadastrar um novo proprietário:

javascript
Copiar código
import { View, Text, SafeAreaView, TextInput, Pressable } from 'react-native';
import React, { useState } from "react";
import axios from "axios";
import styles from './Styles.js';

export default function ProprietarioForm() {
    const [nome, setNome] = useState("");
    const [cpf, setCPF] = useState("");

    const handleClick = async (e) => {
        e.preventDefault();
        try {
            await axios.post("http://localhost:8081/proprietario", {
                nome: nome,
                cpf: cpf
            });
            window.location.reload();
        } catch (err) {
            console.log(err);
        }
    };

    return (
        <SafeAreaView style={styles.container}>
            <View style={{ alignItems: "center" }}>
                <Text style={styles.text}>Digite seu nome</Text>
                <TextInput
                    style={styles.input}
                    placeholder="Digite seu nome"
                    value={nome}
                    onChangeText={(texto) => setNome(texto)}
                />
                <Text style={styles.text}>Digite seu CPF</Text>
                <TextInput
                    style={styles.input}
                    placeholder="Digite seu CPF"
                    value={cpf}
                    onChangeText={(texto) => setCPF(texto)}
                />
            </View>
            <View style={styles.areaBtn}>
                <Pressable
                    style={[styles.botao, { backgroundColor: "#1d75cd" }]}
                    onPress={handleClick}
                >
                    <Text style={styles.botaoText}>Cadastrar</Text>
                </Pressable>
            </View>
        </SafeAreaView>
    );
}
2.6 Tela de Edição de Proprietário
Exemplo de código para editar as informações de um proprietário existente:

javascript
Copiar código
import React, { useState } from 'react';
import { View, Text, TextInput, SafeAreaView, Pressable } from 'react-native';
import axios from 'axios';
import styles from './Styles.js';

export default ({ route, navigation }) => {
    const [proprietarios, setProprietarios] = useState(route.params ? route.params : {});

    const handleClick = async (e) => {
        e.preventDefault();
        try {
            await axios.put(`http://localhost:8081/proprietario/${proprietarios.id_proprietario}`, proprietarios);
            window.location.reload();
        } catch (err) {
            console.log(err);
        }
    };

    return (
        <SafeAreaView style={styles.container}>
            <View style={{ alignItems: "center" }}>
                <Text style={styles.text}>Identificação</Text>
                <TextInput
                    readOnly
                    style={styles.input}
                    onChangeText={id_proprietario => setProprietarios({ ...proprietarios, id_proprietario })}
                    value={proprietarios.id_proprietario}
                />
                <Text style={styles.text}>Digite seu nome</Text>
                <TextInput
                    style={styles.input}
                    onChangeText={nome => setProprietarios({ ...proprietarios, nome })}
                    value={proprietarios.nome}
                />
                <Text style={styles.text}>Digite seu CPF</Text>
                <TextInput
                    style={styles.input}
                    onChangeText={cpf => setProprietarios({ ...proprietarios, cpf })}
                    value={proprietarios.cpf}
                />
                <Pressable style={[styles.botao, { backgroundColor: "#1d75cd" }]} onPress={handleClick}>
                    <Text style={styles.botaoText}>Alterar</Text>
                </Pressable>
            </View>
        </SafeAreaView>
    );
};
