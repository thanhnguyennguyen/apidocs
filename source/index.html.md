---
title: TomoMaster APIs
language_tabs:
  - shell: cURL
  - javascript--nodejs: Node.JS
  - go: GO
  - ruby: Ruby
  - python: Python
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<h1 id="tomochain-apis">TomoChain APIs v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

Happy to code TomoChain APIs

License: <a href="https://github.com/tomochain/tomochain">Github</a>

<h1 id="tomochain-apis-json-rpc">JSON-RPC</h1>

TomoChain JSON-RPC Protocol

## eth_accounts

Returns a list of addresses owned by client.

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_accounts","params":[],"id":1}'
```

### RESPONSE

#### RESULT FIELDS

- `ADDRESSES` - arrays of hex codes as strings representing the addresses owned by the client

> Example responses

> 200 Response

```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": []
}
```

## eth_blockNumber

Returns the current "latest" block number.

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params": [],"id":1}'
```

### RESPONSE

- `BLOCK NUMBER` - a hex code of an integer representing the current block number the client is on.

> Example responses

> 200 Response

```js

  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x65a8db"
}
```

## eth_call

Executes a new message call immediately without creating a transaction on the block chain.

#### REQUEST PAYLOAD
- `TRANSACTION CALL OBJECT` _[required]_
- `from`:  _[optional]_ 20 Bytes - The address the transaction is sent from.
- `to`: 20 Bytes - The address the transaction is directed to.
- `gas`: _[optional]_ Integer of the gas provided for the transaction execution. eth_call consumes zero gas, but this parameter may be needed by some executions.
- `gasPrice`: _[optional]_ Integer of the gasPrice used for each paid gas
- `value`: _[optional]_ Integer of the value sent with this transaction
- `data`: _[optional]_ Hash of the method signature and encoded parameters. For details see Ethereum Contract ABI
- `BLOCK PARAMETER` _[required]_ - an integer block number, or the string "latest", "earliest" or "pending", see the [default block parameter](https://github.com/ethereum/wiki/wiki/JSON-RPC#the-default-block-parameter)

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_call","params": [{"from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155","to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567","gas": "0x76c0","gasPrice": "0x9184e72a000","value": "0x9184e72a","data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"}, "latest"],"id":1}'
    
```

### RESPONSE

#### RESULT FIELDS
- `RETURN VALUE` - the return value of the executed contract method.

> Example responses

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x"
}
```

## eth_estimateGas

Generates and returns an estimate of how much gas is necessary to allow the transaction to complete. The transaction will not be added to the blockchain. Note that the estimate may be significantly more than the amount of gas actually used by the transaction, for a variety of reasons including EVM mechanics and node performance.

#### REQUEST PAYLOAD
- `TRANSACTION CALL OBJECT` _[required]_
- `from`:  _[optional]_ 20 Bytes - The address the transaction is sent from.
- `to`: 20 Bytes - The address the transaction is directed to.
- `gas`: _[optional]_ Integer of the gas provided for the transaction execution. eth_estimateGas consumes zero gas, but this parameter may be needed by some executions.
- `gasPrice`: _[optional]_ Integer of the gasPrice used for each paid gas
- `value`: _[optional]_ Integer of the value sent with this transaction
- `data`: _[optional]_ Hash of the method signature and encoded parameters. For details see Ethereum Contract ABI

If no gas limit is specified geth uses the block gas limit from the pending block as an upper bound. As a result the returned estimate might not be enough to executed the call/transaction when the amount of gas is higher than the pending block gas limit.

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_estimateGas","params": [{"from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155","to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567","gas": "0x76c0","gasPrice": "0x9184e72a000","value": "0x9184e72a","data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"}],"id":1}'

```


### RESPONSE

#### RESULT FIELDS
- `GAS USED` - the amount of gas used.

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x5cec"
}
```

## eth_gasPrice

Returns the current gas price in wei.

> Code samples

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_gasPrice","params": [],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `GAS PRICE` - a hex code of an integer representing the current gas price in wei.

> Example response

> 200 Response

```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x12a05f200"
}
```

## eth_getBalance

Returns the balance of the account of given address.

#### REQUEST PARAMS
- `ADDRESS` _[required]_ - a string representing the address (20 bytes) to check for balance

- `BLOCK PARAMETER` _[required]_ - an integer block number, or the string "latest", "earliest" or "pending", see the [default block parameter](https://github.com/ethereum/wiki/wiki/JSON-RPC#the-default-block-parameter)

> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getBalance","params": ["0xc94770007dda54cF92009BFF0dE90c06F603a09f", "latest"],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `BALANCE` - integer of the current balance in wei.

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x2fe84e3113d7b"
}
```

## eth_getBlockByNumber

Returns the block data of the given BLOCKNUMBER.

#### REQUEST PARAMS
- `BLOCKNUMBER` _[required]_ - a hex code of an integer representing the `BLOCKNUMBER` or one of the following special params:
    - `latest`: get block data of the latest block
    - `pending`:  get block data of pending block
    - `earliest`: get the genesis block

- `FULLTX` _[required]_ - a boolean value specified whether you want to get transactions list or not

> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params": ["0x0" , true],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `RETURN VALUE` - block data of the given `BLOCKNUMBER`

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "difficulty": "0x1",
    "extraData": "0x00000000000000000000000000000000000000000000000000000000000000001b82c4bf317fcafe3d77e8b444c82715d216afe845b7bd987fa22c9bac89b71f0ded03f6e150ba31ad670b2b166684657ffff95f4810380ae7381e9bce41231d5dd8cdd7499e418b648c00af75d184a2f9aba09a6fa4a46fb1a6a3919b027d9cac5aa6890000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "gasLimit": "0x47b760",
    "gasUsed": "0x0",
    "hash": "0x9326145f8a2c8c00bbe13afc7d7f3d9c868b5ef39d89f2f4e9390e9720298624",
    "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "miner": "0x0000000000000000000000000000000000000000",
    "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "nonce": "0x0000000000000000",
    "number": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "penalties": "0x",
    "receiptsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "size": "0x2c5",
    "stateRoot": "0x1394d6e0a3d48b3d25da2206de068a1444108280c60d360bd9d5a870004529ee",
    "timestamp": "0x5c1358f5",
    "totalDifficulty": "0x1",
    "transactions": [],
    "transactionsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "uncles": [],
    "validator": "0x",
    "validators": "0x"
  }
}

```


## eth_getBlockByHash

Returns the block data of the given `BLOCKHASH`.

#### REQUEST PARAMS
- `BLOCKHASH` _[required]_ - a string representing a `BLOCKHASH` 
- `FULLTX` _[required]_ - a boolean value specified whether you want to get transactions list or not

> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getBlockByHash","params": ["0x9326145f8a2c8c00bbe13afc7d7f3d9c868b5ef39d89f2f4e9390e9720298624" , true],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `RETURN VALUE` - block data of the given `BLOCKHASH`

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "difficulty": "0x1",
    "extraData": "0x00000000000000000000000000000000000000000000000000000000000000001b82c4bf317fcafe3d77e8b444c82715d216afe845b7bd987fa22c9bac89b71f0ded03f6e150ba31ad670b2b166684657ffff95f4810380ae7381e9bce41231d5dd8cdd7499e418b648c00af75d184a2f9aba09a6fa4a46fb1a6a3919b027d9cac5aa6890000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "gasLimit": "0x47b760",
    "gasUsed": "0x0",
    "hash": "0x9326145f8a2c8c00bbe13afc7d7f3d9c868b5ef39d89f2f4e9390e9720298624",
    "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "miner": "0x0000000000000000000000000000000000000000",
    "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "nonce": "0x0000000000000000",
    "number": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "penalties": "0x",
    "receiptsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "size": "0x2c5",
    "stateRoot": "0x1394d6e0a3d48b3d25da2206de068a1444108280c60d360bd9d5a870004529ee",
    "timestamp": "0x5c1358f5",
    "totalDifficulty": "0x1",
    "transactions": [],
    "transactionsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "uncles": [],
    "validator": "0x",
    "validators": "0x"
  }
}

