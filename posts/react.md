# React
<div align="center">
    <img src="https://img.icons8.com/?size=100&id=123603&format=png&color=000000">
</div>

- [React](#react)
  - [Hooks](#hooks)
    - [useState](#usestate)
    - [useEffect](#useeffect)
    - [useContext](#usecontext)
    - [useReducer](#usereducer)
    - [useRef](#useref)
  - [Conclusão](#conclusão)
  - [Voltar ao topo](#voltar-ao-topo)
  - [Renderização](#renderização)
  - [Componentes](#componentes)
    - [Componentes Funcionais](#componentes-funcionais)
    - [Componentes de Classe](#componentes-de-classe)
    - [JSX](#jsx)
    - [Propriedades (Props)](#propriedades-props)
    - [Renderização Condicional](#renderização-condicional)
    - [Listas e Chaves](#listas-e-chaves)
  - [Conclusão](#conclusão-1)
  - [Voltar ao topo](#voltar-ao-topo-1)

## Hooks

Os Hooks são funções que permitem usar estado e outras funcionalidades do React em componentes funcionais.

### useState
**O que faz**: Adiciona estado a um componente funcional.
**Como usar**:
```jsx
import React, { useState } from 'react';

function Contador() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Você clicou {count} vezes</p>
      <button onClick={() => setCount(count + 1)}>Clique aqui</button>
    </div>
  );
}
```

### useEffect
**O que faz**: Permite executar efeitos colaterais (ex.: fetch de dados, assinaturas) em componentes funcionais.
**Como usar**:

```jsx
import React, { useState, useEffect } from 'react';

function Relogio() {
  const [time, setTime] = useState(new Date().toLocaleTimeString());

  useEffect(() => {
    const interval = setInterval(() => {
      setTime(new Date().toLocaleTimeString());
    }, 1000);

    return () => clearInterval(interval); // Cleanup
  }, []); // Executa apenas uma vez

  return <div>Hora atual: {time}</div>;
}
```

### useContext
O que faz: Consome valores de um contexto em componentes funcionais.
Como usar:
```jsx
import React, { useContext } from 'react';

const TemaContext = React.createContext('claro');

function ExibirTema() {
  const tema = useContext(TemaContext);

  return <div>O tema atual é {tema}</div>;
}
```
### useReducer
O que faz: Gerencia o estado de um componente através de uma função reducer, útil para estados complexos.
Como usar:
```jsx
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Contador() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Contagem: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Incrementar</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrementar</button>
    </div>
  );
}
```

### useRef
O que faz: Cria uma referência mutável que persiste durante o ciclo de vida do componente, útil para acessar elementos DOM diretamente.
Como usar:
```jsx
import React, { useRef } from 'react';

function TextoFocus() {
  const inputEl = useRef(null);

  const focarInput = () => {
    inputEl.current.focus();
  };

  return (
    <div>
      <input ref={inputEl} type="text" />
      <button onClick={focarInput}>Focar no Input</button>
    </div>
  );
}
```
## Conclusão
- useState: Para gerenciar estado local.
- useEffect: Para efeitos colaterais como fetch de dados.
- useContext: Para consumir valores de contexto.
- useReducer: Para estados mais complexos e lógica de redução.
- useRef: Para acessar diretamente elementos DOM.
[Voltar ao topo](#react)
---

## Renderização

A renderização no React é o processo de atualizar a interface do usuário em resposta a mudanças de estado ou propriedades.

## Componentes
### Componentes Funcionais
Componentes que são funções simples e retornam elementos JSX.

```jsx
import React from 'react';

function Saudacao() {
  return <h1>Olá, mundo!</h1>;
}

export default Saudacao;

```

### Componentes de Classe
Componentes mais antigos que podem manter estado interno e utilizar métodos do ciclo de vida.
```jsx
import React, { Component } from 'react';

class Saudacao extends Component {
  render() {
    return <h1>Olá, mundo!</h1>;
  }
}

export default Saudacao;

```
### JSX
JSX permite escrever HTML dentro do JavaScript.
```jsx
const elemento = <h1>Olá, mundo!</h1>;
```
### Propriedades (Props)
Props são dados passados de um componente pai para um componente filho.

```jsx
function Saudacao({ nome }) {
  return <h1>Olá, {nome}!</h1>;
}

function App() {
  return <Saudacao nome="Maria" />;
}
```

### Renderização Condicional
Renderizar elementos ou componentes com base em uma condição.

```jsx
function Saudacao({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h1>Bem-vindo de volta!</h1>;
  } else {
    return <h1>Por favor, faça login.</h1>;
  }
}
```

### Listas e Chaves
Renderizar listas de elementos e usar uma chave única para cada elemento.
```jsx
function ListaDeItens({ itens }) {
  return (
    <ul>
      {itens.map(item => (
        <li key={item.id}>{item.texto}</li>
      ))}
    </ul>
  );
}
```

## Conclusão
- Componentes: Use componentes funcionais com hooks.
- JSX: Escreva HTML dentro do JavaScript.
- Props: Passe dados entre componentes.
- Renderização Condicional: Renderize com base em condições.
- Listas e Chaves: Renderize listas de elementos.
- Ciclo de Vida: Use useEffect para efeitos colaterais.
[Voltar ao topo](#react)
---
