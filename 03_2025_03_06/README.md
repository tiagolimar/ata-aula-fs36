# Ata da Aula da Turma FS36 - 06 de março de 2025

## Relacionamento entre Tabelas no Banco de Dados

Os relacionamentos entre tabelas no banco de dados servem para conectar informações de diferentes entidades, garantindo integridade e evitando redundância de dados. Os principais tipos de relacionamentos são:

### 1. Relacionamento **1 para 1 (One-to-One)**
Cada registro em uma tabela está relacionado com **exatamente um** registro em outra tabela.

**Exemplo:** Um usuário tem um único perfil.

```mermaid
erDiagram
    Usuario ||--|| Perfil : "possui um"
    Usuario {
        int id(PK)
        string nome
    }
    Perfil {
        int id(PK)
        int user_id(FK)
        string bio
    }
```

### 2. Relacionamento 1 para Muitos (One-to-Many)

Um registro em uma tabela pode estar relacionado a vários registros em outra tabela.

**Exemplo**: Um autor pode escrever vários livros.

```mermaid
erDiagram
    Autor ||--o{ Livro : "escreve vários"
    Autor {
        int id
        string nome
    }
    Livro {
        int id
        int author_id(FK)
        string titulo
    }
```

### 3. Relacionamento Muitos para Muitos (Many-to-Many)

Vários registros em uma tabela podem estar relacionados a vários registros em outra tabela. Esse tipo de relação geralmente exige uma tabela intermediária.

**Exemplo**: Alunos podem estar matriculados em vários cursos, e cursos podem ter vários alunos.

```mermaid
erDiagram
    Estudante }o--o{ Curso : "matriculado em"
    Estudante {
        int id
        string nome
    }
    Curso {
        int id
        string nome
    }
    Inscricao {
        int student_id(FK)
        int course_id(FK)
    }
```

### 4. Implementação no Sequelize
No Sequelize, os relacionamentos podem ser definidos assim:

```javascript
// 1 para 1
User.hasOne(Profile);
Profile.belongsTo(User);

// 1 para Muitos
Author.hasMany(Book);
Book.belongsTo(Author);

// Muitos para Muitos
Student.belongsToMany(Course, { through: 'Enrollment' });
Course.belongsToMany(Student, { through: 'Enrollment' });
```

Esses relacionamentos permitem consultas eficientes e garantem que os dados sejam organizados corretamente.

### 5. Documentação Oficial