```

## eth_getBlockByNumber

Returns information about a block by hash.

### REQUEST

`POST https://rpc.tomochain.com`

#### HEADERS

`Content-Type: application/json`

#### REQUEST PARAMS
- `BLOCK PARAMETER` _[required]_ - an integer block number, or the string "latest", "earliest" or "pending", see the [default block parameter](https://github.com/ethereum/wiki/wiki/JSON-RPC#the-default-block-parameter)
- `SHOW TRANSACTION DETAILS FLAG` _[required]_ - if set to true, it returns the full transaction objects, if false only the hashes of the transactions.

> Code samples
```shell

curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params": ["0x5BAD55",false],"id":1}'
```

### RESPONSE

#### RESULT FIELDS
- `BLOCK` - A block object, or null when no block was found
- `number`: the block number. Null when the returned block is the pending block.
- `hash`: 32 Bytes - hash of the block. Null when the returned block is the pending block.
- `parentHash`: 32 Bytes - hash of the parent block.
- `nonce`: 8 Bytes - hash of the generated proof-of-work. Null when the returned block is the pending block.
- `sha3Uncles`: 32 Bytes - SHA3 of the uncles data in the block.
- `logsBloom`: 256 Bytes - the bloom filter for the logs of the block. Null when the returned block is the pending block.
- `transactionsRoot`: 32 Bytes - the root of the transaction trie of the block.
- `stateRoot`: 32 Bytes - the root of the final state trie of the block.
- `receiptsRoot`: 32 Bytes - the root of the receipts trie of the block.
- `miner`: 20 Bytes - the address of the beneficiary to whom the mining rewards were given.
- `difficulty`: integer of the difficulty for this block.
- `totalDifficulty`: integer of the total difficulty of the chain until this block.
- `extraData`: the "extra data" field of this block.
- `size`: integer the size of this block in bytes.
- `gasLimit`: the maximum gas allowed in this block.
- `gasUsed`: the total used gas by all transactions in this block.
- `timestamp`: the unix timestamp for when the block was collated.
- `transactions`: Array - Array of transaction objects, or 32 Bytes transaction hashes depending on the last given parameter.
- `uncles`: an Array of uncle hashes.

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "difficulty": "0xbfabcdbd93dda",
    "extraData": "0x737061726b706f6f6c2d636e2d6e6f64652d3132",
    "gasLimit": "0x79f39e",
    "gasUsed": "0x79ccd3",
    "hash": "0xb3b20624f8f0f86eb50dd04688409e5cea4bd02d700bf6e79e9384d47d6a5a35",
    "logsBloom": "0x4848112002a2020aaa0812180045840210020005281600c80104264300080008000491220144461026015300100000128005018401002090a824a4150015410020140400d808440106689b29d0280b1005200007480ca950b15b010908814e01911000054202a020b05880b914642a0000300003010044044082075290283516be82504082003008c4d8d14462a8800c2990c88002a030140180036c220205201860402001014040180002006860810ec0a1100a14144148408118608200060461821802c081000042d0810104a8004510020211c088200420822a082040e10104c00d010064004c122692020c408a1aa2348020445403814002c800888208b1",
    "miner": "0x5a0b54d5dc17e0aadc383d2db43b0a0d3e029c4c",
    "mixHash": "0x3d1fdd16f15aeab72e7db1013b9f034ee33641d92f71c0736beab4e67d34c7a7",
    "nonce": "0x4db7a1c01d8a8072",
    "number": "0x5bad55",
    "parentHash": "0x61a8ad530a8a43e3583f8ec163f773ad370329b2375d66433eb82f005e1d6202",
    "receiptsRoot": "0x5eced534b3d84d3d732ddbc714f5fd51d98a941b28182b6efe6df3a0fe90004b",
    "sha3Uncles": "0x8a562e7634774d3e3a36698ac4915e37fc84a2cd0044cb84fa5d80263d2af4f6",
    "size": "0x41c7",
    "stateRoot": "0xf5208fffa2ba5a3f3a2f64ebd5ca3d098978bedd75f335f56b705d8715ee2305",
    "timestamp": "0x5b541449",
    "totalDifficulty": "0x12ac11391a2f3872fcd",
    "transactions": [
      "0x8784d99762bccd03b2086eabccee0d77f14d05463281e121a62abfebcf0d2d5f",
      "0x311be6a9b58748717ac0f70eb801d29973661aaf1365960d159e4ec4f4aa2d7f",
      "0xe42b0256058b7cad8a14b136a0364acda0b4c36f5b02dea7e69bfd82cef252a2",
      "0x4eb05376055c6456ed883fc843bc43df1dcf739c321ba431d518aecd7f98ca11",
      "0x994dd9e72b212b7dc5fd0466ab75adf7d391cf4f206a65b7ad2a1fd032bb06d7",
      "0xf6feecbb9ab0ac58591a4bc287059b1133089c499517e91a274e6a1f5e7dce53",
      "0x7e537d687a5525259480440c6ea2e1a8469cd98906eaff8597f3d2a44422ff97",
      "0xa762220e92bed6d77a2c19ffc60dad77d71bd5028c5230c896ab4b9552a39b50",
      "0xf1fa677edda7e5add8e794732c7554cd5459a5c12781dc71de73c7937dfb2775",
      "0x3220af8e317fde6dac80b1199f9ceeafe60ada4974a7e04a75fbce1ac4cb46c3",
      "0x5566528978250828168f0d30bcc8a3689d129c75d820d604f7eb84c25b34ec81",
      "0x646c98e323a05862778f0c9063a989b6aefd94f28842a3a09d2edb37a050717d",
      "0xe951ea55764f7e8e0720f7042dd1db67525965302ed974a0c8e3b769bc1818e3",
      "0x7ecf2528b7df3831712501f5c60ef156bf5fcac9912199e0a64afcb963ea91ca",
      "0xc43b89783f68b2844918ea515cc146c006e5f162c9be9aedf5e7a6ae1f32e164",
      "0xd74503ede63d6fd41367796433aa14439902e8f57293a0583e19aa6ebf3f128e",
      "0x021e5b7d3ddac97b4c6cb9c3f333766a533c1ed9fbcfb8b2515c38ecd0c53f89",
      "0xbb3a336e3f823ec18197f1e13ee875700f08f03e2cab75f0d0b118dabb44cba0",
      "0x25f65866dba34783200c25fb1c120b36326c9ad3a47e8bc34c3edbc9208f1378",
      "0x5336f5c4132ef00e8b469ecfd4ee0d6800f6bd60aefb1c62232cbce81c085ae2",
      "0xb87410cfe0a75c004f7637736b3de1e8f4e08e9e2b05ab963622a40a5505664d",
      "0x990857a27ec7cfd6dfd88015173adf81959b5abaff6eefbe8e9df6b0f40f2711",
      "0x3563ccb5734b7b5015122a20b558723afe992ff1109a04b57e02f26edd5a6a38",
      "0xd7885d9412cc494fbe680b016bf7402b633c34c66833b35cad59af2a4aff4f0b",
      "0x48e60927d6fb9ae76f69a6400490b5ffcb2f9da3105fad6c61f21256ef0c217c",
      "0x9e30af26ff3836c4b55af62ba134bc55db662cf1d396cca437d12a8195bfcbe4",
      "0x2476eeede4764c6871f50f3235ebeb9a56d33b41bc3bb1ce3c18c5d710a0609c",
      "0x1cd3520fbb1eb6f2f6f257ab7c3cba957806b0b87182baedb4f81c62868064c1",
      "0x78ae3aee0ff16d8ea4f394b7b80021804e1d9f35cdbb9c6189bb6cbf58bc52c4",
      "0xfcc75bad728b8d302ba0674ebe3122fc50e3b78fe4948ddfc0d37ee987e666ca",
      "0xd2175464d72bcc61b2e07aa3aac742b4184480d7a9f6ae5c2ba24d9c9bb9f304",
      "0x42b56b504e59e42a3dc94e740bb4231e6326daaac7a73ef93ee8db7b96ac5d71",
      "0xd42681091641cd2a71f18299e8e206d5659c3076b1c63adc26f5b7740e230d2b",
      "0x1202c354f0a00b31adf9e3d895e0c8f3896182bb3ab9fc69d6c21d31a1bf279c",
      "0xa5cea1f6957431caf589a8dbb58c102fb191b39967fbe8d26cecf6f28bb835da",
      "0x2045efeb2f5ea9176690ece680d3fd7ca9e945d0d572d17786810d323628f98c",
      "0xbf55d13976616a23114b724b14049eaaf91db3f1950320b5306006a6b648b24f",
      "0x9e5c5ea885eb1d6b1b3ffcf703e3381b7681f7420f35408d30ba93ec0cdf0792",
      "0x6f1a61dc4306ca5e976a1706afe1f32279548df98e0373c5fee0ea189ddb77a0",
      "0xc5c16b30c22ee4f90c3a2de70554f7975eb476592ff13c61986d760da6cf7f9d",
      "0xb09de28497227c0537df0a78797fa00407dcd04a4f90d9de602484b61f7bf169",
      "0x1bfea966fa7772a26b4b2c8add15ceedcb70a903618f5d4603d69f52b9954025",
      "0xe58be9c0e3cedd4444c76d1adc098ba40cbe21ef886b2bfc2edb6ed96ba8d966",
      "0x3a29096f712ccdafd56e9a3c635d4fe2e6224ac3666d466c21da66c8829bbfd6",
      "0x31feab77d7c1c87eb79af54193400c8edad16645e1ea5fcc10f2eaec51fe3992",
      "0x4e0278fce62dca8e23cfae6a020fcd3b2facc03244d54b964bbde424f902ffe1",
      "0x300239a64a50ad0e646c232f85cfa4f3d3ed30090cd574329c782d95c2b42532",
      "0x41755f354b06b4b8a452db1cc9b5c810c75b1bbe236603cbc0950c3c81b80c51",
      "0x1e3fbeffc326f1ffd8559c6024c12557e6014bc02c12d65dbc1baa4e1aed94b7",
      "0x4a459a32cf68e9b7697a3a656432b340d6d27c3d4a513e6cce770d63df99839a",
      "0x3ef484913d185de728c787a1053ec1444ec1c7a5827eecba521d3b406b088a89",
      "0x43afa584c21f27a2747a8397b00d3ec4b460d929b61b510d017f01037a3ded3f",
      "0x44e6a37a6c1d8696fa0537385b9d1bb535b2b3309b5482209e95b5b6c58fc8da",
      "0x2a8bca48147955efcfd697f1a97304ae4cc467a7778741c2c47e516610f0a876",
      "0x4c6bd64c8974f8b949cfe265da1c1bb997e3c886f024b38c99d170acc70b83df",
      "0x103f0cca1ae13600c5be5b217e92430a72b0471d05e283c105f5d0df36438b2a",
      "0x00a06bf6fbd07b3a89ef9031a2108c8fa31b467b33a6edcd6eb3687c158743cf",
      "0x0175496d8265dedd693cf88884626c33b699ebcf4f2110e4c7fb7603c53215b2",
      "0x11fb433ab551b33f30d00a34396835fab72e316e81d1e0afcbc92e79801f30c4",
      "0x060dc4541fd534d107f6e49b96d84f5ec6dbe4eb714890e800bd02399a6bfb7f",
      "0x01956de9f96f9a268c6524fffb9919d7fa3de7a4c25d53c2ccc43d0cb022a7ff",
      "0x15057378f2d223829269ec0f31ba4bb03146134220d34eb8eb7c403aa4a2e569",
      "0x16ea0218d72b5e3f69d0ae4daa8085150f5f7e69ee22a3b054744e35e2082879",
      "0x0baf4e8ff92058c1cac3b95c237edb4d2c12ad41d210356c209f1e0bf0d2d12a",
      "0x1a8ac77aff614caeca16a5a3a0931375a5a4fbe0ef1e15d6d15bf6f8e3c60f4f",
      "0xdb899136f41a3d4710907345b09d241490776383271e6b9887499fd05b80fcd4",
      "0x1007e17b1120d37fb930f953d8a3440ca11b8fd84470eb107c8b4a402a9813fd",
      "0x0910324706ffeebf8aa25ca0784636518bf67e5d173c22438a64dd43d5f4aa2a",
      "0x028f2bee56aee7005abcb2258d6d9f0f078a85a65c3d669aca40564ef4bd7f94",
      "0x14adac9bc94cde3166f4b7d42e8862a745483c708e51afbe89ecd6532acc532e",
      "0x54bed12ccad43523ba8527d1b99f5fa04a55b3a7724cfff2e0a21ec90b08590e",
      "0xcdf05df923f6e418505750069d6486276b15fcc3cd2f42a7044c642d19a86d51",
      "0x0c66977ed87db75074cb2bea66b254af3b20bb3315e8095290ceb1260b1b7449",
      "0x22626e2678da34b505b233ef08fc91ea79c5006dff00e33a442fa51a11e34c25",
      "0xe2989560000a1fc7c434c5e9c4bba82e1501bf435292ac25acc3cb182c1c2cd0",
      "0x348cfc85c58b7f3b2e8bdaa517dc8e3c5f8fb41e3ba235f28892b46bc3484756",
      "0x4ac009cebc1f2416b9e39bcc5b41cd53b1a9239e8f6c0ab043b8830ef1ffc563",
      "0xf2a96682362b9ffe9a77190bcbc47937743b6e1da2c56257f9b562f15bbd3cfa",
      "0xf1cd627c97746bc75727c2f0efa2d0dc66cca1b36d8e45d897e18a9b19af2f60",
      "0x241d89f7888fbcfadfd415ee967882fec6fdd67c07ca8a00f2ca4c910a84c7dd"
    ],
    "transactionsRoot": "0xf98631e290e88f58a46b7032f025969039aa9b5696498efc76baf436fa69b262",
    "uncles": [
      "0x824cce7c7c2ec6874b9fa9a9a898eb5f27cbaf3991dfa81084c3af60d1db618c"
    ]
  }
}
```


## eth_getBlockSignersByNumber

Returns the signers set of the block of given `BLOCKNUMBER`.

#### REQUEST PARAMS
- `BLOCKNUMBER` _[required]_ - a hex code of an integer representing the `BLOCKNUMBER` or one of the following special params:
    - `latest`: get block data of the latest block
    - `pending`:  get block data of pending block
    - `earliest`: get the genesis block

> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getBlockSignersByNumber","params": ["0x1"],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `SIGNERS` - signers set of the block of given `BLOCKNUMBER`

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": [
    "0xffc679dcdf444d2eeb0491a998e7902b411ccf20"
  ]
}

```


