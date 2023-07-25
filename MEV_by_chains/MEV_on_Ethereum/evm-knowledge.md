## 🍟 basic evm knowledge 

<br>

### tl;dr 

* the ethereum virtual machine (evm) is a stacked-based computer.
* a virtual machine is a program built into software (ethereum clients, e.g. geth) that recreates a computer's functionality.
* to become a validator and produce blocks, running the evm is a mean to compute state transitions.
* tokens sent to a new account means that the ethereum's map of who owns what needs to change. this is done by the validators taking input/txs, running the instructions in the evm, and then printing the output in a block header.
* an ethereum client contains: 
  * the mempool (location of signed txs ready to get included in a block), 
  * JSON-RPC api (which provides a data structure for processing requests to read/write data to ethereum), 
  * a client process (which sends txs from the mempool to the evm).
  




<br>

---

### merkle patricia trie

* one of the critical functions of the evm is to store the "state" of all accounts and what information those accounts store.
* the evm stores state according to a data structure called "merkle patricia trie", which contains all the key:pairs of all addresses on ethereum. the keys correspond to both public keys and smart contracts addresses, and the values represent the current state of those addresses.
* the value/state of each address is itself an encoding of the hash of the address's respective code, a hash of the data stored by the account, its balance, and the number of txs it's carried out (represented as a nonce).
* a merkle patricia trie is used to store this data because it makes it easy to perform hashes of all the key-value pairs to eventually get to a singular "merkle root hash" of the state of who owns what (a required field in the block header of a validator's proposed block).
* because of how the hashes work, even a minute change in the blockchain state will result in a completely different root hash.
* the reason for mandating validators to include this root hash in a block header is that it significantly enhances the security of the network. this is because it enables light nodes (which don't have the space to store this merkle patricia trie) to verify the legitimacy of the block that a validator is attempting to proliferate.
* a light node can compute a "merkle proof" with the root hash, account key, and  balance value of the proposing full node, and compare that to a merkle proof of its own address & balance. there would be no match in the merkle proofs if there were any incorrect data.

<br>

---

### accounts


* an Ethereum account contains four fields:
   * the nonce: a counter used to make sure each transaction can only be processed once
   * the account's current ether balance
   * the account's contract code
   * the account's storage

* there are two types of accounts: externally owned accounts (controlled by private keys) and contract accounts (controlled by their contract code).

<br>

---

### txs

* a transaction refers to the signed data package that stores a message to be sent from an externally owned account. 
* It contains:
  * the recipient of the message
  * a signature identifying the sender
  * the amount of ether to transfer from the sender to the recipient
  * an optional data field
  * STARTGAS, representing the maximum number of computation steps the transaction is allowed to take
  * GASPRICE, representing the fee the sender pays per computation step 
 
* each tx has an intrinsic cost of 21000 gas, and creating a contract costs 32000 more gas. 

<br>

---

### message 

* a message is like a transaction, except it is produced by a contract and not an external actor. a message is produced when a contract currently executing code executes the CALL opcode.

* contracts can send "messages" to other contracts, which are virtual objects that are never serialized and exist only in the Ethereum execution environment. It contains:
  * the sender of the message (implicit)
  * the recipient of the message
  * the amount of ether to transfer alongside the message
  * an optional data field
  * STARTGAS

<br>

---

### code execution

* The existence of a Turing-complete programming language means that arbitrary contracts can be created for any transaction type or application.
* The operations have access to three types of space in which to store data:
  * the stack, a last-in-first-out container to which values can be pushed and popped
  * memory, an infinitely expandable byte array
  * contract's long-term storage, a key/value store (persist long term)
* the code in Ethereum contracts is written in a low-level, stack-based bytecode language, referred to as the EVM. 
* when a user is submitting a signed tx through a wallet, the tx data is compiled into bytecode and sent to a node using JSON-RPC api. 
* bytecode is the low-level language that the evm reads to compute state transitions. bytecode appears as a hex encoding of a string of binary. collections of these bytes represent specific operations, known as opcodes that the evm will perform.
* the reason why opcodes are important is that when computed, they enable the evm to find the output of the state transition requested by the tx.
* when sent to the mempool, the bytecode is passed as an argument in a tx broadcast to a node's mempool using JSON-RPC api. after this, the tx sits in the mempool with other unconfirmed txs ready to be included in a block by a validator.
* when a validator picks the txs it wants to include in a block, it will have to compute state transitions as defined by the operations/opcodes indicated by each txs respective bytecode (through the evm).


<br>

---

### memory

* when the evm executes a smart contract, a context is created for it (with several memory regions).
* storing the state of all accounts is data that the evm stores permanently, but the evm uses temporary memory to execute opcodes. there are two types of temporary memory during opcode execution: stack and memory.
* memory is an array of data that can be used to store information temporarily to pass through data required to compute the instructions on top of the stack (it only exists during the smart contract execution, and it's accessed with a byte offset).
* the stack is the data area where the computations as defined by opcodes are performed. it's a list of 32-byte elements.
* when txs are accessed by the evm through the mempool using the client process, the evm takes the instructions in the sequence specified by the bytecode and the bytecode gets separated into their respective opcodes.
* the stack follows the instructions at the top of the stack and utilizes data/variables moved to memory during the process to compute the instructions on top of the stack. the evm also requires information about the state it fetched from storage to run the opcodes.
* all instructions interact with the stack, but it can be directly manipulated with instructions like PUSH1, POP, DUP1, or SWAP1.



<br>

---

### opcodes

* a smart contract is a set of instructions. an instruction is assigned a value between 0 and 255 (FF in hex), called opcode, which is a text representation.
* each opcode has a specific cost. there are two part for their gas cost: 1) static cost, for running the opcode, and 2) dynamic cost, depending on factors during execution.
* when all opcodes have been run, this implies that any output about a change in state will be loaded to permanent storage by the stack. 
* once each opcode is run, the amount of gas spent in executing is subtracted from the available gas specified when the user originally submitted the tx.
* if insufficient gas was sent to cover the cost of running the opcodes, the validator does not include the tx in the block but the user doesn't get refunded because the validator has already incurred the cost to run the computation.
* once this process has been completed for all txs in the mempool that the validator wants to include in the block, the validator can compute the root hash of the new state and include it in the block header.

<br>

----

### the calldata

* the calldata region is the data that is sent with a transaction. 
* on contract creation, it's the constructor code.
* this region is immutable and can be read with  CALLDATALOAD, CALLDATASIZE, and CALLDATACOPY.
* calldata costs 4 gas per byte equal to 0, and 16 for others (paid before the opcode is executed).


<br>

--- 

### resources

* [the ethereum book on the evm](https://github.com/ethereumbook/ethereumbook/blob/develop/13evm.asciidoc)
* [0xFunk thread](https://twitter.com/0xFunk/status/1533667533164662785)


