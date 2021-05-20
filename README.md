# Solidity: Smart Contracts

![ETH](https://github.com/bgregory0913/Solidity_Smart_Contraacts/blob/main/Images/eth_coin.jpg)


# Overview:

Demonstrate how to develop and use smart contracts to pay employees. By using a smart contract for this purpose, you essentially automate accounting, auditing, and employee payments.


## Associate-Level Profit Splitter Contract

### Purpose:

The associate profit splitter contract has two main functions:

1. `Deposit` -- This function transfers a deposit with an equal amount of Ether to three different employees. It is set to `public payable check` to ensure only the contract owner can call the function.

2. `Balance` -- Simply put, this function returns the contract's current balance. It is set to `public view returns(uint)`; since we should always be sending Ether to the beneficiaries, this function should always return `0`. If it doesn't, then the function isn't handling the remainders properly and should be fixed. This also serves as a test function to ensure deposits are distributed correctly and there is no remaining balance after a transfer.
    1. Solidity does not fully support float/decimals so the contract must handle a potential remainder since `amount` will discard the remainder during division (we can use the `uint` data type since it can only contain positive whole numbers). At the end of the `Deposit` function, it transfers the `msg.value - amount * 3` back to `msg.sender`, which is Human Resources in this case.


### Testing the Contract:

The contract is compiled using the Solidity Compiler in Remix, then deployed in the `Injected Web3` environment. After deploying, we need to enter three employee addresses in the address parameters (the three employee payable addresses defined in the contract).

![ContractDeployment](https://github.com/bgregory0913/Solidity_Smart_Contraacts/blob/main/Images/DeployAndRunTransaction.PNG)

__Deposit 30 Ether (executed in MetaMask):__

![Deposit](https://github.com/bgregory0913/Solidity_Smart_Contraacts/blob/main/Images/ApproveTransaction.PNG)

__Original Balances (in Ganache):__

![OriginalBalances](https://github.com/bgregory0913/Solidity_Smart_Contraacts/blob/main/Images/AcctBalancesBeforeTransfer.PNG)

__Balances After Deposit:__

![BalancesAfterDeposit](https://github.com/bgregory0913/Solidity_Smart_Contraacts/blob/main/Images/AfterTransfer.PNG)
 
 

## Tiered Profit Splitter Contract

### Purpose:

In this contract, rather than splitting the profits between associate-level employees we calculate rudimentary percentages for different tiers of employees (CEO, CTO, and Bob) and pay them accordingly.

The `deposit` function in this contract has the following differences from the associate-level contract `deposit` function:

1. Calculation of the number of points/units is done by dividing `msg.value` by 100. This allows us to multiply the points with a number representing a percentage.
2. The `uint amount` variable is used to store the amount to send each employee temporarily. For each employee, the amount is set equal to the number of points multiplied by the percentage 
    1. For `employee_one`, distribute points * 60.
    2. For `employee_two`, distribute points * 25.
    3. For `employee_three`, distribute points * 15.
3. After calculating the amount for the first employee, the amount is added to the total to keep a running total of how much of the `msg.value` has distributed.
4. After transfering the amount, the remainder is sent to the employee with the highest percentage by subtracting `total` from `msg.value`.

### Testing the Contract:

The contract is compiled the same way (using the Solidity Compiler in Remix), and deployed in the `Injected Web3` environment. After deploying, we need to enter three employee addresses in the address parameters (the three employee payable addresses defined in the contract).

![ContractDeployment](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/TieredSendDeposit.PNG)

__Deposit 200 Ether (executed in MetaMask):__

![Deposit](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/Tiered_Approval.PNG)

__Original Balances (in Ganache):__

![OriginalBalances](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/Tiered_BalancesBefore.PNG)

__Balances After Deposit:__

![BalancesAfterDeposit](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/Tiered_BalancesAfter.PNG)

__Using the Balance Function:__

The function returns a value of 0 indicating that the deposit function is handling the remaining ethereum successfully.

![ZeroBalance](https://github.com/bgregory0913/Solidity_Smart_Contraacts/Images/Tiered_CheckZeroBalance.PNG)



## Tools Used in This Project:

   * The contract was created with the [Remix IDE](https://remix.ethereum.org/).
   * The Truffle Suite [Ganache](https://www.trufflesuite.com/ganache) development chain is used to generate addresses and populate them with test ethereum.
   * The [MetaMask](https://metamask.io/) Chrome extension is used to execute transactions on localhost:8545.