## eth_getBlockSignersByHash

Returns the signers set of the block of given `BLOCKHASH`.

#### REQUEST PARAMS
- `BLOCKHASH` _[required]_ - a string representing a `BLOCKHASH` 

> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getBlockSignersByHash","params": ["0x9326145f8a2c8c00bbe13afc7d7f3d9c868b5ef39d89f2f4e9390e9720298624"],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `SIGNERS` - signers set of the block of given `BLOCKHASH`

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": [
    "0xffc679dcdf444d2eeb0491a998e7902b411ccf20"
  ]
}

```


## eth_getBlockFinalityByNumber

Returns the the finality of the block of given `BLOCKNUMBER`.

#### REQUEST PARAMS
- `BLOCKNUMBER` _[required]_ - a hex code of an integer representing the `BLOCKNUMBER` or one of the following special params:
    - `latest`: get block data of the latest block
    - `pending`:  get block data of pending block
    - `earliest`: get the genesis block

> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getBlockFinalityByNumber","params": ["0x1"],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `BLOCK_FINALITY` - integer of the the finality of the block of given `BLOCKNUMBER`

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 33
}

```


## eth_getBlockFinalityByHash

Returns the signers set of the block of given `BLOCKHASH`.

#### REQUEST PARAMS
- `BLOCKHASH` _[required]_ - a string representing a `BLOCKHASH` 

> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getBlockFinalityByHash","params": ["0xc186660e3cdd390cf4c7861ebc7ec358f0a5c258f0dec324c44581a3abdef90f"],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `BLOCK_FINALITY` - integer of the the finality of the block of given `BLOCKHASH`

> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 33
}
```


## eth_getCandidates

Returns the statuses of all candidates at a specific epoch

#### REQUEST PARAMS
- `EPOCH_NUMBER` _[required]_ - a hex code of an integer representing the `EPOCH_NUMBER` or the following special param:
    - `latest`: get the status of candidate at the current time


> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getCandidates","params": ["latest"],"id":1}'

```

### RESPONSE

#### RESULT FIELDS

- `EPOCH` - the epoch number of the query of this request
- `CANDIDATES` - list of candidates along with their statuses and capacities
  - `STATUS` - a string representing status of the corresponding candidate
    - `MASTERNODE` - if the candidate is a masternode
    - `SLASHED` - if the candidate is slashed
    - `PROPOSED` - if the candidate is proposed, have not been a masternode yet
    - empty string - if it's not a candidate
  - `CAPACITY` - capacity of the corresponding candidate
- `SUCCESS` - true if the request is successful, otherwise it's false
> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "candidates": {
      "0x059F8114D61AEb2043FA59D39e3872792F653360": {
        "capacity": 52000,
        "status": "MASTERNODE"
      },
      "0x4130393462664146336537643436314131453641": {
        "capacity": 51000,
        "status": "PROPOSED"
      },
      "0x66414BC8D36eCEa132F969B7596cAb2Ba1818b7d": {
        "capacity": 52000,
        "status": "SLASHED"
      },
      "0xB7e038b0229A97c9CB7AD798aA51757E1017A7D4": {
        "capacity": 52000,
        "status": "MASTERNODE"
      },
      "0xDD1BE874E267E5661faEA094bfAF3e7d461A1E6A": {
        "capacity": 52000,
        "status": "MASTERNODE"
      },
      "0xa8D38FB29CDA4Ca011b430a680886fB4CA7F3043": {
        "capacity": 52000,
        "status": "MASTERNODE"
      }
    },
    "epoch": 1786,
    "success": true
  }
}

```


## eth_getCandidateStatus

Returns the status of the candidate of given `COINBASE_ADDRESS` at a specific epoch

#### REQUEST PARAMS
- `COINBASE_ADDRESS` _[required]_ - a string representing a `COINBASE_ADDRESS` (length: 40, start with `0x` )
- `EPOCH_NUMBER` _[required]_ - a hex code of an integer representing the `EPOCH_NUMBER` or the following special param:
    - `latest`: get the status of candidate at the current time


> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getCandidateStatus","params": ["0x1d50df657b6dce50bac634bf18e2d986d807e940", "latest"],"id":1}'

```

### RESPONSE

#### RESULT FIELDS
- `STATUS` - a string representing status of the candicate of given `COINBASE_ADDRESS`
  - `MASTERNODE` - if the candidate is a masternode
  - `SLASHED` - if the candidate is slashed
  - `PROPOSED` - if the candidate is proposed, have not been a masternode yet
  - empty string - if it's not a candidate
- `CAPACITY` - capacity of the candidate
- `EPOCH` - the epoch number of the query of this request
- `SUCCESS` - true if the request is successful, otherwise it's false
> Example response

> 200 Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "capacity": 51000,
    "epoch": 1727,
    "status": "PROPOSED",
    "success": true
  }
}
```


## eth_getTransactionByHash

Returns information about a transaction for a given hash.

### REQUEST

`POST https://rpc.tomochain.com`

