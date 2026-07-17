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

**Mensaje:** `docs: script de despliegue básico con Hardhat`

**Texto para añadir:**

```markdown
### Script de despliegue básico (Hardhat)

```javascript
// deploy.js
const hre = require("hardhat");

async function main() {
  const Counter = await hre.ethers.getContractFactory("Counter");
  const counter = await Counter.deploy();

  await counter.deployed();
  console.log("Counter desplegado en:", counter.address);
}

main().catch((error) => {
  console.error(error);
  process.exit(1);
});

**Mensaje:** `docs: frontend básico para interactuar con Counter`

**Texto para añadir:**

```markdown
### Frontend básico para interactuar con el Counter

```html
<button onclick="increment()">Incrementar</button>
<p>Contador: <span id="value">0</span></p>

<script>
  // Código con ethers.js para llamar al contrato en Base
</script>

```markdown
### Idea de mejora al Counter

Añadir:
- Eventos cuando se modifica el contador
- Ownership (solo owner puede resetear)
- Contador por usuario

Esto lo haría más útil como proyecto de práctica.

### Script de testing básico

```javascript
const { expect } = require("chai");

describe("SimpleStorage", function () {
  it("Debería guardar y leer datos", async function () {
    const SimpleStorage = await ethers.getContractFactory("SimpleStorage");
    const storage = await SimpleStorage.deploy();
    await storage.setData("Test en Base");
    expect(await storage.getData()).to.equal("Test en Base");
  });
});
### Contrato con mapping (usuarios)

```solidity
contract UserRegistry {
    mapping(address => bool) public registered;
    mapping(address => uint256) public score;

    function register() public {
        registered[msg.sender] = true;
        score[msg.sender] = 100;
    }
}

### Ejemplo ERC20 simplificado

```solidity
contract MyToken {
    string public name = "MyBaseToken";
    string public symbol = "MBT";
    uint8 public decimals = 18;
    uint256 public totalSupply;

    mapping(address => uint256) public balanceOf;

    function transfer(address to, uint256 amount) public returns (bool) {
        // lógica de transferencia
        return true;
    }
}

### Uso de OpenZeppelin (buena práctica)

En lugar de escribir todo desde cero, se recomienda usar:

```solidity
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, Ownable {
    constructor() ERC20("MyToken", "MTK") {}
}
### Función de mint en NFT

```solidity
function mint(address to, uint256 tokenId) public onlyOwner {
    _safeMint(to, tokenId);
}

function mintToSelf() public {
    _safeMint(msg.sender, nextTokenId++);
}
### Protección contra reentrancy

```solidity
import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

contract SecureContract is ReentrancyGuard {
    function withdraw() public nonReentrant {
        // lógica segura
    }
}
### Buenas prácticas de errores en Solidity

```solidity
require(balance >= amount, "Insufficient balance");

// Mejor (más gas eficiente):
error InsufficientBalance();
if (balance < amount) revert InsufficientBalance();

### Función payable

```solidity
function deposit() public payable {
    emit Deposit(msg.sender, msg.value);
}

receive() external payable {}

```markdown
### Uso de Libraries

```solidity
import "@openzeppelin/contracts/utils/Strings.sol";

function toString(uint256 value) internal pure returns (string memory) {
    return Strings.toString(value);
}

### Uso de Enums

```solidity
enum Status { Pending, Active, Completed, Cancelled }

Status public currentStatus;

function updateStatus(Status _status) public {
    currentStatus = _status;
}

### Arrays dinámicos y fijos

```solidity
uint256[] public numbers; // dinámico
string[10] public fixedArray; // fijo

function addNumber(uint256 num) public {
    numbers.push(num);
}

### Modifiers avanzados

```solidity
modifier onlyAfter(uint256 time) {
    require(block.timestamp >= time, "Too early");
    _;
}

function claim() public onlyAfter(unlockTime) {
    // claim logic
}

### Contrato que interactúa con otro

```solidity
contract Caller {
    IERC20 public usdc;

    constructor(address _usdc) {
        usdc = IERC20(_usdc);
    }

    function deposit(uint256 amount) public {
        usdc.transferFrom(msg.sender, address(this), amount);
    }
}


### Withdraw Pattern (seguridad)

```solidity
mapping(address => uint256) public balances;

function withdraw() public {
    uint256 amount = balances[msg.sender];
    balances[msg.sender] = 0; // reentrancy protection
    payable(msg.sender).transfer(amount);
}

### Uso básico de Assembly

```solidity
function add(uint256 a, uint256 b) public pure returns (uint256) {
    assembly {
        let result := add(a, b)
        mstore(0x00, result)
        return(0x00, 32)
    }
}

### Uso seguro de block.timestamp

```solidity
require(block.timestamp > lastTime + 1 days, "Too soon");

// Evitar manipulaciones: no usar para lógica crítica sin VRF

### Variables immutable y constant

```solidity
address public immutable owner;
uint256 public constant MAX_SUPPLY = 1000000;

constructor(address _owner) {
    owner = _owner;
}

### Uso de keccak256

```solidity
bytes32 public constant ROLE = keccak256("MINTER_ROLE");

function hasRole(bytes32 role, address account) public view returns (bool) {
    // lógica
}

### Meta-transactions

Permiten que alguien pague el gas por el usuario.

Ventajas:
- Mejor UX (usuario no necesita ETH)
- Usado en muchos proyectos modernos de Base.

### VRF vs block.timestamp

- block.timestamp → manipulable
- Chainlink VRF → número aleatorio verificable y seguro

Usar VRF cuando la aleatoriedad sea crítica.