Para mais detalhes sobre relacionamentos no Sequelize, consulte a documentação oficial:  
🔗 [Sequelize Associations](https://sequelize.org/docs/v6/core-concepts/assocs/)


## Expo

[Expo](https://expo.dev/) é uma plataforma para desenvolvimento de aplicativos **React Native**, facilitando a criação, teste e publicação de apps para **Android e iOS** sem configurações complexas.

### Principais vantagens:
- **Configuração simplificada**: Não é necessário configurar Xcode ou Android Studio para começar.
- **Ecossistema integrado**: Possui bibliotecas para notificações push, câmera, geolocalização e mais.
- **Testes rápidos**: Com o **Expo Go**, é possível testar o app diretamente no celular sem compilar.
- **Publicação facilitada**: Permite distribuir o app facilmente na App Store e Google Play.

🚀 **Ideal para quem quer desenvolver apps mobile de forma rápida e eficiente com React Native!**

## JSON Web Token (JWT)

### 1. O que é JWT?

JWT (JSON Web Token) é um padrão aberto para **autenticação e troca de informações seguras** entre partes. Ele é amplamente utilizado em aplicações web para **gerenciar sessões de usuários** sem necessidade de armazenar estados no servidor.

O JWT é composto por três partes:
1. **Header**: Define o tipo de token e o algoritmo de criptografia.
2. **Payload**: Contém as informações (claims) do usuário.
3. **Signature**: Garante a integridade do token.

O formato final de um JWT é:

xxxxx.yyyyy.zzzzz

Cada parte é separada por um ponto (`.`) e codificada em **Base64**.

---

### 2. Como funciona o JWT?

O fluxo básico do JWT em uma aplicação web segue estas etapas:

1. O usuário faz login com suas credenciais (e-mail/senha).
2. O servidor valida as credenciais e gera um **token JWT**.
3. O cliente recebe e armazena o token (normalmente no **localStorage** ou **cookies**).
4. Em cada requisição protegida, o cliente envia o token no **cabeçalho HTTP**.
5. O servidor valida o token e autoriza o acesso ao recurso.

### 3. Fluxo de Autenticação com JWT:

```mermaid
sequenceDiagram
    participant Cliente
    participant Servidor
    Cliente->>Servidor: Envia credenciais (login)
    Servidor-->>Cliente: Retorna um JWT
    Cliente->>Servidor: Envia JWT nas próximas requisições
    Servidor-->>Cliente: Valida o token e retorna os dados protegidos
```

## 4. Instalando e Configurando JWT no Node.js

Para utilizar JWT em um projeto **Node.js** com **Express**, precisamos instalar a biblioteca `jsonwebtoken`:

```bash
npm install jsonwebtoken
```

Agora, criamos um servidor básico com autenticação JWT:

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');

const app = express();
app.use(express.json());

const SECRET_KEY = 'minhaChaveSecreta'; // Nunca exponha isso em produção!

app.post('/login', (req, res) => {
    const { username } = req.body;

    if (!username) {
        return res.status(400).json({ message: 'Usuário é obrigatório' });
    }

    // Gerando o token
    const token = jwt.sign({ username }, SECRET_KEY, { expiresIn: '1h' });

    res.json({ token });
});

app.listen(3000, () => console.log('Servidor rodando na porta 3000'));
```

Agora, quando um usuário faz login, o servidor gera um JWT contendo o nome do usuário e o envia como resposta.

## 5. Protegendo Rotas com JWT

Após gerar o token, precisamos protegê-lo para que apenas usuários autenticados possam acessar determinadas rotas.

Criamos um **middleware** para validar o JWT em requisições protegidas:

```javascript
const authenticateToken = (req, res, next) => {
    const token = req.headers['authorization'];

    if (!token) {
        return res.status(401).json({ message: 'Acesso negado. Token não fornecido.' });
    }

    jwt.verify(token.split(' ')[1], SECRET_KEY, (err, decoded) => {
        if (err) {
            return res.status(403).json({ message: 'Token inválido.' });
        }
        req.user = decoded;
        next();
    });
};

// Rota protegida
app.get('/perfil', authenticateToken, (req, res) => {
    res.json({ message: `Bem-vindo, ${req.user.username}!` });
});
```

**Como funciona?**

1. O cliente envia o token no cabeçalho HTTP:

```bash
Authorization: Bearer <TOKEN>
```

2. O middleware verifica a autenticidade do token.
3. Se for válido, a requisição continua; caso contrário, o acesso é negado.

### 6. Expiração e Renovação de Token

Os tokens JWT podem ter um tempo de expiração para maior segurança. No exemplo anterior, usamos `{ expiresIn: '1h' }` para definir que o token expira em 1 hora.
Se um token expirar, o usuário precisará refazer login ou utilizar um refresh token.

### 7. Vantagens e Desvantagens do JWT

✅ Vantagens:

- Sem estado (stateless): Não exige armazenamento de sessão no servidor.
- Escalável: Ideal para microsserviços e autenticação distribuída.
- Seguro: Assinatura digital garante integridade dos dados.

❌ Desvantagens:

- Não pode ser revogado: Após gerado, só expira com o tempo definido.
- Payload visível: Os dados dentro do token são codificados em Base64, mas não criptografados.

### 8. Documentação Oficial

Para mais detalhes sobre JWT, consulte a documentação oficial:

🔗 [JWT.io - JSON Web Tokens](https://jwt.io/)  
🔗 [jsonwebtoken no npm](https://www.npmjs.com/package/jsonwebtoken)

## JEST

## CYPRESS