#### HEADERS

`Content-Type: application/json`

#### REQUEST PARAMS
- `TRANSACTION HASH` _[required]_ - a string representing the hash (32 bytes) of a transaction

> Code samples 

```shell
curl https://rpc.tomochain.com \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"eth_getTransactionByHash","params": ["0xbb3a336e3f823ec18197f1e13ee875700f08f03e2cab75f0d0b118dabb44cba0"],"id":1}'
```

### RESPONSE

#### RESULT FIELDS
- `TRANSACTION` - A transaction object, or null when no transaction was found
- `hash`: 32 Bytes - hash of the transaction.
- `nonce`: the number of transactions made by the sender prior to this one.
- `blockHash`: 32 Bytes - hash of the block where this transaction was in. null when its pending.
- `blockNumber`: block number where this transaction was in. null when its pending.
- `transactionIndex`: integer of the transactions index position in the block. null when its pending.
- `from`: 20 Bytes - address of the sender.
- `to`: 20 Bytes - address of the receiver. null when its a contract creation transaction.
- `value`: value transferred in Wei.
- `gasPrice`: gas price provided by the sender in Wei.
- `gas`: gas provided by the sender.
- `input`: the data send along with the transaction.

> Example response

> 200 Response

```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockHash": "0xb3b20624f8f0f86eb50dd04688409e5cea4bd02d700bf6e79e9384d47d6a5a35",
    "blockNumber": "0x5bad55",
    "from": "0x398137383b3d25c92898c656696e41950e47316b",
    "gas": "0x1d45e",
    "gasPrice": "0xfa56ea00",
    "hash": "0xbb3a336e3f823ec18197f1e13ee875700f08f03e2cab75f0d0b118dabb44cba0",
    "input": "0xf7d8c88300000000000000000000000000000000000000000000000000000000000cee6100000000000000000000000000000000000000000000000000000000000ac3e1",
    "nonce": "0x18",
    "r": "0x2a378831cf81d99a3f06a18ae1b6ca366817ab4d88a70053c41d7a8f0368e031",
    "s": "0x450d831a05b6e418724436c05c155e0a1b7b921015d0fbc2f667aed709ac4fb5",
    "to": "0x06012c8cf97bead5deae237070f9587f8e7a266d",
    "transactionIndex": "0x11",
    "v": "0x25",
    "value": "0x1c6bf526340000"
  }
}
```


<h1 id="tomoscan-apis">TomoScan APIs v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

TomoScan APIs

License: <a href="https://github.com/tomochain/tomoscan">Github</a>

Base URL: https://scan.tomochain.com

<h1 id="tomoscan-apis-accounts">Accounts</h1>

Accounts API

## Get list accounts

> Code samples

```shell
# You can also use wget
curl -X GET /api/accounts

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/accounts',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/accounts", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/accounts',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/accounts', params={

)

print r.json()

```

`GET /api/accounts`

<h3 id="get-list-accounts-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|page|query|number|false|default = 1|
|limit|query|number|false|default 20, maximum = 50|

<h3 id="get-list-accounts-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get account detail

> Code samples

```shell
# You can also use wget
curl -X GET /api/accounts/{hash}

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/accounts/{hash}',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/accounts/{hash}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/accounts/{hash}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/accounts/{hash}', params={

)

print r.json()

```

`GET /api/accounts/{hash}`

<h3 id="get-account-detail-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|hash|path|string|true|account address|

<h3 id="get-account-detail-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get list block create

> Code samples

```shell
# You can also use wget
curl -X GET /api/accounts/{hash}/mined

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/accounts/{hash}/mined',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/accounts/{hash}/mined", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/accounts/{hash}/mined',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/accounts/{hash}/mined', params={

)

print r.json()

```

`GET /api/accounts/{hash}/mined`

<h3 id="get-list-block-create-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|hash|path|string|true|account address|
|page|query|number|false|default = 1|
|limit|query|number|false|default 20, maximum = 50|

<h3 id="get-list-block-create-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get list token transactions. Require 1 of 2 conditions - address | token

> Code samples

```shell
# You can also use wget
curl -X GET /api/token-txs

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/token-txs',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/token-txs", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/token-txs',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/token-txs', params={

)

print r.json()

```

`GET /api/token-txs`

<h3 id="get-list-token-transactions.-require-1-of-2-conditions---address-|-token-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|address|query|string|false|account address|
|token|path|string|true|token address|
|page|query|number|false|default = 1|
|limit|query|number|false|default 20, maximum = 50|

<h3 id="get-list-token-transactions.-require-1-of-2-conditions---address-|-token-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get list token holder. Require 1 of 2 conditions - address | hassh

> Code samples

```shell
# You can also use wget
curl -X GET /api/token-holders

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/token-holders',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/token-holders", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/token-holders',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/token-holders', params={

)

print r.json()

```

`GET /api/token-holders`

<h3 id="get-list-token-holder.-require-1-of-2-conditions---address-|-hassh-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|address|query|string|false|token address|
|hash|path|string|true|account address|
|page|query|number|false|default = 1|
|limit|query|number|false|default 20, maximum = 50|

<h3 id="get-list-token-holder.-require-1-of-2-conditions---address-|-hassh-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomoscan-apis-blocks">Blocks</h1>

Blocks API

## Get list blocks

> Code samples

```shell
# You can also use wget
curl -X GET /api/blocks

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/blocks',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/blocks", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/blocks',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/blocks', params={

)

print r.json()

```

`GET /api/blocks`

<h3 id="get-list-blocks-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|page|query|number|false|default = 1|
|limit|query|number|false|default 20, maximum = 50|

<h3 id="get-list-blocks-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get block detail

> Code samples

```shell
# You can also use wget
curl -X GET /api/blocks/{hash}

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/blocks/{hash}',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/blocks/{hash}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/blocks/{hash}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/blocks/{hash}', params={

)

print r.json()

```

`GET /api/blocks/{hash}`

<h3 id="get-block-detail-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|hash|path|string|true|block number or block hash|

<h3 id="get-block-detail-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get list signers of a block

> Code samples

```shell
# You can also use wget
curl -X GET /api/blocks/signers/{blockNumber}

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/blocks/signers/{blockNumber}',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/blocks/signers/{blockNumber}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/blocks/signers/{blockNumber}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/blocks/signers/{blockNumber}', params={

)

print r.json()

```

`GET /api/blocks/signers/{blockNumber}`

<h3 id="get-list-signers-of-a-block-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|blockNumber|path|number|true|account address|

<h3 id="get-list-signers-of-a-block-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomoscan-apis-transactions">Transactions</h1>

Transactions API

## Get list blocks. Params limit & page & ((address & tx_account) | block | type)

> Code samples

```shell
# You can also use wget
curl -X GET /api/txs

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/txs',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/txs", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/txs',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/txs', params={

)

print r.json()

```

`GET /api/txs`

