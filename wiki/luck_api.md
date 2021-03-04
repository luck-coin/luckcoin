# Luck Application Development Interface #

The default JSON-RPC of luck are http://localhost:8009, you can use --rpc to start JSON-RPC.

    $luck --datadir=xxx --rpc --rpcapi=net,web3,personal,fort
	
You can also use --rpcaddr and --rpcport to modify the default listening address and port.

    $luck --datadir=xxx --rpc --rpcapi=net,web3,personal,fort --rpcaddr=x.x.x.x --rpcport=xxx

Common luck interfaces are as follows

## net_listening ##

If the client is in the state of monitoring network connections, then returns true.

**Params**

null

**Returns**

Bool - If the client is in the state of monitoring network connections, then return true, else return false.

**[Example]**

**Req:**

    curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":1}' 127.0.0.1:8009

**Response:**

    {"jsonrpc":"2.0","id":1,"result":true}

## net_peerCount ##

Returns the number of peer nodes connected to the current client

**Params**

null

**Returns**

Int - The number of peer nodes connected to the current node.

**[Example]**

**Req:**

    curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}' 127.0.0.1:8009

**Response:**

    {"jsonrpc":"2.0","id":1,"result":"0x3"}

## personal_newAccount ##

Create a new account to the local node. After you successfully call the API, your will see a new account in your keystore directory

**Params**

String - The unlock password of your account

**Returns**

Address - A new account created

**[Example]**

**Req:**

    curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"personal_newAccount","params":["<PASSWORD>"],"id":1}' 127.0.0.1:8009

**Response:**

	{"jsonrpc":"2.0","id":1,"result":"<ADDRESS>"}

## personal_unlockAccount ##

By default, if an account stayed for more than 5 minutes, the node will automatically lock an account, you need to unlock it before transfer.

If you want to call this api, you must start the node with the command params --allow-insecure-unlock, such as 
	
	$luck --datadir=xxx --rpc --rpcapi=net,web3,personal,fort --rpcaddr=x.x.x.x --rpcport=xxx --allow-insecure-unlock

**Params**

Address - The account to be unlocked

String - The unlock password of your account

**Returns**

Bool - Whether to unlock successfully

**[Example]**

**Req:**

	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"personal_unlockAccount","params":["<ADDRESS>","<PASSWORD>"],"id":1}' 127.0.0.1:8009

**Response:**

	{"jsonrpc":"2.0","id":1,"result":true}

## personal_listAccounts ##

List all accounts in the local node

**Params**

null

**Returns**

List - List of all accounts

**[Example]**

**Req:**

	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"personal_listAccounts","params":[],"id":1}' 127.0.0.1:8009

**Response:**

	{"jsonrpc":"2.0","id":1,"result":["<ADDRESS_1>","<ADDRESS_2>",...,"<ADDRESS_X>"]}

## fort_blockNumber ##

Get the current height of the chain.

**Params**

null

**Returns**

Hex - Hexadecimal representation of the current height

**[Example]**

**Req:**

	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_blockNumber","params":[],"id":1}' 127.0.0.1:8009

**Response:**

	{"jsonrpc":"2.0","id":1,"result":"0x11ce4"}

## fort_getBlockByNumber ##

Get details of a give block

**Params**

Hex - Hexadecimal representation of a given height

Bool - Whether to display transaction details

**Returns**

Block - The block details

**[Example]**

**Req:**
	
	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_getBlockByNumber","params":["0x10",false],"id":1}' 127.0.0.1:8009

**Response:**
         
	{"jsonrpc":"2.0","id":1,"result":{"basis":"0x2eb8575d6753d53bf8190c3fb7c276f936b5cbfe86415fa","difficulty":"0x78002e2","difficultyAlpha":"0x1d67a15daf33ed25ecc0035b528591e81944c8f05a712181","difficultyBeta":"0x153b52b19ff7f7b5d359636d6d7af0e9e29df28ca627032f","extraData":"0xd98301090d846c75636b89676f312e31332e3130856c696e7578","firstNonce":"0x7274c2cc1077d2fe","gasLimit":"0x2ef1b16","gasUsed":"0x0","hash":"0xbbd85b1e87d5ea7b228b7ef96b5dab965c8625770b69d761d690476bac4ca9b5","logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000","luck":"0x78002e2","miner":"0x512b9cc3ac3de758387ee83eac322915b12c2ed54420830a57","mixHash":"0x0000000000000000000000000000000000000000000000000000000000000000","nonce":"0x0000000000000000","number":"0x10","parentHash":"0x8fdc6e303e34c3959cfb59a852d3d7bd04897b952e31a48154c53726f52a1f47","receiptsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421","secondNonce":"0x327f8a2bfdfc2aeb","sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347","size":"0x282","stateRoot":"0x2f5d2c075e6d28732c14a67388cd783f42c9f44b346066de9445830f7e604fe0","timestamp":"0x5f17098a","totalDifficulty":"0x60291702","transactions":[],"transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421","uncles":[]}}

## fort_getBlockByHash ##

Get details of a give block

**Params**

Hash - A given hash

Bool - Whether to display transaction details

**Returns**

Block - The block details

**[Example]**

**Req:**

	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_getBlockByHash","params":["0xbbd85b1e87d5ea7b228b7ef96b5dab965c8625770b69d761d690476bac4ca9b5",false],"id":1}' 127.0.0.1:8009

