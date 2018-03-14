## bitcore-opcodes
[OP_RETURN](https://en.bitcoin.it/wiki/OP_RETURN) is a script opcode used to mark a transaction output as invalid.

It can be used by Proof of Existence, Digital Arts, Assets and others.

In order to find the OP_RETURN code quickly, bitcore-opcodes is the best choice.

## Prerequisites

- [Bitcore 5.x](https://github.com/bitpay/bitcore)

## Usage
[Follow this guide](https://blog.bitpay.com/bitcore-v5/) to install and run a full Bitcore node.

Assuming the created Bitcore node is called ___mynode___ and resides in your home directory

```bash
cd ~/mynode
npm install @poexio/bitcore-opcodes
```

Add ___bitcore-opcodes___ as a dependency in ~/mynode/bitcore-node.json

```javascript
{
  "version": "5.0.0-beta.44",
  "network": "testnet",
  "port": 3001,
  "services": [
    "address",
    "block",
    "db",
    "fee",
    "header",
    "mempool",
    "p2p",
    "timestamp",
    "transaction",
    "web",
    "insight-api",
    "@poexio/bitcore-opcodes"
  ],
  "datadir": "./data"
}
```

Start bitcore-node, then you can access the service with `http://localhost:3001/opcodes`

## API HTTP Endpoints
We can support btc mainnet, testnet3 and regtest

### Hash
Get the transactions that contain the opcodes.

Resource | Method | Request Object | Return Object
-------- | -------|----------------|---------------
/hash/:hash[?limit=1] | GET | [OP_RETURN data](https://bitcore.io/api/lib/transaction#Transaction+addData) | Array

NOTE:

Range of limit: [1, 100], default: 10

* Usage:
```bash
curl http://localhost:3001/opcodes/hash/444f4350524f4f465efa245c88af3bc0bf9e4392976cedafd9a0de8d3f737ba0f48231b0f9262110
curl http://localhost:3001/opcodes/hash/444f4350524f4f465efa245c88af3bc0bf9e4392976cedafd9a0de8d3f737ba0f48231b0f9262110?limit=1
```

This would return (for testnet):

```
[
  {
    "hash": "00000000f959a5ed22dfa034f7957adbda91b3756700dbd29c640ca581bdba22", //blockhash
    "height": "1287345",                                                        //blockheight
    "txid": "30e24f7132635c6b278e9d505112788ca8234dfe15ac545288d33fb675dfdf4c", //tx hash
    "outputIndex": "0"                                                          //output index for sort
  }
]
```