<h3 id="get-list-blocks.-params-limit-&-page-&-((address-&-tx_account)-|-block-|-type)-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|page|query|number|false|default = 1|
|limit|query|number|false|default 20, maximum = 50|
|address|query|string|false|list tx of address, group with tx_account|
|tx_account|query|string|false|in|out, default = all, group with address|
|block|query|number|false|list tx of a block|
|type|query|string|false|signTxs|otherTxs|pending|all|

<h3 id="get-list-blocks.-params-limit-&-page-&-((address-&-tx_account)-|-block-|-type)-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get transaction detail

> Code samples

```shell
# You can also use wget
curl -X GET /api/txs/{hash}

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/txs/{hash}',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/txs/{hash}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/txs/{hash}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/txs/{hash}', params={

)

print r.json()

```

`GET /api/txs/{hash}`

<h3 id="get-transaction-detail-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|hash|path|string|true|transaction hash|

<h3 id="get-transaction-detail-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomoscan-apis-tokens">Tokens</h1>

Tokens API

## Get token detail

> Code samples

```shell
# You can also use wget
curl -X GET /api/tokens/{hash}

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/tokens/{hash}',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/tokens/{hash}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/tokens/{hash}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/tokens/{hash}', params={

)

print r.json()

```

`GET /api/tokens/{hash}`

<h3 id="get-token-detail-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|hash|path|string|true|token address|

<h3 id="get-token-detail-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomoscan-apis-token">Token</h1>

## Get list tokens

> Code samples

```shell
# You can also use wget
curl -X GET /api/tokens

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/tokens',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/tokens", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/tokens',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/tokens', params={

)

print r.json()

```

`GET /api/tokens`

<h3 id="get-list-tokens-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|page|query|number|false|default = 1|
|limit|query|number|false|default 20, maximum = 50|

<h3 id="get-list-tokens-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomoscan-apis-rewards">Rewards</h1>

## Get list rewards of a voter

> Code samples

```shell
# You can also use wget
curl -X GET /api/rewards/{voter}

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/rewards/{voter}',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/rewards/{voter}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/rewards/{voter}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/rewards/{voter}', params={

)

print r.json()

```

`GET /api/rewards/{voter}`

<h3 id="get-list-rewards-of-a-voter-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|voter|path|number|true|account address|
|page|query|number|false|default = 1|
|limit|query|number|false|default 20, maximum = 50|

<h3 id="get-list-rewards-of-a-voter-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get list reward of an epoch

> Code samples

```shell
# You can also use wget
curl -X GET /api/rewards/epoch/{epochNumber}

```

```javascript--nodejs
const fetch = require('node-fetch');

fetch('/api/rewards/epoch/{epochNumber}',
{
  method: 'GET'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/rewards/epoch/{epochNumber}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

result = RestClient.get '/api/rewards/epoch/{epochNumber}',
  params: {
  }

p JSON.parse(result)

```

```python
import requests

r = requests.get('/api/rewards/epoch/{epochNumber}', params={

)

print r.json()

```

`GET /api/rewards/epoch/{epochNumber}`

<h3 id="get-list-reward-of-an-epoch-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|epochNumber|path|number|true|epoch number|
|hash|path|string|true|account address|

<h3 id="get-list-reward-of-an-epoch-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>


<h1 id="tomomaster-apis">TomoMaster APIs v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

Happy to code TomoMaster APIs

License: <a href="https://github.com/tomochain/tomomaster">Github</a>

Base URL: https://master.tomochain.com

<h1 id="tomomaster-apis-config">Config</h1>

Get TomoMaster Application Configuration

## Get TomoMaster Application Configuration

> Code samples

```shell
# You can also use wget
curl -X GET /api/config \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/config',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/config", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/config',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/config', params={

}, headers = headers)

print r.json()

```

`GET /api/config`

> Example responses

> 200 Response

```json
{
  "blockchain": {
    "rpc": "string",
    "ws": "string",
    "epoch": 900,
    "blockTime": 0
  },
  "explorerUrl": "string",
  "GA": "string"
}
```

<h3 id="get-tomomaster-application-configuration-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[config](#schemaconfig)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|None|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server Internal Error|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomomaster-apis-candidates">Candidates</h1>

Get Candidates information

## Get candidates information

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates`

<h3 id="get-candidates-information-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|number|false|Number of record in a query|
|page|query|number|false|Page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "123",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "__v": 0,
      "capacity": "91540333800000001000000",
      "createdAt": "2018-10-31T03:42:39.375Z",
      "owner": "0x11621900588eca4410c00097a9f59237f34064cd",
      "status": "RESIGNED",
      "updatedAt": "2019-01-11T09:21:55.028Z",
      "latestSignedBlock": 2917487,
      "capacityNumber": 91540.33380000001,
      "isMasternode": false,
      "isPenalty": false
    }
  ],
  "total": 100,
  "activeCandidates": 10
}
```

<h3 id="get-candidates-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[candidate](#schemacandidate)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get candidate's information

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate} \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}`

<h3 id="get-candidate's-information-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|

> Example responses

> 200 Response

```json
{
  "_id": "123",
  "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
  "smartContractAddress": "0x0000000000000000000000000000000000000088",
  "__v": 0,
  "capacity": "91540333800000001000000",
  "createdAt": "2018-10-31T03:42:39.375Z",
  "owner": "0x11621900588eca4410c00097a9f59237f34064cd",
  "status": "RESIGNED",
  "updatedAt": "2019-01-11T09:17:59.535Z",
  "latestSignedBlock": "2917487",
  "capacityNumber": 91540.33380000001,
  "isMasternode": false,
  "isPenalty": false
}
```

<h3 id="get-candidate's-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[candidateDetail](#schemacandidatedetail)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get voters who voted for the candidate

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate}/voters \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}/voters',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}/voters", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}/voters',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}/voters', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}/voters`

<h3 id="get-voters-who-voted-for-the-candidate-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|
|limit|query|number|false|Number of record in a query|
|page|query|number|false|Page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5bd924a9aa41b819395d9207",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "voter": "0xf2cce442c7ab5baf194838081b5f9396330ecfb8",
      "__v": 0,
      "capacity": "105000000000000000000",
      "createdAt": "2018-10-31T03:42:33.922Z",
      "updatedAt": "2019-01-05T02:11:31.489Z",
      "capacityNumber": 105
    }
  ],
  "total": 100
}
```

<h3 id="get-voters-who-voted-for-the-candidate-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[candidateVoter](#schemacandidatevoter)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Masternode checking

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate}/isMasternode \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}/isMasternode',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}/isMasternode", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}/isMasternode',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}/isMasternode', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}/isMasternode`

<h3 id="masternode-checking-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|

> Example responses

> 200 Response

```json
"1"
```

<h3 id="masternode-checking-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[isMasternode](#schemaismasternode)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Candidate checking

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate}/isCandidate \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}/isCandidate',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}/isCandidate", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}/isCandidate',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}/isCandidate', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}/isCandidate`

