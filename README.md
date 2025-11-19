# AtividadeArqSoftware
Implementação de Padrão de Projeto
# Exemplo de Padrão de Projeto: **Strategy** em TypeScript

Este repositório demonstra o uso do padrão de projeto **Strategy**, um dos padrões comportamentais mais utilizados quando buscamos flexibilidade na escolha de algoritmos em tempo de execução.

---

## 📌 O que foi implementado

Foi criada uma estrutura simples que simula um sistema de cálculo de frete. Cada tipo de frete (Sedex, PAC, Transportadora) é um algoritmo diferente. Utilizando o padrão **Strategy**, podemos trocar a estratégia de cálculo sem alterar o código principal da aplicação.

Esse exemplo poderia ser facilmente usado em uma arquitetura maior, como em microserviços de checkout, carrinho de compras ou backends de e-commerce.

---

## 📁 Estrutura do Projeto

```
├── src
│   ├── strategies
│   │   ├── shipping-strategy.ts
│   │   ├── pac-strategy.ts
│   │   ├── sedex-strategy.ts
│   │   └── transportadora-strategy.ts
│   └── shipping-context.ts
├── index.ts
└── README.md
```

---

## 💡 Benefícios do Padrão Strategy (com minhas palavras)

* **Facilita a manutenção**: novos algoritmos podem ser adicionados sem mexer nos existentes.
* **Evita condicionais gigantes** como `if/else` ou `switch` espalhados pelo código.
* **Favorece a extensão**: seguir o princípio do *Open/Closed* (aberto para extensão, fechado para modificação).
* **Permite trocar comportamentos dinamicamente**, até mesmo em tempo de execução.

---

## 🧠 Como funciona neste projeto

O objeto principal (`ShippingContext`) recebe uma estratégia de cálculo de frete. Ele não sabe como o frete é calculado — apenas executa a estratégia fornecida.

Assim, você pode mudar o tipo de frete apenas mudando a estratégia utilizada.

---

## 📦 Código de Exemplo

### **1) Interface da Strategy** (`shipping-strategy.ts`)

```ts
export interface ShippingStrategy {
  calculate(distance: number): number;
}
```

### **2) Estratégias Concretas**

#### **PAC** (`pac-strategy.ts`)

```ts
import { ShippingStrategy } from './shipping-strategy';

export class PACStrategy implements ShippingStrategy {
  calculate(distance: number): number {
    return distance * 0.5;
  }
}
```

#### **Sedex** (`sedex-strategy.ts`)

```ts
import { ShippingStrategy } from './shipping-strategy';

export class SedexStrategy implements ShippingStrategy {
  calculate(distance: number): number {
    return distance * 1.2;
  }
}
```

#### **Transportadora** (`transportadora-strategy.ts`)

```ts
import { ShippingStrategy } from './shipping-strategy';

export class TransportadoraStrategy implements ShippingStrategy {
  calculate(distance: number): number {
    return distance * 0.9;
  }
}
```

### **3) Contexto** (`shipping-context.ts`)

```ts
import { ShippingStrategy } from './strategies/shipping-strategy';

export class ShippingContext {
  constructor(private strategy: ShippingStrategy) {}

  setStrategy(strategy: ShippingStrategy) {
    this.strategy = strategy;
  }

  calculate(distance: number) {
    return this.strategy.calculate(distance);
  }
}
```

### **4) Uso no projeto** (`index.ts`)

```ts
import { ShippingContext } from './src/shipping-context';
import { PACStrategy } from './src/strategies/pac-strategy';
import { SedexStrategy } from './src/strategies/sedex-strategy';
import { TransportadoraStrategy } from './src/strategies/transportadora-strategy';

const context = new ShippingContext(new PACStrategy());
console.log('PAC:', context.calculate(100));

context.setStrategy(new SedexStrategy());
console.log('Sedex:', context.calculate(100));

context.setStrategy(new TransportadoraStrategy());
console.log('Transportadora:', context.calculate(100));
```

---

## 🛠️ Instalação e Execução

### **1. Clonar o repositório**

```
git clone https://[github.com/seu-usuario/nome-do-repositorio.git
cd nome-do-repositorio](https://github.com/Dudz1100/AtividadeArqSoftware/tree/main)
```

### **2. Instalar dependências**

```
npm install
```

### **3. Executar o projeto**

```
npx ts-node index.ts
```

---
