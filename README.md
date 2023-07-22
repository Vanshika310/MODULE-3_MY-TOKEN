# MODULE-3_MY-TOKEN

The goal of this project is to create a custom token using the Ethereum blockchain and Solidity smart contract language. The token will be deployed on a local development network using HardHat, a popular development environment for Ethereum smart contract development.

## Steps to install hardhat network

1. Make sure you have Node.js and npm installed on your machine.

2. Create a New Project Directory: Open your terminal and create a new directory for your Hardhat project.

3. Initialize npm Package: Inside your project directory, initialize a new npm package by running the following command: ```npm init```

4. Install Hardhat and Dependencies: To install Hardhat and other required packages, run the following command in your terminal: ```npm install hardhat```

5. Verify Installation: To ensure that Hardhat is installed correctly, run the following command: ```npx hardhat```

6. Write the code
   
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Token {
    string public name = "Google Pay";
    string public symbol = "GPay";
    uint8 public decimals = 18;
    uint256 public totalSupply = 1000000 * 10**uint256(decimals);
    mapping(address => uint256) public balanceOf;


    event Transfer(address indexed from, address indexed to, uint256 value);
    event Mint(address indexed to, uint256 value);
    event Burn(address indexed from, uint256 value);

    constructor() {
        balanceOf[msg.sender] = totalSupply;
    }

    function mint(address to, uint256 amount) public {
        require(to != address(0), "Invalid address");
        require(msg.sender == owner(), "Only the contract owner can mint tokens");
        balanceOf[to] += amount;
        totalSupply += amount;
        emit Mint(to, amount);
        emit Transfer(address(0), to, amount);
    }

    function transfer(address to, uint256 amount) public returns (bool) {
        require(to != address(0), "Invalid address");
        require(amount > 0, "Amount must be greater than 0");
        require(balanceOf[msg.sender] >= amount, "Insufficient balance");
        balanceOf[msg.sender] -= amount;
        balanceOf[to] += amount;
        emit Transfer(msg.sender, to, amount);
        return true;
    }

    function burn(uint256 amount) public {
        require(amount > 0, "Amount must be greater than 0");
        require(balanceOf[msg.sender] >= amount, "Insufficient balance");
        balanceOf[msg.sender] -= amount;
        totalSupply -= amount;
        emit Burn(msg.sender, amount);
        emit Transfer(msg.sender, address(0), amount);
    }

    function owner() public view returns (address) {
    return msg.sender; 
    }
}
```

This is a simple Solidity smart contract that implements the Google Pay Token (GPay) on the Ethereum blockchain. The GPay token is an ERC20-compliant token with basic functionalities like minting, transferring, and burning tokens. Name: Google Pay Token, Symbol: GPay, Decimals: 18, Total Supply: 1,000,000 GPay (1,000,000 * 10^18). 
Constructor: When the contract is deployed, the constructor function is called, and the total supply of GPay tokens is allocated to the creator's address (msg.sender).

mint Function
The mint function allows the contract owner (the creator) to create and assign new GPay tokens to a specified address. Only the contract owner can call this function. When new tokens are minted, the total supply and the recipient's balance are updated accordingly.

transfer Function
The transfer function allows any user to send GPay tokens to another address. To transfer tokens, the sender's address must have a sufficient balance of GPay tokens. The function checks for valid addresses and verifies that the amount to be transferred is greater than zero.

burn Function
The burn function enables any user to permanently destroy their GPay tokens, effectively removing them from circulation. To burn tokens, the user must have a sufficient balance. The function checks that the amount to be burned is greater than zero.

owner Function
The owner function allows anyone to check who is the owner of the contract. In this case, the owner is the address of the person who deployed the contract (msg.sender).

Events
The contract emits three types of events:
Transfer: Emits when tokens are transferred from one address to another.
Mint: Emits when new tokens are minted and assigned to an address by the contract owner.
Burn: Emits when tokens are burned (destroyed) by a user.


The next step after writing the code is:

7. Compile the Smart Contract:
Use the Hardhat development environment to compile the smart contract. Open your terminal and run the following command in your project directory: ```npx hardhat compile```

8. Now open the remix ethereum IDE, then paste the code and compile it there.

9. Now type ```npx hardhat node``` in your project's directory and wait for  it to compile

10. Latly deploy your contract in remix and add Dev-Hardhat Provider in the environment and now deploy it.

11. You will see the command prompt also giving the output along with the remix
