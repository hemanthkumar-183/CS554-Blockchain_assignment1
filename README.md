# SafeTransfer

## Overview
The `SafeTransfer` contract enables secure transfer of SepoliaETH between EOAs and contracts. It supports all four transaction types:  
- EOA → EOA  
- EOA → Contract  
- Contract → EOA  
- Contract → Contract  

## Functions

### `receive() external payable`
Accepts incoming Ether transfers into the contract.

### `getContractBalance() public view returns (uint)`
Returns the current balance of the contract in wei.

### `eoaToAny(address payable recipient) public payable`
Allows an EOA to send SepoliaETH directly to another EOA or a contract.  
- Requires `msg.value > 0`.  
- Emits a `Transfer` event.  

### `contractToAny(address payable recipient, uint amount) public`
Allows the contract to send SepoliaETH from its own balance to any EOA or contract.  
- Requires `amount > 0`.  
- Requires the contract balance ≥ `amount`.  
- Emits a `Transfer` event.  

## Events
- `Deposit(address from, uint amount)` – triggered when the contract receives ETH.  
- `Transfer(address from, address to, uint amount)` – triggered when ETH is sent.  

## Security
1. No account can transfer from another account’s balance.  
2. Transfers only succeed if the sender (EOA or contract) has sufficient balance.  
