# Solidity: Smart Contracts

![ETH](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/eth_coin.jpg)


# Associate Profit Splitter Contract

## Purpose:

Demonstrate developing and using a smart contract to pay associate-level employees. By using a smart contract for this purpose, you essentially automate accounting, auditing, and employee payment on behalf of HR.


## Overview:

The associate profit splitter contract has two main functions:

1. `Deposit` -- This function transfers a deposit with an equal amount of Ether to three different employees. It is set to `public payable check` to ensure only the contract owner can call the function.

2. `Balance` -- Simply put, this function returns the contract's current balance. It is set to `public view returns(uint)`; since we should always be sending Ether to the beneficiaries, this function should always return `0`. If it doesn't, then the function isn't handling the remainders properly and should be fixed. This also serves as a test function to ensure deposits are distributed correctly and there is no remaining balance after a transfer.
    1. Solidity does not fully support float/decimals so the contract must handle a potential remainder since `amount` will discard the remainder during division (we can use the `uint` data type since it can only contain positive whole numbers). At the end of the `Deposit` function, it transfers the `msg.value - amount * 3` back to `msg.sender`, which is Human Resources in this case.


### Testing the Contract:

The contract is compiled using the Solidity Compiler in Remix, then deployed in the `Injected Web3` environment. Before deploying, we need to enter three employee addresses in the address parameters (the three employee payable addresses defined in the contract).

![ContractDeployment](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/DeployAndRunTransaction.PNG)

__Deposit 30 Ether (executed in MetaMask):__

![Deposit](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/ApproveTransaction.PNG)

__Original Balances (in Ganache):__

![OriginalBalances](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/AcctBalancesBeforeTransfer.PNG)

__Balances After Deposit:__

![BalancesAfterDeposit](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/AfterTransfer.PNG)
 


## Tools Used in This Project:

   * The contract was created with the [Remix IDE](https://remix.ethereum.org/).
   * The Truffle Suite [Ganache](https://www.trufflesuite.com/ganache) development chain is used to generate addresses and populate them with test ethereum.
   * The [MetaMask](https://metamask.io/) Chrome extension is used to execute transactions on localhost:8545.