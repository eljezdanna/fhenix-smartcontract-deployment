# Fhenix Quest: Deploy Smart Contract & Verify
Tutorial how to deploying smart contract on fhenix
- Join [discord server](https://discord.gg/fhenix-io)
- Go to `#bot-commands` channel
- Then type `/quests`
- Let's complete (4) and (6) tasks

## Faucet & Bridge
- Request [faucet here](https://get-helium.fhenix.zone/) 
- Official [Bridge Platform](https://bridge.helium.fhenix.zone/)
- Or Using [Pheasant](https://testnet.pheasant.network/)

## Begin
- Open [Github Codespace](https://github.com/codespaces)

**Install Foundry**
```
curl -L https://foundry.paradigm.xyz | bash
```
Then restart your terminal
```bash
source $HOME/.bashrc
```
```bash
foundryup
```
**Creating New Project**
```bash
mkdir new-contract
```
```bash
cd new contract
```
```bash
forge init --no-commit
```
```bash
forge install Openzeppelin/openzeppelin-contracts --no-commit
```

**Create Contract.sol File**
```bash
touch ./src/Contract.sol
```
Copy & Paste This code
```solidity
// SPDX-License-Identifier: MIT
// Compatible with OpenZeppelin Contracts ^5.0.0
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Permit.sol";

contract MyToken is ERC20, ERC20Burnable, ERC20Permit {
    constructor() ERC20("My Token", "MTK") ERC20Permit("My Token") {
        _mint(msg.sender, 1000000000 * 10 ** decimals());
    }
}
```
Save the file and next step..

**Deploy Contract**
```bash
forge create ./src/Contract.sol:MyToken\
 --rpc-url https://api.helium.fhenix.zone\
 --private-key <your_private_key>
```
Enter your private key and wait the process. if the verification failed try again with below command.

**Verify your Contract**
```bash
forge verify-contract <your_contract_address> ./src/Contract.sol:MyToken\
 --verifier blockscout\
 --verifier-url https://explorer.helium.fhenix.zone/api\
 --rpc-url https://api.helium.fhenix.zone
```