<h3 id="candidate-checking-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|

> Example responses

> 200 Response

```json
"1"
```

<h3 id="candidate-checking-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[isCandidate](#schemaiscandidate)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get reward of candidate

> Code samples

```shell
# You can also use wget
curl -X GET /api/candidates/{candidate}/{owner}/getRewards \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/candidates/{candidate}/{owner}/getRewards',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/candidates/{candidate}/{owner}/getRewards", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/candidates/{candidate}/{owner}/getRewards',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/candidates/{candidate}/{owner}/getRewards', params={

}, headers = headers)

print r.json()

```

`GET /api/candidates/{candidate}/{owner}/getRewards`

<h3 id="get-reward-of-candidate-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|
|owner|path|string|true|owner's address|
|limit|query|number|false|number of records|
|page|query|number|false|page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5c19847f0e77307940be9216",
      "epoch": 3193,
      "startBlock": 2872801,
      "endBlock": 2873700,
      "address": "0x11621900588eca4410c00097a9f59237f34064cd",
      "validator": "0x11621900588eca4410c00097a9f59237f34064cd",
      "reason": "Voter",
      "lockBalance": "1000",
      "reward": "8.03540381764608993247",
      "rewardTime": "2018-12-18T23:36:18.000Z",
      "signNumber": 843,
      "__v": 0,
      "createdAt": "2018-12-18T23:36:31.435Z",
      "updatedAt": "2018-12-18T23:36:31.435Z"
    }
  ],
  "total": 100
}
```

<h3 id="get-reward-of-candidate-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[candidateRewards](#schemacandidaterewards)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomomaster-apis-voters">Voters</h1>

Get Voter information

## Get voted candidates

> Code samples

```shell
# You can also use wget
curl -X GET /api/voters/{voter}/candidates \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/voters/{voter}/candidates',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/voters/{voter}/candidates", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/voters/{voter}/candidates',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/voters/{voter}/candidates', params={

}, headers = headers)

print r.json()

```

`GET /api/voters/{voter}/candidates`

<h3 id="get-voted-candidates-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|voter|path|string|true|voter's address|
|limit|query|number|false|Number of record in a query|
|page|query|number|false|Page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "candidate": "0xfc5571921c6d3672e13b58ea23dea534f2b35fa0",
      "capacity": "10000000000000000000",
      "capacityNumber": 10,
      "candidateName": "Earth"
    }
  ],
  "total": 100
}
```

<h3 id="get-voted-candidates-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[voterCandidates](#schemavotercandidates)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get reward of voter

> Code samples

```shell
# You can also use wget
curl -X GET /api/voters/{voter}/rewards \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/voters/{voter}/rewards',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/voters/{voter}/rewards", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/voters/{voter}/rewards',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/voters/{voter}/rewards', params={

}, headers = headers)

print r.json()

```

`GET /api/voters/{voter}/rewards`

<h3 id="get-reward-of-voter-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|voter|path|string|true|candidate's address|
|limit|query|number|false|number of records|
|page|query|number|false|page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5c19847f0e77307940be922a",
      "epoch": 3193,
      "startBlock": 2872801,
      "endBlock": 2873700,
      "address": "0x11621900588eca4410c00097a9f59237f34064cd",
      "validator": "0x11621900588eca4410c00097a9f59237f34064cd",
      "reason": "MasterNode",
      "lockBalance": "1000",
      "reward": "25.97042513863216266174",
      "rewardTime": "2018-12-18T23:36:18.000Z",
      "signNumber": 843,
      "__v": 0,
      "createdAt": "2018-12-18T23:36:31.580Z",
      "updatedAt": "2018-12-18T23:36:31.580Z",
      "candidateName": "0x11621900588eca4410c00097a9f59237f34064cd"
    }
  ],
  "total": 100
}
```

<h3 id="get-reward-of-voter-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[voterRewards](#schemavoterrewards)|
|406|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|Not Acceptable|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="tomomaster-apis-transaction">Transaction</h1>

Get transactions of candidate and voter

## Get transactions of a candidate

> Code samples

```shell
# You can also use wget
curl -X GET /api/transactions/candidate/{candidate} \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/transactions/candidate/{candidate}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/transactions/candidate/{candidate}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/transactions/candidate/{candidate}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/transactions/candidate/{candidate}', params={

}, headers = headers)

print r.json()

```

`GET /api/transactions/candidate/{candidate}`

<h3 id="get-transactions-of-a-candidate-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|candidate|path|string|true|candidate's address|
|limit|query|number|false|number of records|
|page|query|number|false|page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5c247c545e769d2f2c10ab38",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "tx": "0x0f96e419c89dcf1397a6206959334a4485c5a158a0320cb8a8e98db3b7888141",
      "event": "Vote",
      "voter": "0xe91dc9746eed1b5971aabd6e1681da1a4d06be8d",
      "owner": "",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "capacity": "11000000000000000000",
      "blockNumber": 2897395,
      "createdAt": "2018-12-27T07:16:36.000Z",
      "__v": 0
    }
  ],
  "total": 100
}
```

<h3 id="get-transactions-of-a-candidate-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[txCandidate](#schematxcandidate)|

<aside class="success">
This operation does not require authentication
</aside>

## Get transactions of a voter

> Code samples

```shell
# You can also use wget
curl -X GET /api/transactions/voter/{voter} \
  -H 'Accept: application/json'

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('/api/transactions/voter/{voter}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/transactions/voter/{voter}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get '/api/transactions/voter/{voter}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/transactions/voter/{voter}', params={

}, headers = headers)

print r.json()

```

`GET /api/transactions/voter/{voter}`

