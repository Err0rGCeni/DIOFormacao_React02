# Conceitos Fundamentais para React

## JSX

JSX (JavaScript XML) é uma extensão de sintaxe utilizada no React para descrever a estrutura da interface do usuário. É uma parte central da programação com React e permite combinar JavaScript com marcação XML/HTML de forma mais fácil e intuitiva.

## Componentes e Ciclo de Vida

[![Classe e Funcional: ankit patidar](https://miro.medium.com/v2/resize:fit:720/format:webp/1*SFAgu3wDeaeDNM3Fi-oegg.jpeg)](https://medium.com/@ankitpatidar030/the-difference-between-classes-and-function-components-in-react-332c39b42b7a)

### Classe

```jsx
import React, { Component } from "react";

class ClasseExemplo extends Component {
  constructor(props) {
    super(props);
    this.state = {
      contador: 0,
    };
  }

  componentDidMount() {
    console.log("Componente em classe foi montado.");
  }

  componentDidUpdate() {
    console.log("Componente em classe foi atualizado.");
  }

  componentWillUnmount() {
    console.log("Componente em classe será desmontado.");
  }

  incrementarContador = () => {
    this.setState((prevState) => ({
      contador: prevState.contador + 1,
    }));
  };

  render() {
    return (
      <div>
        <h2>Exemplo de componente em classe</h2>
        <p>Contador: {this.state.contador}</p>
        <button onClick={this.incrementarContador}>Incrementar</button>
      </div>
    );
  }
}

export default ClasseExemplo;
```

Ciclo de vida em componentes de classe:

- Em componentes de classe, o ciclo de vida é gerenciado por métodos como `componentDidMount`, `componentDidUpdate`, e `componentWillUnmount`.
  - O `componentDidMount` é executado após o componente ser montado no DOM, permitindo a realização de inicializações.
  - O `componentDidUpdate` é chamado sempre que o componente é atualizado após uma mudança de estado ou de propriedades.
  - O `componentWillUnmount` é chamado antes de o componente ser removido do DOM, permitindo a limpeza e a remoção de event listeners ou outras tarefas.

### Funções

```jsx
import React, { useState, useEffect } from 'react';

const FuncionalExemplo = () => {
  const [contador, setContador] = useState(0);

  useEffect(() => {
    console.log('Componente funcional foi montado.');
    return () => {
      console.log('Componente funcional será desmontado.');
    };
  }, []);

  useEffect(() => {
    console.log('Componente funcional foi atualizado.');
  }, [contador]);

  const incrementarContador = () => {
    setContador((prevContador) => prevContador + 1);
  };

  return (
    <div>
      <h2>Exemplo de componente funcional</h2>
      <p>Contador: {contador}</p>
      <button onClick={incrementarContador}>Incrementar</button>
    </div>
  );
};

export default FuncionalExemplo;

```

Hooks em componentes funcionais:

- Com a introdução dos Hooks no React, como `useState` e `useEffect`, os componentes funcionais agora podem ter estado e lidar com efeitos secundários.
  - O `useState` permite que você adicione estado ao componente funcional usando um array destructuring. A função retornada pelo `useState` pode ser usada para atualizar o estado.
  - O `useEffect` é usado para adicionar efeitos secundários a componentes funcionais, como realizar chamadas de API ou manipular o DOM. Pode ser comparado ao componentDidMount, componentDidUpdate, e componentWillUnmount combinados.
    - O segundo argumento de `useEffect` é uma array de dependências, permitindo controlar quando o efeito será acionado, evitando chamadas desnecessárias.
