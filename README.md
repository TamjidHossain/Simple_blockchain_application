# Simple_blockchain_application

The blockchain application can be implemented using a simple python code (Blockchain_application.py). The function of the application is to demonstrate a blockchain system working procedure where some users exchange some values (like currency) to each other. The transactions are gathered in a Merkle tree structure and some miners perform the validation of transaction and proof-of-work to create the block and store it in the chain. In real life, the miners try to solve the puzzle parallelly. Here, for simplicity, miners are selected randomly to perform the proof-of-work algorithm one-by-one. The miner who solves the puzzle first is selected to mine the block. 

Merkle tree structure used in this application has the following sizable benefits:
•	They provide a way to prove both the integrity and validity of data
•	They significantly reduce the amount of memory needed to do the above
•	Simplified Payment Verification (SPV) – a way of verifying transactions in a block without downloading an entire block. Often used by lightweight Bitcoin clients.

Without using the Merkle tree, we would need to spend a lot of processing power to verify a single transaction in the case of accidentally or intentionally corruption of data. On a different note, Integrity and verifiability has been ensured in the application. For any tiny change in the transactions, the hash value will be changed (data immutability). Root hash matching in Merkle tree structure helps to verify any transaction (data verification). Once a transaction has been added to a block and the block is added to the chain, it cannot be denied or altered, because doing so will change the hash value of the subsequent blocks (non-repudiation). Also, the required computational effort and resource utilization to solve the puzzle prevents adversary to compromise the system in the first hand (prevention against cyberattacks).

The main working steps are –

1.	Genesis block is created and added to the blockchain
2.	The users (sender, receiver) are randomly selected to perform the transactions
3.	A number of transactions are gathered in a Merkle tree structure and Merkle root hash is calculated
4.	A block is created. The block includes ‘index’, ‘timestamp’, ‘previous block hash’, ‘nonce’, ‘tx root hash’
5.	A list of miners is created in a random order to represent the mining nodes. They start to validate the transaction and perform proof-of-work one-by-one
6.	The miner who solves the puzzle is selected to mine the block. The difficulty level of the puzzle is selected as 04 which can be increased if desired
7.	The block is then validated and added to the chain