<h3 id="get-transactions-of-a-voter-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|voter|path|string|true|voter's address|
|limit|query|number|false|number of records|
|page|query|number|false|page number|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "_id": "5c24a189ff305840a2498bf0",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "tx": "0xf8f2d402c6b1cb5f891b687d69ddcd920e58d9e9fe002857cac0e7ce47998884",
      "event": "Unvote",
      "voter": "0x487d62d33467c4842c5e54eb370837e4e88bba0f",
      "owner": "",
      "candidate": "0xfc5571921c6d3672e13b58ea23dea534f2b35fa0",
      "capacity": "10000999000000000000000",
      "blockNumber": 763397,
      "createdAt": "2018-12-27T09:55:21.000Z",
      "__v": 0
    }
  ],
  "total": 100
}
```

<h3 id="get-transactions-of-a-voter-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[txVoter](#schematxvoter)|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocSconfig">config</h2>

<a id="schemaconfig"></a>

```json
{
  "blockchain": {
    "rpc": "string",
    "ws": "string",
    "epoch": 900,
    "blockTime": 0
  },
  "explorerUrl": "string",
  "GA": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|blockchain|object|false|none|Tomochain's configurations|
|» rpc|string|false|none|rpc|
|» ws|string|false|none|websocket|
|» epoch|number|false|none|Number of blocks for 1 epoch|
|» blockTime|number|false|none|Block time|
|explorerUrl|string|false|none|Tomoscan's API|
|GA|string|false|none|Google Analytic code|

<h2 id="tocScandidate">candidate</h2>

<a id="schemacandidate"></a>

```json
{
  "items": [
    {
      "_id": "123",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "__v": 0,
      "capacity": "91540333800000001000000",
      "createdAt": "2018-10-31T03:42:39.375Z",
      "owner": "0x11621900588eca4410c00097a9f59237f34064cd",
      "status": "RESIGNED",
      "updatedAt": "2019-01-11T09:21:55.028Z",
      "latestSignedBlock": 2917487,
      "capacityNumber": 91540.33380000001,
      "isMasternode": false,
      "isPenalty": false
    }
  ],
  "total": 100,
  "activeCandidates": 10
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's data|
|total|number|false|none|Total number of candidate|
|activeCandidates|number|false|none|Number of active candidate|

<h2 id="tocScandidatedetail">candidateDetail</h2>

<a id="schemacandidatedetail"></a>

```json
{
  "_id": "123",
  "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
  "smartContractAddress": "0x0000000000000000000000000000000000000088",
  "__v": 0,
  "capacity": "91540333800000001000000",
  "createdAt": "2018-10-31T03:42:39.375Z",
  "owner": "0x11621900588eca4410c00097a9f59237f34064cd",
  "status": "RESIGNED",
  "updatedAt": "2019-01-11T09:17:59.535Z",
  "latestSignedBlock": "2917487",
  "capacityNumber": 91540.33380000001,
  "isMasternode": false,
  "isPenalty": false
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|_id|string|false|none|id|
|candidate|string|false|none|candidate's address|
|smartContractAddress|string|false|none|smart contract's address|
|__v|number|false|none|__v|
|capacity|string|false|none|capacity in wei|
|createdAt|string|false|none|creation date of candidate|
|owner|string|false|none|owner's address|
|status|string|false|none|candidate's status|
|updatedAt|string|false|none|update time|
|latestSignedBlock|string|false|none|latest signed block|
|capacityNumber|number|false|none|capacity number|
|isMasternode|boolean|false|none|is masternode|
|isPenalty|boolean|false|none|is penalty|

<h2 id="tocScandidaterewards">candidateRewards</h2>

<a id="schemacandidaterewards"></a>

```json
{
  "items": [
    {
      "_id": "5c19847f0e77307940be9216",
      "epoch": 3193,
      "startBlock": 2872801,
      "endBlock": 2873700,
      "address": "0x11621900588eca4410c00097a9f59237f34064cd",
      "validator": "0x11621900588eca4410c00097a9f59237f34064cd",
      "reason": "Voter",
      "lockBalance": "1000",
      "reward": "8.03540381764608993247",
      "rewardTime": "2018-12-18T23:36:18.000Z",
      "signNumber": 843,
      "__v": 0,
      "createdAt": "2018-12-18T23:36:31.435Z",
      "updatedAt": "2018-12-18T23:36:31.435Z"
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's data|
|total|number|false|none|Number of candidate|

<h2 id="tocScandidatevoter">candidateVoter</h2>

<a id="schemacandidatevoter"></a>

```json
{
  "items": [
    {
      "_id": "5bd924a9aa41b819395d9207",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "voter": "0xf2cce442c7ab5baf194838081b5f9396330ecfb8",
      "__v": 0,
      "capacity": "105000000000000000000",
      "createdAt": "2018-10-31T03:42:33.922Z",
      "updatedAt": "2019-01-05T02:11:31.489Z",
      "capacityNumber": 105
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's data|
|total|number|false|none|Total number of voters|

<h2 id="tocSvotercandidates">voterCandidates</h2>

<a id="schemavotercandidates"></a>

```json
{
  "items": [
    {
      "candidate": "0xfc5571921c6d3672e13b58ea23dea534f2b35fa0",
      "capacity": "10000000000000000000",
      "capacityNumber": 10,
      "candidateName": "Earth"
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's data|
|total|number|false|none|Total number of rewards|

<h2 id="tocSvoterrewards">voterRewards</h2>

<a id="schemavoterrewards"></a>

```json
{
  "items": [
    {
      "_id": "5c19847f0e77307940be922a",
      "epoch": 3193,
      "startBlock": 2872801,
      "endBlock": 2873700,
      "address": "0x11621900588eca4410c00097a9f59237f34064cd",
      "validator": "0x11621900588eca4410c00097a9f59237f34064cd",
      "reason": "MasterNode",
      "lockBalance": "1000",
      "reward": "25.97042513863216266174",
      "rewardTime": "2018-12-18T23:36:18.000Z",
      "signNumber": 843,
      "__v": 0,
      "createdAt": "2018-12-18T23:36:31.580Z",
      "updatedAt": "2018-12-18T23:36:31.580Z",
      "candidateName": "0x11621900588eca4410c00097a9f59237f34064cd"
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Voter's reward array|
|total|number|false|none|Number of candidate|

<h2 id="tocSismasternode">isMasternode</h2>

<a id="schemaismasternode"></a>

```json
"1"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|number|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|1|
|*anonymous*|0|

<h2 id="tocSiscandidate">isCandidate</h2>

<a id="schemaiscandidate"></a>

```json
"1"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|number|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|1|
|*anonymous*|0|

<h2 id="tocStxcandidate">txCandidate</h2>

<a id="schematxcandidate"></a>

```json
{
  "items": [
    {
      "_id": "5c247c545e769d2f2c10ab38",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "tx": "0x0f96e419c89dcf1397a6206959334a4485c5a158a0320cb8a8e98db3b7888141",
      "event": "Vote",
      "voter": "0xe91dc9746eed1b5971aabd6e1681da1a4d06be8d",
      "owner": "",
      "candidate": "0x11621900588eca4410c00097a9f59237f34064cd",
      "capacity": "11000000000000000000",
      "blockNumber": 2897395,
      "createdAt": "2018-12-27T07:16:36.000Z",
      "__v": 0
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's transactions array|
|total|number|false|none|Number of candidate|

<h2 id="tocStxvoter">txVoter</h2>

<a id="schematxvoter"></a>

```json
{
  "items": [
    {
      "_id": "5c24a189ff305840a2498bf0",
      "smartContractAddress": "0x0000000000000000000000000000000000000088",
      "tx": "0xf8f2d402c6b1cb5f891b687d69ddcd920e58d9e9fe002857cac0e7ce47998884",
      "event": "Unvote",
      "voter": "0x487d62d33467c4842c5e54eb370837e4e88bba0f",
      "owner": "",
      "candidate": "0xfc5571921c6d3672e13b58ea23dea534f2b35fa0",
      "capacity": "10000999000000000000000",
      "blockNumber": 763397,
      "createdAt": "2018-12-27T09:55:21.000Z",
      "__v": 0
    }
  ],
  "total": 100
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[object]|false|none|Candidate's transactions array|
|total|number|false|none|Number of candidate|

