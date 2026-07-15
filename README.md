### ¿Qué es Base?

Base es una Layer 2 construida sobre Ethereum por Coinbase. Destaca por sus bajos fees, velocidad y enfoque en developers y adopción masiva.

Me interesa porque facilita construir dApps sin pagar gas caro.

### Conceptos básicos de Layer 2 que estoy aprendiendo

- Layer 2 hereda la seguridad de Ethereum pero es mucho más rápida y barata
- Base usa Optimism Stack
- Los fees bajos permiten experimentar sin miedo
- Chain ID de Base Mainnet: 8453

### Diferencia entre testnet y mainnet en Base

- Testnet: Ideal para practicar sin gastar dinero real
- Mainnet: Para proyectos serios y con valor real
- Siempre empezar en testnet para evitar errores costosos

### ¿Qué es un bridge y cómo usarlo en Base?

Un bridge sirve para mover fondos desde Ethereum u otras chains a Base. 

Consejo: Siempre usar el bridge oficial al principio y probar con cantidades pequeñas.

### Tipos de transacciones comunes en Base

- Transferencias simples de ETH o tokens
- Interacción con contratos (swaps, mint, etc.)
- Despliegue de contratos
- Aprobaciones (approve)

Cada una tiene un costo de gas diferente.

### Cómo verificar un contrato en Blockscout (Base)

Después de desplegar es importante verificar el código fuente para que sea transparente.

Pasos básicos:
- Ir a Blockscout
- Buscar el contrato
- Subir el código fuente y metadata

### Gas en Base: qué es y cómo optimizarlo

El gas es el costo de ejecutar operaciones en la blockchain.

Consejos para ahorrar:
- Minimizar operaciones de almacenamiento
- Usar variables adecuadas
- Agrupar transacciones cuando sea posible

- ### Cómo funciona un swap en un DEX de Base

1. Usuario aprueba el token que quiere vender
2. Llama al router del DEX con los parámetros del swap
3. Recibe el token deseado en su wallet

Todo se hace en una o dos transacciones.

### On-chain vs Off-chain

- On-chain: Todo queda registrado en la blockchain (transparente pero caro)
- Off-chain: Se hace fuera de la cadena (más rápido y barato) y luego se lleva a on-chain cuando es necesario

- ### Introducción a Hardhat

Hardhat es una herramienta de desarrollo para Ethereum y L2s como Base.

Ventajas:
- Entorno local completo
- Testing fácil
- Scripts de despliegue

- ### Airdrops en el ecosistema Base

Algunos proyectos hacen airdrops a usuarios activos. 

Forma de participar:
- Usar sus dApps
- Proporcionar liquidez
- Participar en quests o testnets

- ### Gas Limit y Gas Price

- Gas Limit: Cantidad máxima de gas que estás dispuesto a gastar en una transacción
- Gas Price: Precio por unidad de gas

En Base suelen ser muy bajos comparado con Ethereum.

### Contrato Counter simple (primer experimento)

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Counter {
    uint256 public count = 0;

    function increment() public {
        count += 1;
    }

    function decrement() public {
        count -= 1;
    }

    function reset() public {
        count = 0;
    }
}
