# Ata da Aula da Turma FS36 - 27 de fevereiro de 2025

## Criação de um CRUD
- Desenvolvimento de um CRUD com frontend simples, aproveitando o backend das últimas aulas.
- Uso do [React Router DOM](https://reactrouter.com/) para gerenciamento de rotas.
- Uso do [Material-UI Data Grid](https://mui.com/components/data-grid/) para exibição de dados em tabela.

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