**Response:**

	{"jsonrpc":"2.0","id":1,"result":{"basis":"0x2eb8575d6753d53bf8190c3fb7c276f936b5cbfe86415fa","difficulty":"0x78002e2","difficultyAlpha":"0x1d67a15daf33ed25ecc0035b528591e81944c8f05a712181","difficultyBeta":"0x153b52b19ff7f7b5d359636d6d7af0e9e29df28ca627032f","extraData":"0xd98301090d846c75636b89676f312e31332e3130856c696e7578","firstNonce":"0x7274c2cc1077d2fe","gasLimit":"0x2ef1b16","gasUsed":"0x0","hash":"0xbbd85b1e87d5ea7b228b7ef96b5dab965c8625770b69d761d690476bac4ca9b5","logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000","luck":"0x78002e2","miner":"0x512b9cc3ac3de758387ee83eac322915b12c2ed54420830a57","mixHash":"0x0000000000000000000000000000000000000000000000000000000000000000","nonce":"0x0000000000000000","number":"0x10","parentHash":"0x8fdc6e303e34c3959cfb59a852d3d7bd04897b952e31a48154c53726f52a1f47","receiptsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421","secondNonce":"0x327f8a2bfdfc2aeb","sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347","size":"0x282","stateRoot":"0x2f5d2c075e6d28732c14a67388cd783f42c9f44b346066de9445830f7e604fe0","timestamp":"0x5f17098a","totalDifficulty":"0x60291702","transactions":[],"transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421","uncles":[]}}

## fort_getBalance ##

Get the balance of a given address

**Params**

Address - A given address

Hex or String - Hexadecimal representation of a given height or a string with "latest"

**Returns**

Hex - Hexadecimal representation of balance

**[Example]**

**Req:**

	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_getBalance","params":["<ADDRESS>","latest"],"id":1}' 127.0.0.1:8009

**Response:**

	{"jsonrpc":"2.0","id":1,"result":"0x2936237766000"}

## fort_getTransactionCount ##

Returns the number of transactions that occurred at the specified address

**Params**

Address - A given address

Hex or String - Hexadecimal representation of a given height or a string with "latest"

**Returns**

Hex - Hexadecimal representation of the transaction count

**[Example]**

**Req:**

	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_getTransactionCount","params":["<ADDRESS>","latest"],"id":1}' 127.0.0.1:8009

**Response:**

	{"jsonrpc":"2.0","id":1,"result":"0x3"}

## fort_estimateGas ##

Estimate the amount of gas required for a transaction. This transaction will not be written to the blockchain.

**Params**

Transaction - A transaction as {"from":"{ADDRESS-FROM}","to":"{ADDRESS-TO}","value":"{AMOUNT}"}

**Returns**

Hex - Hexadecimal representation of transaction gas

**[Example]**

**Req:**
	
	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_estimateGas","params":[{"from":"<ADDRESS-FROM>","to":"<ADDRESS-TO>","value":"<HEX-AMOUNT>"}],"id":1}' 127.0.0.1:8009	

**Response:**

	{"jsonrpc":"2.0","id":1,"result":"0x5208"}

## fort_gasPrice ##

Estimate the current gasPrice.

**Params**

null

**Returns**

Hex - Hexadecimal representation of current gasprice.

**[Example]**

**Req:**

	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_gasPrice","params":[],"id":1}' 127.0.0.1:8009

**Response:**

	{"jsonrpc":"2.0","id":1,"result":"0x3b9aca00"}

## fort_signTransaction ##

Generate a signature for the transaction

**Params**

Transaction - A transaction as {"from":"{ADDRESS-FROM}","to":"{ADDRESS-TO}","value":"{AMOUNT}","gas":"{GAS}","gasprice":"{GASPRICE}","nonce":"{NONCE}"}.

{GAS} can be set to the return of fort\_estimateGas, {GASPRICE} can be set to the return of fort\_gasPrice, {NONCE} can be set to the return of fort\_getTransactionCount.

**Returns**

Transaction - A transaction with raw data.

**[Example]**

**Req:**

	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_signTransaction","params":[{"from":"<ADDRESS_FROM>","to":"<ADDRESS_TO>","value":"0x1","gas":"0x5208","gasPrice":"0x3b9aca00","nonce":"0x0"}],"id":1}' 127.0.0.1:8009

**Response:**
	
	{"jsonrpc":"2.0","id":1,"result":{"raw":"<RAW_DATA>","tx":{"nonce":"0x0","gasPrice":"0x3b9aca00","gas":"0x5208","to":"<ADDRESS>","value":"0x1","input":"0x","v":"0x506","r":"<R>","s":"<S>","hash":"<HASH>"}}}

## fort_sendSignedTransaction ##

Send a signed transaction to the chain.

**Params**

Raw - The raw data returned by fort_signTransaction called or other signature methods.

**Returns**

Hash - The transaction hash.

**[Example]**

**Req:**
	
	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_sendRawTransaction","params":["<RAW_DATA>"],"id":1}' 127.0.0.1:8009	

**Response:**

	{"jsonrpc":"2.0","id":1,"result":"<TRANSACTION_HASH>"}

## fort_getTransactionByHash ##

Get the details of a given transaction.

**Params**

Hash - Transactin hash or ID

**Returns**

Transaction - The transaction details

**[Example]**

**Req:**
	
	curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"fort_getTransactionByHash","params":["<TRANSACTION_HASH>"],"id":1}' 127.0.0.1:8009

**Response:**

	{"jsonrpc":"2.0","id":1,"result":{"blockHash":"<BLOCK_HASH>","blockNumber":"<BLOCK_NUMBER>","from":"<ADDRESS_FROM>","gas":"0xcf08","gasPrice":"0x3b9aca00","hash":"<TRANSACTION_HASH>","input":"0x","nonce":"0x3","to":"<ADDRESS_TO>","transactionIndex":"0x1","value":"0xb469471f80140000","v":"0x506","r":"<R>","s":"<S>"}}

