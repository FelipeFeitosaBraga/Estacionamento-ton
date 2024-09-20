Aqui está o arquivo README.md baseado nas instruções fornecidas:

```markdown
# Projeto Estacionamento - Frontend

Este projeto consiste em uma aplicação simples de gerenciamento de estacionamento com cadastro,
 listagem e edição de proprietários e veículos, desenvolvido em React Native com navegação Stack,
 Axios para consumo de API e estilização básica.

## Requisitos

- Node.js
- Expo CLI
- API backend rodando (com `npx nodemon index`)

## Estrutura do Projeto

```bash
├── src
│   ├── pages
│   │   ├── Home.js
│   │   ├── Proprietario
│   │   │   ├── ProprietarioForm.js
│   │   │   ├── ProprietarioList.js
│   │   │   ├── ProprietarioEdit.js
│   │   ├── Veiculo
│   │   │   ├── VeiculoList.js
│   ├── assets
│   │   ├── estacionamento.png
└── styles.js
```

## Instruções para Rodar o Projeto

### Passo 1: Inicie o Backend

Antes de iniciar o frontend, certifique-se de que a API backend está rodando. No diretório da API, execute o comando:

```bash
npx nodemon index
```

### Passo 2: Criar o Projeto Frontend

1. Crie a pasta `FrontEnd2` dentro da pasta `Estacionamento`.
2. Abra a pasta no Visual Studio Code.
3. No terminal, crie o projeto Expo dentro desta pasta:

```bash
npx create-expo-app ./
```

### Passo 3: Instalar Dependências

Execute os seguintes comandos no terminal para instalar as dependências necessárias:

```bash
npm run web
```

Se solicitado, confirme o uso da porta `8082` clicando `Y`.

Instale as dependências para rodar o app na web:

```bash
npx expo install react-native-web@~0.19.6 react-dom@18.2.0 @expo/metro-runtime@~3.1.3
```

Instale as dependências de navegação e Axios para consumo de API:

```bash
npm install @react-navigation/native
npx expo install react-native-screens react-native-safe-area-context
npm install axios
npm install @react-navigation/stack
npm install react-native-elements --save
npm install react-native-vector-icons --save
```

### Passo 4: Executar o Projeto

Para iniciar o projeto:

```bash
npm run web
```

### Estrutura do Projeto

1. **Tela de Login**: Com campos de usuário e senha.
2. **Navegação Stack**: Gerencia a navegação entre telas (Splash, Login, Feed, Perfil, Configurações).
3. **Feed**: Utiliza `FlatList` para exibir postagens.
4. **Perfil**: Tela para editar informações do perfil.
5. **Configurações**: Ajustes de preferências de tema e idioma.

### Funcionalidades Principais

- **ProprietárioForm.js**: Cadastro de proprietários.
- **ProprietárioList.js**: Listagem de proprietários com botões para editar e deletar.
- **ProprietárioEdit.js**: Edição de dados de proprietários.
- **VeiculoList.js**: Listagem simples de veículos.

### Modificação do App.js

O arquivo `App.js` gerencia as telas principais do app utilizando o `createStackNavigator` do React Navigation.
Certifique-se de configurar as telas e rotas corretamente para garantir o funcionamento da navegação.

### Executando a Aplicação

Certifique-se de que o backend está rodando e execute o frontend com o comando:

```bash
npm run web
```

Agora você pode utilizar o aplicativo no navegador!

```

Este arquivo README fornece um guia passo a passo para rodar o projeto e explica sua estrutura e funcionalidades.
