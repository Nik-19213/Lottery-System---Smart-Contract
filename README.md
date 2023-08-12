# Lottery Smart Contract

This is a Solidity smart contract for a simple lottery game where participants can enter by sending 1 ether. The contract manager can trigger the selection of a winner when there are at least three participants. The selected winner receives the entire balance of the contract. Below is a brief explanation of the contract's functionality.

## Contract Details

### Variables
- manager: The address of the manager who deployed the contract.
- participants: An array of payable addresses representing the participants who entered the lottery.

### Constructor
The contract's constructor sets the manager address to the address of the contract deployer.

### Functions
- receive() external payable
This function allows participants to enter the lottery by sending 1 ether along with the transaction. The sender's address is added to the participants array.

- getBalance() public view returns(uint)
This function returns the current balance of the contract. Only the contract manager can call this function.

- random() public view returns(uint)
This function generates a pseudo-random number based on the block's difficulty, timestamp, and the number of participants. It's important to note that the use of block.timestamp for randomness is not recommended for secure applications due to potential manipulation.

- selectWinner() public
This function is used by the contract manager to select a winner. It verifies that the manager is the sender and that there are at least three participants. It then calculates a random index using the random() function, selects a winner from the participants array based on the index, transfers the entire contract balance to the winner, and resets the participants array.

## Important Considerations
- Security Note: Using block.timestamp for randomness can expose the contract to manipulation by miners. It's recommended to use more secure randomness generation mechanisms, such as oracles.

- Gas Costs: Transferring the entire contract balance to a winner might lead to out-of-gas errors if there are a large number of participants. Consider using a withdraw pattern where winners can claim their winnings individually to mitigate this issue.

- Edge Cases: Ensure that the contract handles edge cases, such as what happens if there are not enough participants or if multiple winners are selected in rapid succession.

- Testing: Thoroughly test the contract on a testnet before deploying it to the mainnet. Test various scenarios including entering the lottery, selecting a winner, edge cases, and potential vulnerabilities.

- Gas Fees: Participants should be aware of the gas fees associated with sending transactions to the Ethereum network.

Remember that smart contracts handle real value, so security and careful consideration of contract logic are crucial.
