# Ata da Aula da Turma FS36 - 27 de fevereiro de 2025

## Criação de um CRUD
- Desenvolvimento de um CRUD com frontend simples, aproveitando o backend das últimas aulas.

## React Router DOM
- Uso do [React Router DOM](https://reactrouter.com/) para gerenciamento de rotas.

## Material-UI
- Uso do [Material-UI Data Grid](https://mui.com/components/data-grid/) para exibição de dados em tabela.

## Problema de CORS

O problema de CORS (Cross-Origin Resource Sharing) ocorre quando um navegador impede que um site acesse recursos de outro domínio. Isso é uma medida de segurança implementada pelos navegadores para proteger os usuários de possíveis ataques.

O cabeçalho HTTP `Access-Control-Allow-Origin` é usado para controlar o acesso a recursos de diferentes origens. Ele especifica quais domínios têm permissão para acessar os recursos de um determinado domínio.

Quando o navegador faz uma solicitação para um recurso em um domínio diferente, ele verifica se o cabeçalho `Access-Control-Allow-Origin` está presente na resposta. Se o domínio do navegador estiver na lista de domínios permitidos, a solicitação é permitida. Caso contrário, o navegador bloqueia a solicitação e gera um erro de CORS.

Para resolver o problema de CORS, existem algumas abordagens:

1. Configurar o servidor para incluir o cabeçalho `Access-Control-Allow-Origin` na resposta. Isso pode ser feito definindo o cabeçalho no servidor ou usando uma biblioteca como o CORS.

2. Usar um proxy reverso para redirecionar as solicitações do cliente para o servidor. O proxy pode adicionar o cabeçalho `Access-Control-Allow-Origin` na resposta, permitindo que o cliente acesse os recursos.

A biblioteca CORS é uma solução popular para lidar com o problema de CORS em aplicativos web. Ela simplifica a configuração do cabeçalho `Access-Control-Allow-Origin` e fornece opções flexíveis para controlar o acesso a recursos de diferentes origens.

Ao usar a biblioteca CORS, você pode definir as origens permitidas, os métodos HTTP permitidos, os cabeçalhos permitidos e outras configurações relacionadas ao CORS. Isso permite que você tenha um controle granular sobre quais solicitações são permitidas e quais são bloqueadas.

Para usar a biblioteca CORS, você precisa instalá-la via npm ou yarn:

```bash
npm install cors
```

Em seguida, você pode importar a biblioteca e usá-la no seu servidor. Aqui está um exemplo de como configurar o CORS em um servidor Node.js usando a biblioteca CORS:

```javascript
const express = require('express');
const cors = require('cors');

const app = express();

// Configuração do CORS para permitir acesso a um único endpoint
app.use(cors({
  origin: 'https://meuwebsite.com' // Substitua "https://meuwebsite.com" pelo seu endpoint específico
}));

// app.use(cors()) Permite o acesso de qualquer origem ao invés de um endpoint específico

// Resto do código do servidor...

app.listen(3000, () => {
  console.log('Servidor iniciado na porta 3000');
});
```

Neste exemplo, o CORS está configurado para permitir acesso apenas ao endpoint específico "https://meuwebsite.com". Isso significa que somente as solicitações originadas desse endpoint terão permissão para acessar o servidor.

Para permitir acesso de qualquer origem, você pode substituir o valor de `origin` por `'*'`. No entanto, é importante considerar os riscos de segurança ao permitir acesso de qualquer origem, pois isso pode expor seu servidor a possíveis ataques. Certifique-se de avaliar cuidadosamente os riscos antes de tomar essa decisão.

Lembre-se de reiniciar o servidor após fazer as alterações no código.


## Curiosidade Javascript !!

- No JavaScript, !! (dupla negação) é uma forma de converter um valor para um booleano (verdadeiro ou falso).
  > 1. A primeira ! (negação) converte o valor para seu oposto booleano.
  > 1. A segunda ! reverte esse valor novamente para seu estado booleano correto.

- É equivalente a usar Boolean(), pois ambos convertem um valor para um booleano.

``` javascript
console.log(!!"texto");    // true
console.log(Boolean("texto")); // true

console.log(!!0);          // false
console.log(Boolean(0));   // false
```

## React Hook Form
- React Hook Form é uma biblioteca flexível e eficiente para gerenciar formulários no React. Ela fornece uma API simples e intuitiva para lidar com validação de formulários, mensagens de erro e envio de formulários. Com o React Hook Form, você pode criar facilmente formulários complexos com código mínimo e melhor desempenho. Para saber mais sobre o React Hook Form, você pode visitar a documentação oficial [aqui](https://react-hook-form.com/).

Exemplo de uso do React Hook Form: 

``` javascript
import React from 'react';
import { useForm } from 'react-hook-form';

const MyForm = () => {
  const { register, handleSubmit, formState: { errors } } = useForm();

  const onSubmit = (data) => {
    console.log(data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register('name', { required: true })} />
      {errors.name && <span>This field is required</span>}

      <input {...register('email', { required: true, pattern: /^\S+@\S+$/i })} />
      {errors.email && <span>Please enter a valid email address</span>}

      <button type="submit">Submit</button>
    </form>
  );
};

export default MyForm;
```

## Axios

- Axios é uma biblioteca JavaScript popular usada para fazer requisições HTTP a partir de um navegador ou do Node.js. Ela fornece uma API fácil de usar para enviar requisições HTTP assíncronas e lidar com as respostas.

Para usar o Axios no seu projeto, você pode instalá-lo via npm ou yarn:

```bash
npm install axios
```

Uma vez instalado, você pode importar o Axios e começar a fazer requisições. Aqui está um exemplo de como fazer uma requisição GET:

```javascript
import axios from 'axios';

axios.get('https://api.exemplo.com/dados')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error(error);
  });
```

O Axios suporta vários métodos de requisição, como GET, POST, PUT, DELETE e outros. Ele também permite definir cabeçalhos de requisição, lidar com interceptadores de requisição e resposta, e cancelar requisições.

## SWR

- SWR é uma biblioteca para React que facilita o processo de busca de dados em tempo real. Ela fornece uma solução simples e eficiente para lidar com o cache, revalidação e atualização dos dados.

- Com o SWR, você pode buscar dados de APIs de forma declarativa, mantendo-os atualizados automaticamente. Ele também oferece recursos avançados, como suporte a paginção, revalidação sob demanda e manipulação de erros.

- Além disso, o SWR possui uma integração perfeita com o React, permitindo que você utilize hooks personalizados para buscar e gerenciar os dados. Isso torna o processo de busca de dados mais fácil e intuitivo.

- Para começar a usar o SWR, você pode instalá-lo via npm ou yarn:

```bash
npm install swr
```

- Em seguida, você pode importar o hook `useSWR` e começar a buscar dados. Aqui está um exemplo de como buscar dados de uma API:

```javascript
import useSWR from 'swr';

const fetcher = (url) => fetch(url).then((res) => res.json());

const MyComponent = () => {
  const { data, error, isLoading } = useSWR('/api/data', fetcher);

  if (error) return <div>Erro ao buscar os dados</div>;
  if (isLoading) return <div>Carregando...</div>;

  return (
    <div>
      {data.map((item) => (
        <div key={item.id}>{item.name}</div>
      ))}
    </div>
  );
};

export default MyComponent;
```

- Neste exemplo, o hook `useSWR` é utilizado para buscar dados da API `/api/data` utilizando a função `fetcher`. O hook gerencia automaticamente o cache, revalidação e atualização dos dados, permitindo que você exiba os dados em tempo real.

- Para obter mais informações sobre como usar o SWR e seus recursos, você pode consultar a documentação oficial [aqui](https://swr.vercel.app/).

## Migrations no Sequelize

As migrations são uma forma de controlar e versionar o esquema do banco de dados em uma aplicação. Elas permitem que você defina e aplique alterações no esquema do banco de dados de forma incremental, facilitando a colaboração entre desenvolvedores e o gerenciamento de alterações no banco de dados ao longo do tempo.

No contexto do Sequelize, um ORM (Object-Relational Mapping) para Node.js, as migrations são implementadas através de arquivos JavaScript que descrevem as alterações a serem feitas no esquema do banco de dados. Cada migration é composta por um par de métodos `up` e `down`. O método `up` define as alterações a serem aplicadas no esquema do banco de dados, enquanto o método `down` define as alterações a serem desfeitas, permitindo a reversão das migrations.

### 1. Instalação do Sequelize CLI
```bash
npm install --save-dev sequelize-cli
```

### 2. Inicialização do Sequelize
```bash
npx sequelize-cli init
```

### 3. Criar uma Migration
```bash
npx sequelize-cli migration:generate --name create-users
```

### 4. Editar a Migration
Abra o arquivo gerado em `migrations/` e defina a estrutura da tabela:

```javascript
module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('Users', {
      id: {
        type: Sequelize.INTEGER,
        autoIncrement: true,
        primaryKey: true,
        allowNull: false
      },
      name: {
        type: Sequelize.STRING,
        allowNull: false
      },
      createdAt: {
        type: Sequelize.DATE,
        allowNull: false
      },
      updatedAt: {
        type: Sequelize.DATE,
        allowNull: false
      }
    });
  },

  down: async (queryInterface, Sequelize) => {
    await queryInterface.dropTable('Users');
  }
};
```

### 5. Executar Migrations
```bash
npx sequelize-cli db:migrate
```

### 7. Reverter Migrations
```bash
npx sequelize-cli db:migrate:undo
npx sequelize-cli db:migrate:undo:all
```

### Documentação Oficial

Para mais informações, consulte a documentação oficial do Sequelize:

🔗 [Sequelize Migrations](https://sequelize.org/docs/v6/other-topics/migrations/)


## TSX e uso de Interfaces
- Estudo sobre o uso de TypeScript e Interfaces para tipagem estática e melhor organização do código.
- Recomenda-se a leitura do [Handbook oficial do TypeScript sobre Interfaces](https://www.typescriptlang.org/docs/handbook/interfaces.html).

## Tutorial de Interfaces

### Passo 1: Definir a Interface do Modelo

Primeiramente, definimos uma interface que representa a estrutura dos dados que estaremos manipulando. Por exemplo, para uma aplicação de gerenciamento de contatos:

``` typescript
// models/Contato.ts
export interface Contato {
    id: number;
  nome: string;
  email: string;
  telefone: string;
}
```

### Passo 2: Implementar a Interface no Componente

Em seguida, utilizamos essa interface nos componentes do React para garantir que os dados manipulados estejam no formato correto.

``` typescript
// components/ListaDeContatos.tsx
import React from 'react';
import { Contato } from '../models/Contato';

interface ListaDeContatosProps {
    contatos: Contato[];
}

const ListaDeContatos: React.FC<ListaDeContatosProps> = ({ contatos }) => {
    return (
        <ul>
      {contatos.map((contato) => (
          <li key={contato.id}>
          {contato.nome} - {contato.email} - {contato.telefone}
        </li>
      ))}
    </ul>
  );
};

export default ListaDeContatos;
```

### Passo 3: Consumir o Componente com Dados

Por fim, consumimos o componente <code>ListaDeContatos</code> passando um array de objetos que seguem a estrutura definida pela interface <code>Contato</code>.

``` typescript
// App.tsx
import React, { useState } from 'react';
import ListaDeContatos from './components/ListaDeContatos';
import { Contato } from './models/Contato';

const App: React.FC = () => {
  const [contatos, setContatos] = useState<Contato[]>([
    { id: 1, nome: 'João Silva', email: 'joao@example.com', telefone: '1234-5678' },
    { id: 2, nome: 'Maria Souza', email: 'maria@example.com', telefone: '8765-4321' },
  ]);

  return (
    <div>
      <h1>Lista de Contatos</h1>
      <ListaDeContatos contatos={contatos} />
    </div>
  );
};

export default App;
```

Neste exemplo, a interface <code>Contato</code> define a estrutura que os objetos de contato devem seguir. O componente <code>ListaDeContatos</code> recebe uma lista de contatos como propriedade e os exibe. O componente <code>App</code> mantém o estado dos contatos e passa esses dados para <code>ListaDeContatos</code>.

Para aprofundar seu conhecimento sobre o uso de interfaces em TypeScript, recomendo o seguinte recurso:

[Como Usar Interfaces no TypeScript | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-interfaces-in-typescript)

