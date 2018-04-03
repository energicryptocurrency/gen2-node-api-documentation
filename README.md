# core-api-documentation
JSON/REST API Documentation for Energi Core

# Addressindex

## `getaddressbalance`

Returns the balance for an address(es) (requires addressindex to be enabled).

#### Arguments:
```
{
  "addresses"
    [
      "address"  (string) The base58check encoded address
      ,...
    ]
}
```

#### Result:
```
{
  "balance"  (string) The current balance in atoms
  "received"  (string) The total number of atoms received (including change)
}
```

#### #### Examples:
```
> energi-cli getaddressbalance '{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}'
```

```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressbalance", "params": [{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getaddressdeltas

Returns all changes for an address (requires addressindex to be enabled).

#### Arguments:
```
{
  "addresses"
    [
      "address"  (string) The base58check encoded address
      ,...
    ]
  "start" (number) The start block height
  "end" (number) The end block height
}
```

#### Result:
```
[
  {
    "satoshis"  (number) The difference of atoms
    "txid"  (string) The related txid
    "index"  (number) The related input or output index
    "blockindex"  (number) The related block index
    "height"  (number) The block height
    "address"  (string) The base58check encoded address
  }
]
```

#### #### Examples:
```
> energi-cli getaddressdeltas '{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}'
```

```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressdeltas", "params": [{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getaddressmempool

Returns all mempool deltas for an address (requires addressindex to be enabled).

#### Arguments:
```
{
  "addresses"
    [
      "address"  (string) The base58check encoded address
      ,...
    ]
}
```

#### Result:
```
[
  {
    "address"  (string) The base58check encoded address
    "txid"  (string) The related txid
    "index"  (number) The related input or output index
    "satoshis"  (number) The difference of atoms
    "timestamp"  (number) The time the transaction entered the mempool (seconds)
    "prevtxid"  (string) The previous txid (if spending)
    "prevout"  (string) The previous transaction output index (if spending)
  }
]
```

#### Examples:
```
> energi-cli getaddressmempool '{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}'
```

```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressmempool", "params": [{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getaddresstxids

Returns the txids for an address(es) (requires addressindex to be enabled).

#### Arguments:
```
{
  "addresses"
    [
      "address"  (string) The base58check encoded address
      ,...
    ]
  "start" (number) The start block height
  "end" (number) The end block height
}
```

#### Result:
```
[
  "transactionid"  (string) The transaction id
  ,...
]
```

#### Examples:
```
> energi-cli getaddresstxids '{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}'
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddresstxids", "params": [{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```
## getaddressutxos

Returns all unspent outputs for an address (requires addressindex to be enabled).

#### Arguments:
```
{
  "addresses"
    [
      "address"  (string) The base58check encoded address
      ,...
    ]
}
```

#### Result:
```
[
  {
    "address"  (string) The address base58check encoded
    "txid"  (string) The output txid
    "outputIndex"  (number) The output index
    "script"  (string) The script hex encoded
    "satoshis"  (number) The number of atoms of the output
    "height"  (number) The block height
  }
]
```

#### Examples:
```
> energi-cli getaddressutxos '{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}'
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressutxos", "params": [{"addresses": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"]}] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getbestblockhash

Returns the hash of the best (tip) block in the longest block chain.

#### Result:
```
"hex"      (string) the block hash hex encoded
```

#### Examples:
```
> energi-cli getbestblockhash
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbestblockhash", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getblock "hash" ( verbose )

If verbose is false, returns a string that is serialized, hex-encoded data for block 'hash'.
If verbose is true, returns an Object with information about block <hash>.

#### Arguments:
```
1. "hash"          (string, required) The block hash
2. verbose           (boolean, optional, default=true) true for a json object, false for the hex encoded data

```

#### Result: (for verbose = true):
```
{
  "hash" : "hash",     (string) the block hash (same as provided)
  "confirmations" : n,   (numeric) The number of confirmations, or -1 if the block is not on the main chain
  "size" : n,            (numeric) The block size
  "height" : n,          (numeric) The block height or index
  "version" : n,         (numeric) The block version
  "merkleroot" : "xxxx", (string) The merkle root
  "tx" : [               (array of string) The transaction ids
     "transactionid"     (string) The transaction id
     ,...
  ],
  "time" : ttt,          (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
  "mediantime" : ttt,    (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
  "nonce" : n,           (numeric) The nonce
  "bits" : "1d00ffff", (string) The bits
  "difficulty" : x.xxx,  (numeric) The difficulty
  "chainwork" : "xxxx",  (string) Expected number of hashes required to produce the chain up to this block (in hex)
  "hashmix      " : "hash",      (string) The hashmix of the block
  "previousblockhash" : "hash",  (string) The hash of the previous block
  "nextblockhash" : "hash"       (string) The hash of the next block
}
```

#### Result: (for verbose=false):
```
"data"             (string) A string that is serialized, hex-encoded data for block 'hash'.
```

#### Examples:
```
> energi-cli getblock "00000000000fd08c2fb661d2fcb0d49abb3a91e5f27082ce64feed3b4dede2e2"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblock", "params": ["00000000000fd08c2fb661d2fcb0d49abb3a91e5f27082ce64feed3b4dede2e2"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getblockchaininfo
Returns an object containing various state info regarding block chain processing.

#### Result:
```
{
  "chain": "xxxx",        (string) current network name as defined in BIP70 (main, test, regtest)
  "blocks": xxxxxx,         (numeric) the current number of blocks processed in the server
  "headers": xxxxxx,        (numeric) the current number of headers we have validated
  "bestblockhash": "...", (string) the hash of the currently best block
  "difficulty": xxxxxx,     (numeric) the current difficulty
  "mediantime": xxxxxx,     (numeric) median time for the current best block
  "verificationprogress": xxxx, (numeric) estimate of verification progress [0..1]
  "chainwork": "xxxx"     (string) total amount of work in active chain, in hexadecimal
  "pruned": xx,             (boolean) if the blocks are subject to pruning
  "pruneheight": xxxxxx,    (numeric) heighest block available
  "softforks": [            (array) status of softforks in progress
     {
        "id": "xxxx",        (string) name of softfork
        "version": xx,         (numeric) block version
        "enforce": {           (object) progress toward enforcing the softfork rules for new-version blocks
           "status": xx,       (boolean) true if threshold reached
           "found": xx,        (numeric) number of blocks with the new version found
           "required": xx,     (numeric) number of blocks required to trigger
           "window": xx,       (numeric) maximum size of examined window of recent blocks
        },
        "reject": { ... }      (object) progress toward rejecting pre-softfork blocks (same fields as "enforce")
     }, ...
  ],
  "bip9_softforks": [       (array) status of BIP9 softforks in progress
     {
        "id": "xxxx",        (string) name of the softfork
        "status": "xxxx",    (string) one of "defined", "started", "lockedin", "active", "failed"
     }
  ]
}
```

#### Examples:
```
> energi-cli getblockchaininfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockchaininfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```
## getblockcount

Returns the number of blocks in the longest block chain.

#### Result:
```
n    (numeric) The current block count
```

#### Examples:
```
> energi-cli getblockcount
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockcount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getblockhash index

Returns hash of block in best-block-chain at index provided.

#### Arguments:
```
1. index         (numeric, required) The block index
```

#### Result:
```
"hash"         (string) The block hash
```

#### Examples:
```
> energi-cli getblockhash 1000
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockhash", "params": [1000] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getblockhashes timestamp

Returns array of hashes of blocks within the timestamp range provided.

#### Arguments:
```
1. high         (numeric, required) The newer block timestamp
2. low          (numeric, required) The older block timestamp
```

#### Result:
```
[
  "hash"         (string) The block hash
]
```

#### Examples:
```
> energi-cli getblockhashes 1231614698 1231024505
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockhashes", "params": [1231614698, 1231024505] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getblockheader "hash" ( verbose )

If verbose is false, returns a string that is serialized, hex-encoded data for blockheader 'hash'.
If verbose is true, returns an Object with information about blockheader <hash>.

#### Arguments:
```
1. "hash"          (string, required) The block hash
2. verbose           (boolean, optional, default=true) true for a json object, false for the hex encoded data
```

#### Result: (for verbose = true):
```
{
  "hash" : "hash",     (string) the block hash (same as provided)
  "confirmations" : n,   (numeric) The number of confirmations, or -1 if the block is not on the main chain
  "height" : n,          (numeric) The block height or index
  "version" : n,         (numeric) The block version
  "merkleroot" : "xxxx", (string) The merkle root
  "time" : ttt,          (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
  "mediantime" : ttt,    (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
  "nonce" : n,           (numeric) The nonce
  "bits" : "1d00ffff", (string) The bits
  "difficulty" : x.xxx,  (numeric) The difficulty
  "hashmix      " : "hash",      (string) The hashmix of the block
  "previousblockhash" : "hash",  (string) The hash of the previous block
  "nextblockhash" : "hash",      (string) The hash of the next block
  "chainwork" : "0000...1f3"     (string) Expected number of hashes required to produce the current chain (in hex)
}
```

#### Result: (for verbose=false):
```
"data"             (string) A string that is serialized, hex-encoded data for block 'hash'.
```

#### Examples:
```
> energi-cli getblockheader "00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockheader", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getblockheaders "hash" ( count verbose )

Returns an array of items with information about <count> blockheaders starting from <hash>.

If verbose is false, each item is a string that is serialized, hex-encoded data for a single blockheader.
If verbose is true, each item is an Object with information about a single blockheader.

#### Arguments:
```
1. "hash"          (string, required) The block hash
2. count           (numeric, optional, default/max=2000)
3. verbose         (boolean, optional, default=true) true for a json object, false for the hex encoded data
```

#### Result: (for verbose = true):
```
[ {
  "hash" : "hash",               (string)  The block hash
  "confirmations" : n,           (numeric) The number of confirmations, or -1 if the block is not on the main chain
  "height" : n,                  (numeric) The block height or index
  "version" : n,                 (numeric) The block version
  "merkleroot" : "xxxx",         (string)  The merkle root
  "time" : ttt,                  (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
  "mediantime" : ttt,            (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
  "nonce" : n,                   (numeric) The nonce
  "bits" : "1d00ffff",           (string)  The bits
  "difficulty" : x.xxx,          (numeric) The difficulty
  "hashmix      " : "hash",      (string) The hashmix of the block
  "previousblockhash" : "hash",  (string)  The hash of the previous block
  "nextblockhash" : "hash",      (string)  The hash of the next block
  "chainwork" : "0000...1f3"     (string)  Expected number of hashes required to produce the current chain (in hex)
}, {
       ...
   },
...
]
```


#### Result: (for verbose=false):
```
[
  "data",                        (string)  A string that is serialized, hex-encoded data for block header.
  ...
]
```

#### Examples:
```
> energi-cli getblockheaders "00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09" 2000
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockheaders", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09" 2000] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getchaintips ( count branchlen )
Return information about all known tips in the block tree, including the main chain as well as orphaned branches.

#### Arguments:
```
1. count       (numeric, optional) only show this much of latest tips
2. branchlen   (numeric, optional) only show tips that have equal or greater length of branch
```

#### Result:
```
[
  {
    "height": xxxx,             (numeric) height of the chain tip
    "hash": "xxxx",             (string) block hash of the tip
    "difficulty" : x.xxx,       (numeric) The difficulty
    "chainwork" : "0000...1f3"  (string) Expected number of hashes required to produce the current chain (in hex)
    "branchlen": 0              (numeric) zero for main chain
    "status": "active"          (string) "active" for the main chain
  },
  {
    "height": xxxx,
    "hash": "xxxx",
    "difficulty" : x.xxx,
    "chainwork" : "0000...1f3"
    "branchlen": 1              (numeric) length of branch connecting the tip to the main chain
    "status": "xxxx"            (string) status of the chain (active, valid-fork, valid-headers, headers-only, invalid)
  }
]
Possible values for status:
1.  "invalid"               This branch contains at least one invalid block
2.  "headers-only"          Not all blocks for this branch are available, but the headers are valid
3.  "valid-headers"         All blocks are available for this branch, but they were never fully validated
4.  "valid-fork"            This branch is not part of the active chain, but is fully validated
5.  "active"                This is the tip of the active main chain, which is certainly valid
```

#### Examples:
```
> energi-cli getchaintips
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getchaintips", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getdifficulty

Returns the proof-of-work difficulty as a multiple of the minimum difficulty.

#### Result:
```
n.nnn       (numeric) the proof-of-work difficulty as a multiple of the minimum difficulty.
```

#### Examples:
```
> energi-cli getdifficulty
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getdifficulty", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getmempoolinfo

Returns details on the active state of the TX memory pool.

#### Result:
```
{
  "size": xxxxx,               (numeric) Current tx count
  "bytes": xxxxx,              (numeric) Sum of all tx sizes
  "usage": xxxxx,              (numeric) Total memory usage for the mempool
  "maxmempool": xxxxx,         (numeric) Maximum memory usage for the mempool
  "mempoolminfee": xxxxx       (numeric) Minimum fee for tx to be accepted
}
```

#### Examples:
```
> energi-cli getmempoolinfo
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getrawmempool ( verbose )

Returns all transaction ids in memory pool as a json array of string transaction ids.

#### Arguments:
```
1. verbose           (boolean, optional, default=false) true for a json object, false for array of transaction ids
```

#### Result: (for verbose = false):
```
[                     (json array of string)
  "transactionid"     (string) The transaction id
  ,...
]
```

#### Result: (for verbose = true):
```
{                           (json object)
  "transactionid" : {       (json object)
    "size" : n,             (numeric) transaction size in bytes
    "fee" : n,              (numeric) transaction fee in NRG
    "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority
    "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
    "height" : n,           (numeric) block height when transaction entered pool
    "startingpriority" : n, (numeric) priority when transaction entered pool
    "currentpriority" : n,  (numeric) transaction priority now
    "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
    "descendantsize" : n,   (numeric) size of in-mempool descendants (including this one)
    "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one)
    "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
        "transactionid",    (string) parent transaction id
       ... ]
  }, ...
}
```

#### Examples:
```
> energi-cli getrawmempool true
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawmempool", "params": [true] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getspentinfo

Returns the txid and index where an output is spent.

#### Arguments:
```
{
  "txid" (string) The hex string of the txid
  "index" (number) The start block height
}
```

#### Result:
```
{
  "txid"  (string) The transaction id
  "index"  (number) The spending input index
  ,...
}
```

#### Examples:
```
> energi-cli getspentinfo '{"txid": "0437cd7f8525ceed2324359c2d0ba26006d92d856a9c20fa0241106ee5a597c9", "index": 0}'
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getspentinfo", "params": [{"txid": "0437cd7f8525ceed2324359c2d0ba26006d92d856a9c20fa0241106ee5a597c9", "index": 0}] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## gettxout "txid" n ( includemempool )

Returns details about an unspent transaction output.

#### Arguments:
```
1. "txid"       (string, required) The transaction id
2. n              (numeric, required) vout value
3. includemempool  (boolean, optional) Whether to included the mem pool
```

#### Result:
```
{
  "bestblock" : "hash",    (string) the block hash
  "confirmations" : n,       (numeric) The number of confirmations
  "value" : x.xxx,           (numeric) The transaction value in NRG
  "scriptPubKey" : {         (json object)
     "asm" : "code",       (string)
     "hex" : "hex",        (string)
     "reqSigs" : n,          (numeric) Number of required signatures
     "type" : "pubkeyhash", (string) The type, eg pubkeyhash
     "addresses" : [          (array of string) array of energi addresses
        "energiaddress"     (string) energi address
        ,...
     ]
  },
  "version" : n,            (numeric) The version
  "coinbase" : true|false   (boolean) Coinbase or not
}
```

#### Examples:

Get unspent transactions
```
> energi-cli listunspent
```

View the details
```
> energi-cli gettxout "txid" 1
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxout", "params": ["txid", 1] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## gettxoutproof ["txid",...] ( blockhash )

Returns a hex-encoded proof that "txid" was included in a block.

NOTE: By default this function only works sometimes. This is when there is an
unspent output in the utxo for this transaction. To make it always work,
you need to maintain a transaction index, using the -txindex command line option or
specify the block in which the transaction is included in manually (by blockhash).

Return the raw transaction data.

#### Arguments:
```
1. "txids"       (string) A json array of txids to filter
    [
      "txid"     (string) A transaction hash
      ,...
    ]
2. "block hash"  (string, optional) If specified, looks for txid in the block with this hash
```

#### Result:
```
"data"           (string) A string that is a serialized, hex-encoded data for the proof.
```

#### Examples:
```
> energi-cli gettxoutproof '["mytxid",...]'
```
```
> energi-cli gettxoutproof '["mytxid",...]' "blockhash"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxoutproof", "params": [["mytxid",...], "blockhash"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## gettxoutsetinfo

Returns statistics about the unspent transaction output set.
Note this call may take some time.

#### Result:
```
{
  "height":n,     (numeric) The current block height (index)
  "bestblock": "hex",   (string) the best block hash hex
  "transactions": n,      (numeric) The number of transactions
  "txouts": n,            (numeric) The number of output transactions
  "bytes_serialized": n,  (numeric) The serialized size
  "hash_serialized": "hash",   (string) The serialized hash
  "total_amount": x.xxx          (numeric) The total amount
}
```

#### Examples:
```
> energi-cli gettxoutsetinfo
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxoutsetinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## verifychain ( checklevel numblocks )

Verifies blockchain database.

#### Arguments:
```
1. checklevel   (numeric, optional, 0-4, default=3) How thorough the block verification is.
2. numblocks    (numeric, optional, default=288, 0=all) The number of blocks to check.
```

#### Result:
```
true|false       (boolean) Verified or not
```

#### Examples:
```
> energi-cli verifychain
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "verifychain", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## verifytxoutproof "proof"

Verifies that a proof points to a transaction in a block, returning the transaction it commits to
and throwing an RPC error if the block is not in our best chain

#### Arguments:
```
1. "proof"    (string, required) The hex-encoded proof generated by gettxoutproof
```

#### Result:
```
["txid"]      (array, strings) The txid(s) which the proof commits to, or empty array if the proof is invalid
```

#### Examples:
```
> energi-cli verifytxoutproof "proof"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxoutproof", "params": ["proof"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## debug ( 0|1|addrman|alert|bench|coindb|db|reindex|estimatefee|lock|rand|rpc|selectcoins|mempool|mempoolrej|net|proxy|prune|http|libevent|tor|zmq|energi|nrghash|privatesend|instantsend|masternode|spork|keepass|mnpayments|mnsync|gobject )
Change debug category on the fly. Specify single category or use comma to specify many.

#### Examples:
```
> energi-cli debug energi
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "debug", "params": [energi,net] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getinfo
Returns an object containing various state info.

#### Result:
```
{
  "version": xxxxx,           (numeric) the server version
  "protocolversion": xxxxx,   (numeric) the protocol version
  "walletversion": xxxxx,     (numeric) the wallet version
  "balance": xxxxxxx,         (numeric) the total energi balance of the wallet
  "privatesend_balance": xxxxxx, (numeric) the anonymized energi balance of the wallet
  "blocks": xxxxxx,           (numeric) the current number of blocks processed in the server
  "timeoffset": xxxxx,        (numeric) the time offset
  "connections": xxxxx,       (numeric) the number of connections
  "proxy": "host:port",     (string, optional) the proxy used by the server
  "difficulty": xxxxxx,       (numeric) the current difficulty
  "testnet": true|false,      (boolean) if the server is using testnet or not
  "keypoololdest": xxxxxx,    (numeric) the timestamp (seconds since GMT epoch) of the oldest pre-generated key in the key pool
  "keypoolsize": xxxx,        (numeric) how many new keys are pre-generated
  "unlocked_until": ttt,      (numeric) the timestamp in seconds since epoch (midnight Jan 1 1970 GMT) that the wallet is unlocked for transfers, or 0 if the wallet is locked
  "paytxfee": x.xxxx,         (numeric) the transaction fee set in NRG/kB
  "relayfee": x.xxxx,         (numeric) minimum relay fee for non-free transactions in NRG/kB
  "errors": "..."           (string) any error messages
}
```

#### Examples:
```
> energi-cli getinfo
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## help ( "command" )

List all commands, or get help for a specified command.

#### Arguments:
```
1. "command"     (string, optional) The command to get help on
```

#### Result:
```
"text"     (string) The help text
```

## stop

Stop Energi Core server.
## getactivedag

Returns a JSON list specifying loaded DAG
## getcache
 "epoch"
Returns a JSON object specifying DAG cache information for the specified epoch n or the current epoch if n is not specified
Arguments
"epoch" the epoch number
## getdag
 "epoch"
Returns a JSON object specifying DAG information for the specified epoch n or the current epoch if n is not specified
Arguments
"epoch" the epoch number
## getdagcachesize
 "epoch"
Returns the size of the DAG chache in bytes for the specified epoch n or the current epoch if n is not specified
Arguments
"epoch" the epoch number
## getdagsize
 "epoch"
Returns the size of the DAG in bytes for the specified epoch n or the current epoch if n is not specified
Arguments
"epoch" the epoch number
## getepoch

Returns current epoch number
## getseedhash
 "epoch"
Returns the hex encoded seedhash for specified epoch n or current epoch if n is not specified
Arguments
"epoch" the epoch number
## getgovernanceinfo
Returns an object containing governance parameters.

#### Result:
```
{
  "governanceminquorum": xxxxx,           (numeric) the absolute minimum number of votes needed to trigger a governance action
  "masternodewatchdogmaxseconds": xxxxx,  (numeric) sentinel watchdog expiration time in seconds
  "proposalfee": xxx.xx,                  (numeric) the collateral transaction fee which must be paid to create a proposal in NRG
  "superblockcycle": xxxxx,               (numeric) the number of blocks between superblocks
  "lastsuperblock": xxxxx,                (numeric) the block number of the last superblock
  "nextsuperblock": xxxxx,                (numeric) the block number of the next superblock
}
```

#### Examples:
```
> energi-cli getgovernanceinfo
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getgovernanceinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getpoolinfo
Returns an object containing mixing pool related information.

## getsuperblockbudget index

Returns the absolute maximum sum of superblock payments allowed.

#### Arguments:
```
1. index         (numeric, required) The block index
```

#### Result:
```
n                (numeric) The absolute maximum sum of superblock payments allowed, in NRG
```

#### Examples:
```
> energi-cli getsuperblockbudget 1000
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getsuperblockbudget", "params": [1000] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## gobject "command"...
Manage governance objects

Available commands:
  check              - Validate governance object data (proposal only)
  prepare            - Prepare governance object by signing and creating tx
  submit             - Submit governance object to network
  deserialize        - Deserialize governance object from hex string to JSON
  count              - Count governance objects and votes
  get                - Get governance object by hash
  getvotes           - Get all votes for a governance object hash (including old votes)
  getcurrentvotes    - Get only current (tallying) votes for a governance object hash (does not include old votes)
  list               - List governance objects (can be filtered by signal and/or object type)
  diff               - List differences since last diff
  vote-alias         - Vote on a governance object by masternode alias (using masternode.conf setup)
  vote-conf          - Vote on a governance object by masternode configured in energi.conf
  vote-many          - Vote on a governance object by all masternodes (using masternode.conf setup)

## masternode "command"...
Set of commands to execute masternode related actions

#### Arguments:
```
1. "command"        (string or set of strings, required) The command to execute

Available commands:
  count        - Print number of all known masternodes (optional: 'ps', 'enabled', 'all', 'qualify')
  current      - Print info on current masternode winner to be paid the next block (calculated locally)
  debug        - Print masternode status
  genkey       - Generate new masternodeprivkey
  outputs      - Print masternode compatible outputs
  start        - Start local Hot masternode configured in energi.conf
  start-alias  - Start single remote masternode by assigned alias configured in masternode.conf
  start-<mode> - Start remote masternodes configured in masternode.conf (<mode>: 'all', 'missing', 'disabled')
  status       - Print masternode status information
  list         - Print list of all known masternodes (see masternodelist for more info)
  list-conf    - Print masternode.conf in JSON format
  winner       - Print info on next masternode winner to vote for
  winners      - Print list of masternode winners
```

## masternodebroadcast "command"...
Set of commands to create and relay masternode broadcast messages

#### Arguments:
```
1. "command"        (string or set of strings, required) The command to execute

Available commands:
  create-alias  - Create single remote masternode broadcast message by assigned alias configured in masternode.conf
  create-all    - Create remote masternode broadcast messages for all masternodes configured in masternode.conf
  decode        - Decode masternode broadcast message
  relay         - Relay masternode broadcast message to the network
```

## masternodelist ( "mode" "filter" )
Get a list of masternodes in different modes

#### Arguments:
```
1. "mode"      (string, optional/required to use filter, defaults = status) The mode to run list in
2. "filter"    (string, optional) Filter results. Partial match by outpoint by default in all modes,
                                    additional matches in some modes are also available

Available modes:
  activeseconds  - Print number of seconds masternode recognized by the network as enabled
                   (since latest issued "masternode start/start-many/start-alias")
  addr           - Print ip address associated with a masternode (can be additionally filtered, partial match)
  full           - Print info in format 'status protocol payee lastseen activeseconds lastpaidtime lastpaidblock IP'
                   (can be additionally filtered, partial match)
  info           - Print info in format 'status protocol payee lastseen activeseconds sentinelversion sentinelstate IP'
                   (can be additionally filtered, partial match)
  lastpaidblock  - Print the last block height a node was paid on the network
  lastpaidtime   - Print the last time a node was paid on the network
  lastseen       - Print timestamp of when a masternode was last seen on the network
  payee          - Print Energi address associated with a masternode (can be additionally filtered,
                   partial match)
  protocol       - Print protocol of a masternode (can be additionally filtered, exact match))
  pubkey         - Print the masternode (not collateral) public key
  rank           - Print rank of a masternode based on current block
  status         - Print masternode status: PRE_ENABLED / ENABLED / EXPIRED / WATCHDOG_EXPIRED / NEW_START_REQUIRED /
                   UPDATE_REQUIRED / POSE_BAN / OUTPOINT_SPENT (can be additionally filtered, partial match)
```

## mnsync [status|next|reset]
Returns the sync status, updates to the next step or resets it entirely.

## privatesend "command"

#### Arguments:
```
1. "command"        (string or set of strings, required) The command to execute

Available commands:
  start       - Start mixing
  stop        - Stop mixing
  reset       - Reset mixing
```
## sentinelping version

Sentinel ping.

#### Arguments:
```1. version           (string, required) Sentinel version in the form "x.x.x"
```

#### Result:
```
state                (boolean) Ping result
```

#### Examples:
```
> energi-cli sentinelping 1.0.2
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sentinelping", "params": [1.0.2] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## spork <name> [<value>]
<name> is the corresponding spork name, or 'show' to show all current spork settings, active to show which sporks are active<value> is a epoch datetime to enable or disable spork
## voteraw <masternode-tx-hash> <masternode-tx-index> <governance-hash> <vote-signal> [yes|no|abstain] <time> <vote-sig>
Compile and relay a governance vote with provided external signature instead of signing vote internally

## generate numblocks

Mine blocks immediately (before the RPC call returns)

Note: this function can only be used on the regtest network

#### Arguments:
```
1. numblocks    (numeric, required) How many blocks are generated immediately.
```

#### Result:
```
[ blockhashes ]     (array) hashes of blocks generated
```

#### Examples:

Generate 11 blocks
```
> energi-cli generate 11
```

## getgenerate

Return if the server is set to generate coins or not. The default is false.
It is set with the command line argument -gen (or energi.conf setting gen)
It can also be set with the setgenerate call.

#### Result:
```
true|false      (boolean) If the server is set to generate coins or not
```

#### Examples:
```
> energi-cli getgenerate
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getgenerate", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## setgenerate generate ( genproclimit )

Set 'generate' true or false to turn generation on or off.
Generation is limited to 'genproclimit' processors, -1 is unlimited.
See the getgenerate call for the current setting.

#### Arguments:
```
1. generate         (boolean, required) Set to true to turn on generation, false to turn off.
2. genproclimit     (numeric, optional) Set the processor limit for when generation is on. Can be -1 for unlimited.
```

#### Examples:

Set the generation on with a limit of one processor
```
> energi-cli setgenerate true 1
```

Check the setting
```
> energi-cli getgenerate
```

Turn off generation
```
> energi-cli setgenerate false
```

Using json rpc
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setgenerate", "params": [true, 1] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getblocktemplate ( "jsonrequestobject" )

If the request parameters include a 'mode' key, that is used to explicitly select between the default 'template' request or a 'proposal'.
It returns data needed to construct a block to work on.
For full specification, see BIPs 22 and 9:
    https://github.com/bitcoin/bips/blob/master/bip-0022.mediawiki
    https://github.com/bitcoin/bips/blob/master/bip-0009.mediawiki#getblocktemplate_changes

#### Arguments:
```
1. "jsonrequestobject"       (string, optional) A json object in the following spec
     {
       "mode":"template"    (string, optional) This must be set to "template" or omitted
       "capabilities":[       (array, optional) A list of strings
           "support"           (string) client side supported feature, 'longpoll', 'coinbasetxn', 'coinbasevalue', 'proposal', 'serverlist', 'workid'
           ,...
         ]
     }
```

#### Result:
```
{
  "version" : n,                    (numeric) The block version
  "rules" : [ "rulename", ... ],    (array of strings) specific block rules that are to be enforced
  "vbavailable" : {                 (json object) set of pending, supported versionbit (BIP 9) softfork deployments
      "rulename" : bitnumber        (numeric) identifies the bit number as indicating acceptance and readiness for the named softfork rule
      ,...
  },
  "vbrequired" : n,                 (numeric) bit mask of versionbits the server requires set in submissions
  "previousblockhash" : "xxxx",    (string) The hash of current highest block
  "transactions" : [                (array) contents of non-coinbase transactions that should be included in the next block
      {
         "data" : "xxxx",          (string) transaction data encoded in hexadecimal (byte-for-byte)
         "hash" : "xxxx",          (string) hash/id encoded in little-endian hexadecimal
         "depends" : [              (array) array of numbers
             n                        (numeric) transactions before this one (by 1-based index in 'transactions' list) that must be present in the final block if this one is
             ,...
         ],
         "fee": n,                   (numeric) difference in value between transaction inputs and outputs (in atoms); for coinbase transactions, this is a negative Number of the total collected block fees (ie, not including the block subsidy); if key is not present, fee is unknown and clients MUST NOT assume there isn't one
         "sigops" : n,               (numeric) total number of SigOps, as counted for purposes of block limits; if key is not present, sigop count is unknown and clients MUST NOT assume there aren't any
         "required" : true|false     (boolean) if provided and true, this transaction must be in the final block
      }
      ,...
  ],
  "coinbaseaux" : {                  (json object) data that should be included in the coinbase's scriptSig content
      "flags" : "flags"            (string)
  },
  "coinbasevalue" : n,               (numeric) maximum allowable input to coinbase transaction, including the generation award and transaction fees (in atoms)
  "coinbasetxn" : { ... },           (json object) information for coinbase transaction
  "target" : "xxxx",               (string) The hash target
  "mintime" : xxx,                   (numeric) The minimum timestamp appropriate for next block time in seconds since epoch (Jan 1 1970 GMT)
  "mutable" : [                      (array of string) list of ways the block template may be changed
     "value"                         (string) A way the block template may be changed, e.g. 'time', 'transactions', 'prevblock'
     ,...
  ],
  "noncerange" : "00000000ffffffff",   (string) A range of valid nonces
  "sigoplimit" : n,                 (numeric) limit of sigops in blocks
  "sizelimit" : n,                  (numeric) limit of block size
  "curtime" : ttt,                  (numeric) current timestamp in seconds since epoch (Jan 1 1970 GMT)
  "bits" : "xxx",                 (string) compressed target of next block
  "height" : n                      (numeric) The height of the next block
  "backbone" : {                  (json object) required Energi Backbone payee that must be included in the next block
      "payee" : "xxxx",             (string) payee address
      "script" : "xxxx",            (string) payee scriptPubKey
      "amount": n                   (numeric) required amount to pay
  },
  "masternode" : {                  (json object) required masternode payee that must be included in the next block
      "payee" : "xxxx",             (string) payee address
      "script" : "xxxx",            (string) payee scriptPubKey
      "amount": n                   (numeric) required amount to pay
  },
  "masternode_payments_started" :  true|false, (boolean) true, if masternode payments started
  "masternode_payments_enforced" : true|false, (boolean) true, if masternode payments are enforced
  "superblock" : [                  (array) required superblock payees that must be included in the next block
      {
         "payee" : "xxxx",          (string) payee address
         "script" : "xxxx",         (string) payee scriptPubKey
         "amount": n                (numeric) required amount to pay
      }
      ,...
  ],
  "superblocks_started" : true|false, (boolean) true, if superblock payments started
  "superblocks_enabled" : true|false  (boolean) true, if superblock payments are enabled
}
```
#### Examples:
```
> energi-cli getblocktemplate
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblocktemplate", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getmininginfo

Returns a json object containing mining-related information.

#### Result:
```
{
  "blocks": nnn,             (numeric) The current block
  "currentblocksize": nnn,   (numeric) The last block size
  "currentblocktx": nnn,     (numeric) The last block transaction
  "difficulty": xxx.xxxxx    (numeric) The current difficulty
  "errors": "..."          (string) Current errors
  "generate": true|false     (boolean) If the generation is on or off (see getgenerate or setgenerate calls)
  "genproclimit": n          (numeric) The processor limit for generation. -1 if no generation. (see getgenerate or setgenerate calls)
  "pooledtx": n              (numeric) The size of the mem pool
  "testnet": true|false      (boolean) If using testnet or not
  "chain": "xxxx",         (string) current network name as defined in BIP70 (main, test, regtest)
}
```

#### Examples:
```
> energi-cli getmininginfo
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmininginfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getnetworkhashps ( blocks height )

Returns the estimated network hashes per second based on the last n blocks.
Pass in [blocks] to override ## of blocks, -1 specifies since last difficulty change.
Pass in [height] to estimate the network speed at the time when a certain block was found.

#### Arguments:
```
1. blocks     (numeric, optional, default=120) The number of blocks, or -1 for blocks since last difficulty change.
2. height     (numeric, optional, default=-1) To estimate at the time of the given height.
```

#### Result:
```
x             (numeric) Hashes per second estimated
```

#### Examples:
```
> energi-cli getnetworkhashps
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnetworkhashps", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## prioritisetransaction <txid> <priority delta> <fee delta>
Accepts the transaction into mined blocks at a higher (or lower) priority

#### Arguments:
```
1. "txid"       (string, required) The transaction id.
2. priority delta (numeric, required) The priority to add or subtract.
                  The transaction selection algorithm considers the tx as it would have a higher priority.
                  (priority of a transaction is calculated: coinage * value_in_atoms / txsize)
3. fee delta      (numeric, required) The fee value (in atoms) to add (or subtract, if negative).
                  The fee is not actually paid, only the algorithm for selecting transactions into a block
                  considers the transaction as it would have paid a higher (or lower) fee.

Result
true              (boolean) Returns true
```

#### Examples:
```
> energi-cli prioritisetransaction "txid" 0.0 10000
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "prioritisetransaction", "params": ["txid", 0.0, 10000] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## submitblock "hexdata" ( "jsonparametersobject" )

Attempts to submit new block to network.
The 'jsonparametersobject' parameter is currently ignored.
See https://en.bitcoin.it/wiki/BIP_0022 for full specification.

#### Arguments
```
1. "hexdata"    (string, required) the hex-encoded block data to submit
2. "jsonparametersobject"     (string, optional) object of optional parameters
    {
      "workid" : "id"    (string, optional) if the server provided a workid, it MUST be included with submissions
    }
```

#### Result:
```
```

#### Examples:
```
> energi-cli submitblock "mydata"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "submitblock", "params": ["mydata"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## addnode "node" "add|remove|onetry"

Attempts add or remove a node from the addnode list.
Or try a connection to a node once.

#### Arguments:
```
1. "node"     (string, required) The node (see getpeerinfo for nodes)
2. "command"  (string, required) 'add' to add a node to the list, 'remove' to remove a node from the list, 'onetry' to try a connection to the node once
```

#### Examples:
```
> energi-cli addnode "192.168.0.6:9797" "onetry"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "addnode", "params": ["192.168.0.6:9797", "onetry"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## clearbanned

Clear all banned IPs.

#### Examples:
```
> energi-cli clearbanned
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "clearbanned", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## disconnectnode "node"

Immediately disconnects from the specified node.

#### Arguments:
```
1. "node"     (string, required) The node (see getpeerinfo for nodes)
```

#### Examples:
```
> energi-cli disconnectnode "192.168.0.6:8333"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "disconnectnode", "params": ["192.168.0.6:8333"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getaddednodeinfo dummy ( "node" )

Returns information about the given added node, or all added nodes
(note that onetry addnodes are not listed here)

#### Arguments:
```
1. dummy      (boolean, required) Kept for historical purposes but ignored
2. "node"   (string, optional) If provided, return information about this specific node, otherwise all nodes are returned.
```

#### Result:
```
[
  {
    "addednode" : "192.168.0.201",   (string) The node ip address or name (as provided to addnode)
    "connected" : true|false,          (boolean) If connected
    "addresses" : [                    (list of objects) Only when connected = true
       {
         "address" : "192.168.0.201:9797",  (string) The Energi server IP and port we're connected to
         "connected" : "outbound"           (string) connection, inbound or outbound
       }
     ]
  }
  ,...
]
```

#### Examples:
```
> energi-cli getaddednodeinfo true
```
```
> energi-cli getaddednodeinfo true "192.168.0.201"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddednodeinfo", "params": [true, "192.168.0.201"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getconnectioncount

Returns the number of connections to other nodes.

#### Result:
```
n          (numeric) The connection count
```

#### Examples:
```
> energi-cli getconnectioncount
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getconnectioncount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getnettotals

Returns information about network traffic, including bytes in, bytes out,
and current time.

#### Result:
```
{
  "totalbytesrecv": n,   (numeric) Total bytes received
  "totalbytessent": n,   (numeric) Total bytes sent
  "timemillis": t,       (numeric) Total cpu time
  "uploadtarget":
  {
    "timeframe": n,                         (numeric) Length of the measuring timeframe in seconds
    "target": n,                            (numeric) Target in bytes
    "target_reached": true|false,           (boolean) True if target is reached
    "serve_historical_blocks": true|false,  (boolean) True if serving historical blocks
    "bytes_left_in_cycle": t,               (numeric) Bytes left in current time cycle
    "time_left_in_cycle": t                 (numeric) Seconds left in current time cycle
  }
}
```

#### Examples:
```
> energi-cli getnettotals
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnettotals", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getnetworkinfo
Returns an object containing various state info regarding P2P networking.

#### Result:
```
{
  "version": xxxxx,                      (numeric) the server version
  "subversion": "/Energi Core:x.x.x/",     (string) the server subversion string
  "protocolversion": xxxxx,              (numeric) the protocol version
  "localservices": "xxxxxxxxxxxxxxxx", (string) the services we offer to the network
  "localrelay": true|false,              (bool) true if transaction relay is requested from peers
  "timeoffset": xxxxx,                   (numeric) the time offset
  "connections": xxxxx,                  (numeric) the number of connections
  "networkactive": true|false,           (bool) whether p2p networking is enabled
  "networks": [                          (array) information per network
  {
    "name": "xxx",                     (string) network (ipv4, ipv6 or onion)
    "limited": true|false,               (boolean) is the network limited using -onlynet?
    "reachable": true|false,             (boolean) is the network reachable?
    "proxy": "host:port"               (string) the proxy that is used for this network, or empty if none
  }
  ,...
  ],
  "relayfee": x.xxxxxxxx,                (numeric) minimum relay fee for non-free transactions in NRG/kB
  "localaddresses": [                    (array) list of local addresses
  {
    "address": "xxxx",                 (string) network address
    "port": xxx,                         (numeric) network port
    "score": xxx                         (numeric) relative score
  }
  ,...
  ]
  "warnings": "..."                    (string) any network warnings (such as alert messages)
}
```

#### Examples:
```
> energi-cli getnetworkinfo
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnetworkinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getpeerinfo

Returns data about each connected network node as a json array of objects.

#### Result:
```
[
  {
    "id": n,                   (numeric) Peer index
    "addr":"host:port",      (string) The ip address and port of the peer
    "addrlocal":"ip:port",   (string) local address
    "services":"xxxxxxxxxxxxxxxx",   (string) The services offered
    "relaytxes":true|false,    (boolean) Whether peer has asked us to relay transactions to it
    "lastsend": ttt,           (numeric) The time in seconds since epoch (Jan 1 1970 GMT) of the last send
    "lastrecv": ttt,           (numeric) The time in seconds since epoch (Jan 1 1970 GMT) of the last receive
    "bytessent": n,            (numeric) The total bytes sent
    "bytesrecv": n,            (numeric) The total bytes received
    "conntime": ttt,           (numeric) The connection time in seconds since epoch (Jan 1 1970 GMT)
    "timeoffset": ttt,         (numeric) The time offset in seconds
    "pingtime": n,             (numeric) ping time (if available)
    "minping": n,              (numeric) minimum observed ping time (if any at all)
    "pingwait": n,             (numeric) ping wait (if non-zero)
    "version": v,              (numeric) The peer version, such as 7001
    "subver": "/Energi Core:x.x.x/",  (string) The string version
    "inbound": true|false,     (boolean) Inbound (true) or Outbound (false)
    "startingheight": n,       (numeric) The starting height (block) of the peer
    "banscore": n,             (numeric) The ban score
    "synced_headers": n,       (numeric) The last header we have in common with this peer
    "synced_blocks": n,        (numeric) The last block we have in common with this peer
    "inflight": [
       n,                        (numeric) The heights of blocks we're currently asking from this peer
       ...
    ]
    "bytessent_per_msg": {
       "addr": n,             (numeric) The total bytes sent aggregated by message type
       ...
    }
    "bytesrecv_per_msg": {
       "addr": n,             (numeric) The total bytes received aggregated by message type
       ...
    }
  }
  ,...
]
```

#### Examples:
```
> energi-cli getpeerinfo
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getpeerinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## listbanned

List all banned IPs/Subnets.

#### Examples:
```
> energi-cli listbanned
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listbanned", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## ping

Requests that a ping be sent to all other nodes, to measure ping time.
Results provided in getpeerinfo, pingtime and pingwait fields are decimal seconds.
Ping command is handled in queue with all other commands, so it measures processing backlog, not just network ping.

#### Examples:
```
> energi-cli ping
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "ping", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## setban "ip(/netmask)" "add|remove" (bantime) (absolute)

Attempts add or remove a IP/Subnet from the banned list.

#### Arguments:
```
1. "ip(/netmask)" (string, required) The IP/Subnet (see getpeerinfo for nodes ip) with a optional netmask (default is /32 = single ip)
2. "command"      (string, required) 'add' to add a IP/Subnet to the list, 'remove' to remove a IP/Subnet from the list
3. "bantime"      (numeric, optional) time in seconds how long (or until when if [absolute] is set) the ip is banned (0 or empty means using the default time of 24h which can also be overwritten by the -bantime startup argument)
4. "absolute"     (boolean, optional) If set, the bantime must be a absolute timestamp in seconds since epoch (Jan 1 1970 GMT)
```

#### Examples:
```
> energi-cli setban "192.168.0.6" "add" 86400
```
```
> energi-cli setban "192.168.0.0/24" "add"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setban", "params": ["192.168.0.6", "add" 86400] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## setnetworkactive true|false
Disable/enable all p2p network activity.

## createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,"data":"hex",...} ( locktime )

Create a transaction spending the given inputs and creating new outputs.
Outputs can be addresses or data.
Returns hex-encoded raw transaction.
Note that the transaction's inputs are not signed, and
it is not stored in the wallet or transmitted to the network.

#### Arguments:
```
1. "transactions"        (string, required) A json array of json objects
     [
       {
         "txid":"id",    (string, required) The transaction id
         "vout":n        (numeric, required) The output number
       }
       ,...
     ]
2. "outputs"             (string, required) a json object with outputs
    {
      "address": x.xxx   (numeric or string, required) The key is the energi address, the numeric value (can be string) is the NRG amount
      "data": "hex",     (string, required) The key is "data", the value is hex encoded data
      ...
    }
3. locktime                (numeric, optional, default=0) Raw locktime. Non-0 value also locktime-activates inputs
```

#### Result:
```
"transaction"            (string) hex string of the transaction

Examples
> energi-cli createrawtransaction "[{\"txid\":\"myid\",\"vout\":0}]" "{\"address\":0.01}"
> energi-cli createrawtransaction "[{\"txid\":\"myid\",\"vout\":0}]" "{\"data\":\"00010203\"}"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": ["[{\"txid\":\"myid\",\"vout\":0}]", "{\"address\":0.01}"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": ["[{\"txid\":\"myid\",\"vout\":0}]", "{\"data\":\"00010203\"}"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## decoderawtransaction "hexstring"

Return a JSON object representing the serialized, hex-encoded transaction.

#### Arguments:
```
1. "hex"      (string, required) The transaction hex string
```

#### Result:
```
{
  "txid" : "id",        (string) The transaction id
  "size" : n,             (numeric) The transaction size
  "version" : n,          (numeric) The version
  "locktime" : ttt,       (numeric) The lock time
  "vin" : [               (array of json objects)
     {
       "txid": "id",    (string) The transaction id
       "vout": n,         (numeric) The output number
       "scriptSig": {     (json object) The script
         "asm": "asm",  (string) asm
         "hex": "hex"   (string) hex
       },
       "sequence": n     (numeric) The script sequence number
     }
     ,...
  ],
  "vout" : [             (array of json objects)
     {
       "value" : x.xxx,            (numeric) The value in NRG
       "n" : n,                    (numeric) index
       "scriptPubKey" : {          (json object)
         "asm" : "asm",          (string) the asm
         "hex" : "hex",          (string) the hex
         "reqSigs" : n,            (numeric) The required sigs
         "type" : "pubkeyhash",  (string) The type, eg 'pubkeyhash'
         "addresses" : [           (json array of string)
           "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"   (string) Energi address
           ,...
         ]
       }
     }
     ,...
  ],
}
```

#### Examples:
```
> energi-cli decoderawtransaction "hexstring"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "decoderawtransaction", "params": ["hexstring"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## decodescript "hex"

Decode a hex-encoded script.

#### Arguments:
```
1. "hex"     (string) the hex encoded script
```

#### Result:
```
{
  "asm":"asm",   (string) Script public key
  "hex":"hex",   (string) hex encoded public key
  "type":"type", (string) The output type
  "reqSigs": n,    (numeric) The required signatures
  "addresses": [   (json array of string)
     "address"     (string) energi address
     ,...
  ],
  "p2sh","address" (string) address of P2SH script wrapping this redeem script (not returned if the script is already a P2SH).
}
```

#### Examples:
```
> energi-cli decodescript "hexstring"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "decodescript", "params": ["hexstring"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## fundrawtransaction "hexstring" includeWatching

Add inputs to a transaction until it has enough in value to meet its out value.
This will not modify existing inputs, and will add one change output to the outputs.
Note that inputs which were signed may need to be resigned after completion since in/outputs have been added.
The inputs added will not be signed, use signrawtransaction for that.
Note that all existing inputs must have their previous output transaction be in the wallet.
Note that all inputs selected must be of standard form and P2SH scripts must bein the wallet using importaddress or addmultisigaddress (to calculate fees).
You can see whether this is the case by checking the "solvable" field in the listunspent output.
Only pay-to-pubkey, multisig, and P2SH versions thereof are currently supported for watch-only

#### Arguments:
```
1. "hexstring"     (string, required) The hex string of the raw transaction
2. includeWatching (boolean, optional, default false) Also select inputs which are watch only
```

#### Result:
```
{
  "hex":       "value", (string)  The resulting raw transaction (hex-encoded string)
  "fee":       n,         (numeric) Fee the resulting transaction pays
  "changepos": n          (numeric) The position of the added change output, or -1
}
"hex"
```

#### Examples:

Create a transaction with no inputs
```
> energi-cli createrawtransaction "[]" "{\"myaddress\":0.01}"
```

Add sufficient unsigned inputs to meet the output value
```
> energi-cli fundrawtransaction "rawtransactionhex"
```

Sign the transaction
```
> energi-cli signrawtransaction "fundedtransactionhex"
```

Send the transaction
```
> energi-cli sendrawtransaction "signedtransactionhex"
```

## getrawtransaction "txid" ( verbose )

NOTE: By default this function only works sometimes. This is when the tx is in the mempool
or there is an unspent output in the utxo for this transaction. To make it always work,
you need to maintain a transaction index, using the -txindex command line option.

Return the raw transaction data.

If verbose=0, returns a string that is serialized, hex-encoded data for 'txid'.
If verbose is non-zero, returns an Object with information about 'txid'.

#### Arguments:
```
1. "txid"      (string, required) The transaction id
2. verbose       (numeric, optional, default=0) If 0, return a string, other return a json object

Result (if verbose is not set or set to 0):
"data"      (string) The serialized, hex-encoded data for 'txid'

Result (if verbose > 0):
{
  "hex" : "data",       (string) The serialized, hex-encoded data for 'txid'
  "txid" : "id",        (string) The transaction id (same as provided)
  "size" : n,             (numeric) The transaction size
  "version" : n,          (numeric) The version
  "locktime" : ttt,       (numeric) The lock time
  "vin" : [               (array of json objects)
     {
       "txid": "id",    (string) The transaction id
       "vout": n,         (numeric)
       "scriptSig": {     (json object) The script
         "asm": "asm",  (string) asm
         "hex": "hex"   (string) hex
       },
       "sequence": n      (numeric) The script sequence number
     }
     ,...
  ],
  "vout" : [              (array of json objects)
     {
       "value" : x.xxx,            (numeric) The value in NRG
       "n" : n,                    (numeric) index
       "scriptPubKey" : {          (json object)
         "asm" : "asm",          (string) the asm
         "hex" : "hex",          (string) the hex
         "reqSigs" : n,            (numeric) The required sigs
         "type" : "pubkeyhash",  (string) The type, eg 'pubkeyhash'
         "addresses" : [           (json array of string)
           "energiaddress"        (string) energi address
           ,...
         ]
       }
     }
     ,...
  ],
  "blockhash" : "hash",   (string) the block hash
  "confirmations" : n,      (numeric) The confirmations
  "time" : ttt,             (numeric) The transaction time in seconds since epoch (Jan 1 1970 GMT)
  "blocktime" : ttt         (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
}
```

#### Examples:
```
> energi-cli getrawtransaction "mytxid"
```
```
> energi-cli getrawtransaction "mytxid" 1
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawtransaction", "params": ["mytxid", 1] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## sendrawtransaction "hexstring" ( allowhighfees instantsend )

Submits raw transaction (serialized, hex-encoded) to local node and network.

Also see createrawtransaction and signrawtransaction calls.

#### Arguments:
```
1. "hexstring"    (string, required) The hex string of the raw transaction)
2. allowhighfees  (boolean, optional, default=false) Allow high fees
3. instantsend    (boolean, optional, default=false) Use InstantSend to send this transaction
```

#### Result:
```
"hex"             (string) The transaction hash in hex
```

#### Examples:

Create a transaction
```
> energi-cli createrawtransaction "[{\"txid\" : \"mytxid\",\"vout\":0}]" "{\"myaddress\":0.01}"
```

Sign the transaction, and get back the hex
```
> energi-cli signrawtransaction "myhex"
```

Send the transaction (signed hex)
```
> energi-cli sendrawtransaction "signedhex"
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendrawtransaction", "params": ["signedhex"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## signrawtransaction "hexstring" ( [{"txid":"id","vout":n,"scriptPubKey":"hex","redeemScript":"hex"},...] ["privatekey1",...] sighashtype )

Sign inputs for raw transaction (serialized, hex-encoded).
The second optional argument (may be null) is an array of previous transaction outputs that
this transaction depends on but may not yet be in the block chain.
The third optional argument (may be null) is an array of base58-encoded private
keys that, if given, will be the only keys used to sign the transaction.


#### Arguments:
```
1. "hexstring"     (string, required) The transaction hex string
2. "prevtxs"       (string, optional) An json array of previous dependent transaction outputs
     [               (json array of json objects, or 'null' if none provided)
       {
         "txid":"id",             (string, required) The transaction id
         "vout":n,                  (numeric, required) The output number
         "scriptPubKey": "hex",   (string, required) script key
         "redeemScript": "hex"    (string, required for P2SH) redeem script
       }
       ,...
    ]
3. "privatekeys"     (string, optional) A json array of base58-encoded private keys for signing
    [                  (json array of strings, or 'null' if none provided)
      "privatekey"   (string) private key in base58-encoding
      ,...
    ]
4. "sighashtype"     (string, optional, default=ALL) The signature hash type. Must be one of
       "ALL"
       "NONE"
       "SINGLE"
       "ALL|ANYONECANPAY"
       "NONE|ANYONECANPAY"
       "SINGLE|ANYONECANPAY"
```

#### Result:
```
{
  "hex" : "value",           (string) The hex-encoded raw transaction with signature(s)
  "complete" : true|false,   (boolean) If the transaction has a complete set of signatures
  "errors" : [                 (json array of objects) Script verification errors (if there are any)
    {
      "txid" : "hash",           (string) The hash of the referenced, previous transaction
      "vout" : n,                (numeric) The index of the output to spent and used as input
      "scriptSig" : "hex",       (string) The hex-encoded signature script
      "sequence" : n,            (numeric) Script sequence number
      "error" : "text"           (string) Verification or signing error related to the input
    }
    ,...
  ]
}
```

#### Examples:
```
> energi-cli signrawtransaction "myhex"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signrawtransaction", "params": ["myhex"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## createmultisig nrequired ["key",...]

Creates a multi-signature address with n signature of m keys required.
It returns a json object with the address and redeemScript.

#### Arguments:
```
1. nrequired      (numeric, required) The number of required signatures out of the n keys or addresses.
2. "keys"       (string, required) A json array of keys which are energi addresses or hex-encoded public keys
     [
       "key"    (string) energi address or hex-encoded public key
       ,...
     ]
```

#### Result:
```
{
  "address":"multisigaddress",  (string) The value of the new multisig address.
  "redeemScript":"script"       (string) The string value of the hex-encoded redemption script.
}
```

#### Examples:

Create a multisig address from 2 addresses
```
> energi-cli createmultisig 2 "[\"Xt4qk9uKvQYAonVGSZNXqxeDmtjaEWgfrs\",\"XoSoWQkpgLpppPoyyzbUFh1fq2RBvW6UK1\"]"
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createmultisig", "params": [2, "[\"Xt4qk9uKvQYAonVGSZNXqxeDmtjaEWgfrs\",\"XoSoWQkpgLpppPoyyzbUFh1fq2RBvW6UK1\"]"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## estimatefee nblocks

Estimates the approximate fee per kilobyte needed for a transaction to begin
confirmation within nblocks blocks.

#### Arguments:
```
1. nblocks     (numeric)
```

#### Result:
```
n              (numeric) estimated fee-per-kilobyte

A negative value is returned if not enough transactions and blocks
have been observed to make an estimate.
```

#### Example:
```
> energi-cli estimatefee 6
```

## estimatepriority nblocks

Estimates the approximate priority a zero-fee transaction needs to begin
confirmation within nblocks blocks.

#### Arguments:
```
1. nblocks     (numeric)
```

#### Result:
```
n              (numeric) estimated priority

A negative value is returned if not enough transactions and blocks
have been observed to make an estimate.
```

#### Example:
```
> energi-cli estimatepriority 6
```

## estimatesmartfee nblocks

WARNING: This interface is unstable and may disappear or change!

Estimates the approximate fee per kilobyte needed for a transaction to begin
confirmation within nblocks blocks if possible and return the number of blocks
for which the estimate is valid.

#### Arguments:
```
1. nblocks     (numeric)
```

#### Result:
```
{
  "feerate" : x.x,     (numeric) estimate fee-per-kilobyte (in BTC)
  "blocks" : n         (numeric) block number where estimate was found
}
```

A negative value is returned if not enough transactions and blocks
have been observed to make an estimate for any number of blocks.
However it will not return a value below the mempool reject fee.

#### Example:
```
> energi-cli estimatesmartfee 6
```

## estimatesmartpriority nblocks

WARNING: This interface is unstable and may disappear or change!

Estimates the approximate priority a zero-fee transaction needs to begin
confirmation within nblocks blocks if possible and return the number of blocks
for which the estimate is valid.

#### Arguments:
```
1. nblocks     (numeric)
```

#### Result:
```
{
  "priority" : x.x,    (numeric) estimated priority
  "blocks" : n         (numeric) block number where estimate was found
}
```

A negative value is returned if not enough transactions and blocks
have been observed to make an estimate for any number of blocks.
However if the mempool reject fee is set it will return 1e9 * MAX_MONEY.

#### Example:
```
> energi-cli estimatesmartpriority 6
```

## validateaddress "energiaddress"

Return information about the given energi address.

#### Arguments:
```
1. "energiaddress"     (string, required) The energi address to validate
```

#### Result:
```
{
  "isvalid" : true|false,       (boolean) If the address is valid or not. If not, this is the only property returned.
  "address" : "energiaddress", (string) The energi address validated
  "scriptPubKey" : "hex",       (string) The hex encoded scriptPubKey generated by the address
  "ismine" : true|false,        (boolean) If the address is yours or not
  "iswatchonly" : true|false,   (boolean) If the address is watchonly
  "isscript" : true|false,      (boolean) If the key is a script
  "pubkey" : "publickeyhex",    (string) The hex value of the raw public key
  "iscompressed" : true|false,  (boolean) If the address is compressed
  "account" : "account"         (string) DEPRECATED. The account associated with the address, "" is the default account
  "hdkeypath" : "keypath"       (string, optional) The HD keypath if the key is HD and available
  "hdchainid" : "<hash>"        (string, optional) The ID of the HD chain
}
```

#### Examples:
```
> energi-cli validateaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "validateaddress", "params": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## verifymessage "energiaddress" "signature" "message"

Verify a signed message

#### Arguments:
```
1. "energiaddress"  (string, required) The energi address to use for the signature.
2. "signature"       (string, required) The signature provided by the signer in base 64 encoding (see signmessage).
3. "message"         (string, required) The message that was signed.
```

#### Result:
```
true|false   (boolean) If the signature is verified or not.
```

#### Examples:

Unlock the wallet for 30 seconds
```
> energi-cli walletpassphrase "mypassphrase" 30
```

Create the signature
```
> energi-cli signmessage "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" "my message"
```

Verify the signature
```
> energi-cli verifymessage "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" "signature" "my message"
```

As json rpc
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "verifymessage", "params": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg", "signature", "my message"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## abandontransaction "txid"

Mark in-wallet transaction <txid> as abandoned
This will mark this transaction and all its in-wallet descendants as abandoned which will allow
for their inputs to be respent.  It can be used to replace "stuck" or evicted transactions.
It only works on transactions which are not included in a block and are not currently in the mempool.
It has no effect on transactions which are already conflicted or abandoned.

#### Arguments:
```
1. "txid"    (string, required) The transaction id
```

#### Result:
```
```

#### Examples:
```
> energi-cli abandontransaction "1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "abandontransaction", "params": ["1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## addmultisigaddress nrequired ["key",...] ( "account" )

Add a nrequired-to-sign multisignature address to the wallet.
Each key is an Energi address or hex-encoded public key.
If 'account' is specified (DEPRECATED), assign address to that account.

#### Arguments:
```
1. nrequired        (numeric, required) The number of required signatures out of the n keys or addresses.
2. "keysobject"   (string, required) A json array of energi addresses or hex-encoded public keys
     [
       "address"  (string) energi address or hex-encoded public key
       ...,
     ]
3. "account"      (string, optional) DEPRECATED. An account to assign the addresses to.
```

#### Result:
```
"energiaddress"  (string) A energi address associated with the keys.
```

#### Examples:

Add a multisig address from 2 addresses
```
> energi-cli addmultisigaddress 2 "[\"Xt4qk9uKvQYAonVGSZNXqxeDmtjaEWgfrs\",\"XoSoWQkpgLpppPoyyzbUFh1fq2RBvW6UK1\"]"
```

As json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "addmultisigaddress", "params": [2, "[\"Xt4qk9uKvQYAonVGSZNXqxeDmtjaEWgfrs\",\"XoSoWQkpgLpppPoyyzbUFh1fq2RBvW6UK1\"]"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## backupwallet "destination"

Safely copies wallet.dat to destination, which can be a directory or a path with filename.

#### Arguments:
```
1. "destination"   (string) The destination directory or file
```

#### Examples:
```
> energi-cli backupwallet "backup.dat"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "backupwallet", "params": ["backup.dat"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## dumphdinfo
Returns an object containing sensitive private info about this HD wallet.

#### Result:
```
{
  "hdseed": "seed",                    (string) The HD seed (bip32, in hex)
  "mnemonic": "words",                 (string) The mnemonic for this HD wallet (bip39, english words)
  "mnemonicpassphrase": "passphrase",  (string) The mnemonic passphrase for this HD wallet (bip39)
}
```

#### Examples:
```
> energi-cli dumphdinfo
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumphdinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## dumpprivkey "energiaddress"

Reveals the private key corresponding to 'energiaddress'.
Then the importprivkey can be used with this output

#### Arguments:
```
1. "energiaddress"   (string, required) The energi address for the private key
```

#### Result:
```
"key"                (string) The private key
```

#### Examples:
```
> energi-cli dumpprivkey "myaddress"
```
```
> energi-cli importprivkey "mykey"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpprivkey", "params": ["myaddress"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## dumpwallet "filename"

Dumps all wallet keys in a human-readable format.

#### Arguments:
```
1. "filename"    (string, required) The filename
```

#### Examples:
```
> energi-cli dumpwallet "test"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpwallet", "params": ["test"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## encryptwallet "passphrase"

Encrypts the wallet with 'passphrase'. This is for first time encryption.
After this, any calls that interact with private keys such as sending or signing
will require the passphrase to be set prior the making these calls.
Use the walletpassphrase call for this, and then walletlock call.
If the wallet is already encrypted, use the walletpassphrasechange call.
Note that this will shutdown the server.

#### Arguments:
```
1. "passphrase"    (string) The pass phrase to encrypt the wallet with. It must be at least 1 character, but should be long.
```

#### Examples:

Encrypt you wallet
```
> energi-cli encryptwallet "my pass phrase"
```

Now set the passphrase to use the wallet, such as for signing or sending energi
```
> energi-cli walletpassphrase "my pass phrase"
```

Now we can so something like sign
```
> energi-cli signmessage "energiaddress" "test message"
```

Now lock the wallet again by removing the passphrase
```
> energi-cli walletlock
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "encryptwallet", "params": ["my pass phrase"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getaccount "energiaddress"

DEPRECATED. Returns the account associated with the given address.

#### Arguments:
```
1. "energiaddress"  (string, required) The energi address for account lookup.
```

#### Result:
```
"accountname"        (string) the account address
```

#### Examples:
```
> energi-cli getaccount "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaccount", "params": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getaccountaddress "account"

DEPRECATED. Returns the current Energi address for receiving payments to this account.

#### Arguments:
```
1. "account"       (string, required) The account name for the address. It can also be set to the empty string "" to represent the default account. The account does not need to exist, it will be created and a new address created  if there is no account by the given name.
```

#### Result:
```
"energiaddress"   (string) The account energi address
```

#### Examples:
```
> energi-cli getaccountaddress
```
```
> energi-cli getaccountaddress ""
```
```
> energi-cli getaccountaddress "myaccount"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaccountaddress", "params": ["myaccount"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getaddressesbyaccount "account"

DEPRECATED. Returns the list of addresses for the given account.

#### Arguments:
```
1. "account"  (string, required) The account name.
```

#### Result:
```
[                     (json array of string)
  "energiaddress"  (string) a energi address associated with the given account
  ,...
]
```

#### Examples:
```
> energi-cli getaddressesbyaccount "tabby"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressesbyaccount", "params": ["tabby"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getbalance ( "account" minconf addlockconf includeWatchonly )

If account is not specified, returns the server's total available balance.
If account is specified (DEPRECATED), returns the balance in the account.
Note that the account "" is not the same as leaving the parameter out.
The server total may be different to the balance in the default "" account.

#### Arguments:
```
1. "account"        (string, optional) DEPRECATED. The selected account, or "*" for entire wallet. It may be the default account using "".
2. minconf          (numeric, optional, default=1) Only include transactions confirmed at least this many times.
3. addlockconf      (bool, optional, default=false) Whether to add 5 confirmations to transactions locked via InstantSend.
4. includeWatchonly (bool, optional, default=false) Also include balance in watchonly addresses (see 'importaddress')
```

#### Result:
```
amount              (numeric) The total amount in NRG received for this account.
```

#### Examples:

The total amount in the wallet
```
> energi-cli getbalance
```

The total amount in the wallet at least 5 blocks confirmed
```
> energi-cli getbalance "*" 6
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbalance", "params": ["*", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getnewaddress ( "account" )

Returns a new Energi address for receiving payments.
If 'account' is specified (DEPRECATED), it is added to the address book
so payments received with the address will be credited to 'account'.

#### Arguments:
```
1. "account"        (string, optional) DEPRECATED. The account name for the address to be linked to. If not provided, the default account "" is used. It can also be set to the empty string "" to represent the default account. The account does not need to exist, it will be created if there is no account by the given name.
```

#### Result:
```
"energiaddress"    (string) The new energi address
```

#### Examples:
```
> energi-cli getnewaddress
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnewaddress", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getrawchangeaddress

Returns a new Energi address, for receiving change.
This is for use with raw transactions, NOT normal use.

#### Result:
```
"address"    (string) The address
```

#### Examples:
```
> energi-cli getrawchangeaddress
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawchangeaddress", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getreceivedbyaccount "account" ( minconf addlockconf )

DEPRECATED. Returns the total amount received by addresses with <account> in transactions with specified minimum number of confirmations.

#### Arguments:
```
1. "account"      (string, required) The selected account, may be the default account using "".
2. minconf        (numeric, optional, default=1) Only include transactions confirmed at least this many times.
3. addlockconf    (bool, optional, default=false) Whether to add 5 confirmations to transactions locked via InstantSend.
```

#### Result:
```
amount            (numeric) The total amount in NRG received for this account.
```

#### Examples:

Amount received by the default account with at least 1 confirmation
```
> energi-cli getreceivedbyaccount ""
```

Amount received at the tabby account including unconfirmed amounts with zero confirmations
```
> energi-cli getreceivedbyaccount "tabby" 0
```

The amount with at least 6 confirmation, very safe
```
> energi-cli getreceivedbyaccount "tabby" 6
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getreceivedbyaccount", "params": ["tabby", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getreceivedbyaddress "energiaddress" ( minconf addlockconf )

Returns the total amount received by the given dashaddress in transactions with specified minimum number of confirmations.

#### Arguments:
```
1. "energiaddress"  (string, required) The energi address for transactions.
2. minconf        (numeric, optional, default=1) Only include transactions confirmed at least this many times.
3. addlockconf    (bool, optional, default=false) Whether to add 5 confirmations to transactions locked via InstantSend.
```

#### Result:
```
amount            (numeric) The total amount in NRG received at this address.
```

#### Examples:

The amount from transactions with at least 1 confirmation
```
> energi-cli getreceivedbyaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg"
```

The amount including unconfirmed transactions, zero confirmations
```
> energi-cli getreceivedbyaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 0
```

The amount with at least 6 confirmation, very safe
```
> energi-cli getreceivedbyaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 6
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getreceivedbyaddress", "params": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## gettransaction "txid" ( includeWatchonly )

Get detailed information about in-wallet transaction <txid>

#### Arguments:
```
1. "txid"                (string, required) The transaction id
2. "includeWatchonly"    (bool, optional, default=false) Whether to include watchonly addresses in balance calculation and details[]
```

#### Result:
```
{
  "amount" : x.xxx,        (numeric) The transaction amount in NRG
  "instantlock" : true|false, (bool) Current transaction lock state
  "confirmations" : n,     (numeric) The number of blockchain confirmations
  "blockhash" : "hash",    (string) The block hash
  "blockindex" : xx,       (numeric) The index of the transaction in the block that includes it
  "blocktime" : ttt,       (numeric) The time in seconds since epoch (1 Jan 1970 GMT)
  "txid" : "transactionid",   (string) The transaction id.
  "time" : ttt,            (numeric) The transaction time in seconds since epoch (1 Jan 1970 GMT)
  "timereceived" : ttt,    (numeric) The time received in seconds since epoch (1 Jan 1970 GMT)
  "bip125-replaceable": "yes|no|unknown"  (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                                   may be unknown for unconfirmed transactions not in the mempool
  "details" : [
    {
      "account" : "accountname",      (string) DEPRECATED. The account name involved in the transaction, can be "" for the default account.
      "address" : "energiaddress",      (string) The energi address involved in the transaction
      "category" : "send|receive",    (string) The category, either 'send' or 'receive'
      "amount" : x.xxx,               (numeric) The amount in NRG
      "label" : "label",              (string) A comment for the address/transaction, if any
      "vout" : n,                     (numeric) the vout value
    }
    ,...
  ],
  "hex" : "data"                      (string) Raw data for transaction
}
```

#### Examples:
```
> energi-cli gettransaction "1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"
```
```

> energi-cli gettransaction "1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d" true
```
```

> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettransaction", "params": ["1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## getunconfirmedbalance
Returns the server's total unconfirmed balance

## getwalletinfo
Returns an object containing various wallet state info.

#### Result:
```
{
  "walletversion": xxxxx,     (numeric) the wallet version
  "balance": xxxxxxx,         (numeric) the total confirmed balance of the wallet in NRG
  "unconfirmed_balance": xxx, (numeric) the total unconfirmed balance of the wallet in NRG
  "immature_balance": xxxxxx, (numeric) the total immature balance of the wallet in NRG
  "txcount": xxxxxxx,         (numeric) the total number of transactions in the wallet
  "keypoololdest": xxxxxx,    (numeric) the timestamp (seconds since GMT epoch) of the oldest pre-generated key in the key pool
  "keypoolsize": xxxx,        (numeric) how many new keys are pre-generated (only counts external keys)
  "keypoolsize_hd_internal": xxxx, (numeric) how many new keys are pre-generated for internal use (used for change outputs, only appears if the wallet is using this feature, otherwise external keys are used)
  "keys_left": xxxx,          (numeric) how many new keys are left since last automatic backup
  "unlocked_until": ttt,      (numeric) the timestamp in seconds since epoch (midnight Jan 1 1970 GMT) that the wallet is unlocked for transfers, or 0 if the wallet is locked
  "paytxfee": x.xxxx,         (numeric) the transaction fee configuration, set in NRG/kB
  "hdchainid": "<hash>",      (string) the ID of the HD chain
  "hdaccountcount": xxx,      (numeric) how many accounts of the HD chain are in this wallet
    [
      {
      "hdaccountindex": xxx,         (numeric) the index of the account
      "hdexternalkeyindex": xxxx,    (numeric) current external childkey index
      "hdinternalkeyindex": xxxx,    (numeric) current internal childkey index
      }
      ,...
    ]
}
```

#### Examples:
```
> energi-cli getwalletinfo
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getwalletinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## importaddress "address" ( "label" rescan p2sh )

Adds a script (in hex) or address that can be watched as if it were in your wallet but cannot be used to spend.

#### Arguments:
```
1. "script"           (string, required) The hex-encoded script (or address)
2. "label"            (string, optional, default="") An optional label
3. rescan               (boolean, optional, default=true) Rescan the wallet for transactions
4. p2sh                 (boolean, optional, default=false) Add the P2SH version of the script as well

Note: This call can take minutes to complete if rescan is true.
If you have the full public key, you should call importpublickey instead of this.
```

#### Examples:

Import a script with rescan
```
> energi-cli importaddress "myscript"
```

Import using a label without rescan
```
> energi-cli importaddress "myscript" "testing" false
```

As a JSON-RPC call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importaddress", "params": ["myscript", "testing", false] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## importelectrumwallet "filename" index

Imports keys from an Electrum wallet export file (.csv or .json)

#### Arguments:
```
1. "filename"    (string, required) The Electrum wallet export file, should be in csv or json format
2. index         (numeric, optional, default=0) Rescan the wallet for transactions starting from this block index
```

#### Examples:

Import the wallet
```
> energi-cli importelectrumwallet "test.csv"
```
```
> energi-cli importelectrumwallet "test.json"
```

Import using the json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importelectrumwallet", "params": ["test.csv"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importelectrumwallet", "params": ["test.json"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## importprivkey "energiprivkey" ( "label" rescan )

Adds a private key (as returned by dumpprivkey) to your wallet.

#### Arguments:
```
1. "energiprivkey"   (string, required) The private key (see dumpprivkey)
2. "label"            (string, optional, default="") An optional label
3. rescan               (boolean, optional, default=true) Rescan the wallet for transactions

Note: This call can take minutes to complete if rescan is true.
```

#### Examples:

Dump a private key
```
> energi-cli dumpprivkey "myaddress"
```

Import the private key with rescan
```
> energi-cli importprivkey "mykey"
```

Import using a label and without rescan
```
> energi-cli importprivkey "mykey" "testing" false
```

As a JSON-RPC call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importprivkey", "params": ["mykey", "testing", false] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## importpubkey "pubkey" ( "label" rescan )

Adds a public key (in hex) that can be watched as if it were in your wallet but cannot be used to spend.

#### Arguments:
```
1. "pubkey"           (string, required) The hex-encoded public key
2. "label"            (string, optional, default="") An optional label
3. rescan               (boolean, optional, default=true) Rescan the wallet for transactions

Note: This call can take minutes to complete if rescan is true.
```

#### Examples:

Import a public key with rescan
```
> energi-cli importpubkey "mypubkey"
```

Import using a label without rescan
```
> energi-cli importpubkey "mypubkey" "testing" false
```

As a JSON-RPC call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importpubkey", "params": ["mypubkey", "testing", false] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## importwallet "filename"

Imports keys from a wallet dump file (see dumpwallet).

#### Arguments:
```
1. "filename"    (string, required) The wallet file
```

#### Examples:

Dump the wallet
```
> energi-cli dumpwallet "test"
```

Import the wallet
```
> energi-cli importwallet "test"
```

Import using the json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importwallet", "params": ["test"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## instantsendtoaddress "energiaddress" amount ( "comment" "comment-to" subtractfeefromamount )

Send an amount to a given address. The amount is a real and is rounded to the nearest 0.00000001

#### Arguments:
```
1. "energiaddress"  (string, required) The energi address to send to.
2. "amount"      (numeric, required) The amount in btc to send. eg 0.1
3. "comment"     (string, optional) A comment used to store what the transaction is for.
                             This is not part of the transaction, just kept in your wallet.
4. "comment-to"  (string, optional) A comment to store the name of the person or organization
                             to which you're sending the transaction. This is not part of the
                             transaction, just kept in your wallet.
5. subtractfeefromamount  (boolean, optional, default=false) The fee will be deducted from the amount being sent.
                             The recipient will receive less amount of Energi than you enter in the amount field.
```

#### Result:
```
"transactionid"  (string) The transaction id.
```

#### Examples:
```
> energi-cli instantsendtoaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 0.1
```
```
> energi-cli instantsendtoaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 0.1 "donation" "seans outpost"
```
```
> energi-cli instantsendtoaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 0.1 "" "" true
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "instantsendtoaddress", "params": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg", 0.1, "donation", "seans outpost"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## keepass <genkey|init|setpassphrase>

## keypoolrefill ( newsize )

Fills the keypool.

#### Arguments
```
1. newsize     (numeric, optional, default=1000) The new keypool size
```

#### Examples:
```> energi-cli keypoolrefill
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "keypoolrefill", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## listaccounts ( minconf addlockconf includeWatchonly)

DEPRECATED. Returns Object that has account names as keys, account balances as values.

#### Arguments:
```
1. minconf           (numeric, optional, default=1) Only include transactions with at least this many confirmations
2. addlockconf       (bool, optional, default=false) Whether to add 5 confirmations to transactions locked via InstantSend.
3. includeWatchonly  (bool, optional, default=false) Include balances in watchonly addresses (see 'importaddress')
```

#### Result:
```
{                    (json object where keys are account names, and values are numeric balances
  "account": x.xxx,  (numeric) The property name is the account name, and the value is the total balance for the account.
  ...
}
```

#### Examples:

List account balances where there at least 1 confirmation
```
> energi-cli listaccounts
```

List account balances including zero confirmation transactions
```
> energi-cli listaccounts 0
```

List account balances for 6 or more confirmations
```
> energi-cli listaccounts 6
```

As json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listaccounts", "params": [6] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## listaddressgroupings

Lists groups of addresses which have had their common ownership
made public by common use as inputs or as the resulting change
in past transactions

#### Result:
```
[
  [
    [
      "energiaddress",     (string) The energi address
      amount,                 (numeric) The amount in NRG
      "account"             (string, optional) The account (DEPRECATED)
    ]
    ,...
  ]
  ,...
]
```

#### Examples:
```
> energi-cli listaddressgroupings
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listaddressgroupings", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## listlockunspent

Returns list of temporarily unspendable outputs.
See the lockunspent call to lock and unlock transactions for spending.

#### Result:
```
[
  {
    "txid" : "transactionid",     (string) The transaction id locked
    "vout" : n                      (numeric) The vout value
  }
  ,...
]
```

#### Examples:

List the unspent transactions
```
> energi-cli listunspent
```

Lock an unspent transaction
```
> energi-cli lockunspent false "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"
```

List the locked transactions
```
> energi-cli listlockunspent
```

Unlock the transaction again
```
> energi-cli lockunspent true "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listlockunspent", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## listreceivedbyaccount ( minconf addlockconf includeempty includeWatchonly)

DEPRECATED. List balances by account.

#### Arguments:
```
1. minconf           (numeric, optional, default=1) The minimum number of confirmations before payments are included.
2. addlockconf      (bool, optional, default=false) Whether to add 5 confirmations to transactions locked via InstantSend.
3. includeempty      (bool, optional, default=false) Whether to include accounts that haven't received any payments.
4. includeWatchonly  (bool, optional, default=false) Whether to include watchonly addresses (see 'importaddress').
```

#### Result:
```
[
  {
    "involvesWatchonly" : true,   (bool) Only returned if imported addresses were involved in transaction
    "account" : "accountname",    (string) The account name of the receiving account
    "amount" : x.xxx,             (numeric) The total amount received by addresses with this account
    "confirmations" : n           (numeric) The number of blockchain confirmations of the most recent transaction included
    "label" : "label"             (string) A comment for the address/transaction, if any
  }
  ,...
]
```

#### Examples:
```
> energi-cli listreceivedbyaccount
```
```
> energi-cli listreceivedbyaccount 6 false true
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbyaccount", "params": [6, false, true, true] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## listreceivedbyaddress ( minconf addlockconf includeempty includeWatchonly)

List balances by receiving address.

#### Arguments:
```
1. minconf          (numeric, optional, default=1) The minimum number of confirmations before payments are included.
2. addlockconf      (bool, optional, default=false) Whether to add 5 confirmations to transactions locked via InstantSend.
3. includeempty     (bool, optional, default=false) Whether to include addresses that haven't received any payments.
4. includeWatchonly (bool, optional, default=false) Whether to include watchonly addresses (see 'importaddress').
```

#### Result:
```
[
  {
    "involvesWatchonly" : true,        (bool) Only returned if imported addresses were involved in transaction
    "address" : "receivingaddress",    (string) The receiving address
    "account" : "accountname",         (string) DEPRECATED. The account of the receiving address. The default account is "".
    "amount" : x.xxx,                  (numeric) The total amount in NRG received by the address
    "confirmations" : n                (numeric) The number of confirmations of the most recent transaction included.
                                                 If 'addlockconf' is true, the minimum number of confirmations is calculated
                                                 including additional 5 confirmations for transactions locked via InstantSend
    "label" : "label"                  (string) A comment for the address/transaction, if any
  }
  ,...
]
```

#### Examples:
```
> energi-cli listreceivedbyaddress
```
```
> energi-cli listreceivedbyaddress 6 false true
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbyaddress", "params": [6, false, true, true] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## listsinceblock ( "blockhash" target-confirmations includeWatchonly)

Get all transactions in blocks since block [blockhash], or all transactions if omitted

#### Arguments:
```
1. "blockhash"              (string, optional) The block hash to list transactions since
2. target-confirmations:    (numeric, optional) The confirmations required, must be 1 or more
3. includeWatchonly:        (bool, optional, default=false) Include transactions to watchonly addresses (see 'importaddress')
```

#### Result:
```
{
  "transactions": [
    "account":"accountname",  (string) DEPRECATED. The account name associated with the transaction. Will be "" for the default account.
    "address":"energiaddress",  (string) The energi address of the transaction. Not present for move transactions (category = move).
    "category":"send|receive",  (string) The transaction category. 'send' has negative amounts, 'receive' has positive amounts.
    "amount": x.xxx,          (numeric) The amount in NRG. This is negative for the 'send' category, and for the 'move' category for moves
                                          outbound. It is positive for the 'receive' category, and for the 'move' category for inbound funds.
    "vout" : n,               (numeric) the vout value
    "fee": x.xxx,             (numeric) The amount of the fee in NRG. This is negative and only available for the 'send' category of transactions.
    "instantlock" : true|false, (bool) Current transaction lock state. Available for 'send' and 'receive' category of transactions.
    "confirmations" : n,      (numeric) The number of blockchain confirmations for the transaction. Available for 'send' and 'receive' category of transactions.
    "blockhash": "hashvalue", (string) The block hash containing the transaction. Available for 'send' and 'receive' category of transactions.
    "blockindex": n,          (numeric) The index of the transaction in the block that includes it. Available for 'send' and 'receive' category of transactions.
    "blocktime": xxx,         (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
    "txid": "transactionid",  (string) The transaction id. Available for 'send' and 'receive' category of transactions.
    "time": xxx,              (numeric) The transaction time in seconds since epoch (Jan 1 1970 GMT).
    "timereceived": xxx,      (numeric) The time received in seconds since epoch (Jan 1 1970 GMT). Available for 'send' and 'receive' category of transactions.
    "comment": "...",         (string) If a comment is associated with the transaction.
    "label" : "label"         (string) A comment for the address/transaction, if any
    "to": "...",              (string) If a comment to is associated with the transaction.
  ],
  "lastblock": "lastblockhash"  (string) The hash of the last block
}
```

#### Examples:
```
> energi-cli listsinceblock
```
```
> energi-cli listsinceblock "000000000000000bacf66f7497b7dc45ef753ee9a7d38571037cdb1a57f663ad" 6
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listsinceblock", "params": ["000000000000000bacf66f7497b7dc45ef753ee9a7d38571037cdb1a57f663ad", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## listtransactions    ( "account" count from includeWatchonly)

Returns up to 'count' most recent transactions skipping the first 'from' transactions for account 'account'.

#### Arguments:
```
1. "account"        (string, optional) DEPRECATED. The account name. Should be "*".
2. count            (numeric, optional, default=10) The number of transactions to return
3. from             (numeric, optional, default=0) The number of transactions to skip
4. includeWatchonly (bool, optional, default=false) Include transactions to watchonly addresses (see 'importaddress')
```

#### Result:
```
[
  {
    "account":"accountname",  (string) DEPRECATED. The account name associated with the transaction.
                                                It will be "" for the default account.
    "address":"energiaddress",  (string) The energi address of the transaction. Not present for
                                                move transactions (category = move).
    "category":"send|receive|move", (string) The transaction category. 'move' is a local (off blockchain)
                                                transaction between accounts, and not associated with an address,
                                                transaction id or block. 'send' and 'receive' transactions are
                                                associated with an address, transaction id and block details
    "amount": x.xxx,          (numeric) The amount in NRG. This is negative for the 'send' category, and for the
                                         'move' category for moves outbound. It is positive for the 'receive' category,
                                         and for the 'move' category for inbound funds.
    "vout": n,                (numeric) the vout value
    "fee": x.xxx,             (numeric) The amount of the fee in NRG. This is negative and only available for the
                                         'send' category of transactions.
    "instantlock" : true|false, (bool) Current transaction lock state. Available for 'send' and 'receive' category of transactions.
    "confirmations": n,       (numeric) The number of blockchain confirmations for the transaction. Available for 'send' and
                                         'receive' category of transactions. Negative confirmations indicate the
                                         transation conflicts with the block chain
    "trusted": xxx            (bool) Whether we consider the outputs of this unconfirmed transaction safe to spend.
    "blockhash": "hashvalue", (string) The block hash containing the transaction. Available for 'send' and 'receive'
                                          category of transactions.
    "blockindex": n,          (numeric) The index of the transaction in the block that includes it. Available for 'send' and 'receive'
                                          category of transactions.
    "blocktime": xxx,         (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
    "txid": "transactionid",  (string) The transaction id. Available for 'send' and 'receive' category of transactions.
    "time": xxx,              (numeric) The transaction time in seconds since epoch (midnight Jan 1 1970 GMT).
    "timereceived": xxx,      (numeric) The time received in seconds since epoch (midnight Jan 1 1970 GMT). Available
                                          for 'send' and 'receive' category of transactions.
    "comment": "...",         (string) If a comment is associated with the transaction.
    "label": "label"          (string) A comment for the address/transaction, if any
    "otheraccount": "accountname",  (string) For the 'move' category of transactions, the account the funds came
                                          from (for receiving funds, positive amounts), or went to (for sending funds,
                                          negative amounts).
    "bip125-replaceable": "yes|no|unknown"  (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                                     may be unknown for unconfirmed transactions not in the mempool
  }
]
```

#### Examples:

List the most recent 10 transactions in the systems
```
> energi-cli listtransactions
```

List transactions 100 to 120
```
> energi-cli listtransactions "*" 20 100
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listtransactions", "params": ["*", 20, 100] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## listunspent ( minconf maxconf ["address",...] )

Returns array of unspent transaction outputs
with between minconf and maxconf (inclusive) confirmations.
Optionally filter to only include txouts paid to specified addresses.
Results are an array of Objects, each of which has:
{txid, vout, scriptPubKey, amount, confirmations}

#### Arguments:
```
1. minconf          (numeric, optional, default=1) The minimum confirmations to filter
2. maxconf          (numeric, optional, default=9999999) The maximum confirmations to filter
3. "addresses"    (string) A json array of energi addresses to filter
    [
      "address"   (string) energi address
      ,...
    ]
```

#### Result:
```
[                             (array of json object)
  {
    "txid" : "txid",          (string) the transaction id
    "vout" : n,               (numeric) the vout value
    "address" : "address",  (string) the energi address
    "account" : "account",  (string) DEPRECATED. The associated account, or "" for the default account
    "scriptPubKey" : "key", (string) the script key
    "amount" : x.xxx,         (numeric) the transaction amount in NRG
    "confirmations" : n       (numeric) The number of confirmations
    "ps_rounds" : n           (numeric) The number of PS round
    "spendable" : xxx,        (bool) Whether we have the private keys to spend this output
    "solvable" : xxx          (bool) Whether we know how to spend this output, ignoring the lack of keys
  }
  ,...
]
```

#### Examples:
```
> energi-cli listunspent
```
```
> energi-cli listunspent 6 9999999 "[\"XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg\",\"XuQQkwA4FYkq2XERzMY2CiAZhJTEDAbtcg\"]"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [6, 9999999 "[\"XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg\",\"XuQQkwA4FYkq2XERzMY2CiAZhJTEDAbtcg\"]"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## lockunspent unlock [{"txid":"txid","vout":n},...]

Updates list of temporarily unspendable outputs.
Temporarily lock (unlock=false) or unlock (unlock=true) specified transaction outputs.
A locked transaction output will not be chosen by automatic coin selection, when spending NRG.
Locks are stored in memory only. Nodes start with zero locked outputs, and the locked output list
is always cleared (by virtue of process exit) when a node stops or fails.
Also see the listunspent call

#### Arguments:
```
1. unlock            (boolean, required) Whether to unlock (true) or lock (false) the specified transactions
2. "transactions"  (string, required) A json array of objects. Each object the txid (string) vout (numeric)
     [           (json array of json objects)
       {
         "txid":"id",    (string) The transaction id
         "vout": n         (numeric) The output number
       }
       ,...
     ]
```

#### Result:
```
true|false    (boolean) Whether the command was successful or not
```

#### Examples:

List the unspent transactions
```
> energi-cli listunspent
```

Lock an unspent transaction
```
> energi-cli lockunspent false "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"
```

List the locked transactions
```
> energi-cli listlockunspent
```

Unlock the transaction again
```
> energi-cli lockunspent true "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "lockunspent", "params": [false, "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## move "fromaccount" "toaccount" amount ( minconf "comment" )

DEPRECATED. Move a specified amount from one account in your wallet to another.

#### Arguments:
```
1. "fromaccount"    (string, required) The name of the account to move funds from. May be the default account using "".
2. "toaccount"      (string, required) The name of the account to move funds to. May be the default account using "".
3. amount           (numeric) Quantity of NRG to move between accounts.
4. minconf          (numeric, optional, default=1) Only use funds with at least this many confirmations.
5. "comment"        (string, optional) An optional comment, stored in the wallet only.
```

#### Result:
```
true|false          (boolean) true if successful.
```

#### Examples:

Move 0.01 NRG from the default account to the account named tabby
```
> energi-cli move "" "tabby" 0.01
```

Move 0.01 NRG timotei to akiko with a comment and funds have 6 confirmations
```
> energi-cli move "timotei" "akiko" 0.01 6 "happy birthday!"
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "move", "params": ["timotei", "akiko", 0.01, 6, "happy birthday!"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## sendfrom "fromaccount" "toenergiaddress" amount ( minconf addlockconf "comment" "comment-to" )

DEPRECATED (use sendtoaddress). Sent an amount from an account to an energi address.

#### Arguments:
```
1. "fromaccount"    (string, required) The name of the account to send funds from. May be the default account using "".
2. "toenergiaddress"  (string, required) The energi address to send funds to.
3. amount           (numeric or string, required) The amount in NRG (transaction fee is added on top).
4. minconf          (numeric, optional, default=1) Only use funds with at least this many confirmations.
5. addlockconf      (bool, optional, default=false) Whether to add 5 confirmations to transactions locked via InstantSend.
6. "comment"        (string, optional) A comment used to store what the transaction is for.
                                     This is not part of the transaction, just kept in your wallet.
7. "comment-to"     (string, optional) An optional comment to store the name of the person or organization
                                     to which you're sending the transaction. This is not part of the transaction,
                                     it is just kept in your wallet.
```

#### Result:
```
"transactionid"     (string) The transaction id.
```

#### Examples:

Send 0.01 NRG from the default account to the address, must have at least 1 confirmation
```
> energi-cli sendfrom "" "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 0.01
```

Send 0.01 from the tabby account to the given address, funds must have at least 6 confirmations
```
> energi-cli sendfrom "tabby" "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 0.01 6 false "donation" "seans outpost"
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendfrom", "params": ["tabby", "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg", 0.01, 6, false, "donation", "seans outpost"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## sendmany "fromaccount" {"address":amount,...} ( minconf addlockconf "comment" ["address",...] subtractfeefromamount use_is use_ps )

Send multiple times. Amounts are double-precision floating point numbers.

#### Arguments:
```
1. "fromaccount"           (string, required) DEPRECATED. The account to send the funds from. Should be "" for the default account
2. "amounts"               (string, required) A json object with addresses and amounts
    {
      "address":amount     (numeric or string) The energi address is the key, the numeric amount (can be string) in NRG is the value
      ,...
    }
3. minconf                 (numeric, optional, default=1) Only use the balance confirmed at least this many times.
4. addlockconf             (bool, optional, default=false) Whether to add 5 confirmations to transactions locked via InstantSend.
5. "comment"               (string, optional) A comment
6. subtractfeefromamount   (string, optional) A json array with addresses.
                           The fee will be equally deducted from the amount of each selected address.
                           Those recipients will receive less NRG than you enter in their corresponding amount field.
                           If no addresses are specified here, the sender pays the fee.
    [
      "address"            (string) Subtract fee from this address
      ,...
    ]
7. "use_is"                (bool, optional) Send this transaction as InstantSend (default: false)
8. "use_ps"                (bool, optional) Use anonymized funds only (default: false)
```

#### Result:
```
"transactionid"            (string) The transaction id for the send. Only 1 transaction is created regardless of
                                    the number of addresses.
```

#### Examples:

Send two amounts to two different addresses:
```
> energi-cli sendmany "tabby" "{\"XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg\":0.01,\"XuQQkwA4FYkq2XERzMY2CiAZhJTEDAbtcg\":0.02}"
```

Send two amounts to two different addresses setting the confirmation and comment:
```
> energi-cli sendmany "tabby" "{\"XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg\":0.01,\"XuQQkwA4FYkq2XERzMY2CiAZhJTEDAbtcg\":0.02}" 6 false "testing"
```

As a json rpc call
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendmany", "params": ["tabby", "{\"XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg\":0.01,\"XuQQkwA4FYkq2XERzMY2CiAZhJTEDAbtcg\":0.02}", 6, false, "testing"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## sendtoaddress "energiaddress" amount ( "comment" "comment-to" subtractfeefromamount use_is use_ps )

Send an amount to a given address.

#### Arguments:
```
1. "energiaddress" (string, required) The energi address to send to.
2. "amount"      (numeric or string, required) The amount in NRG to send. eg 0.1
3. "comment"     (string, optional) A comment used to store what the transaction is for.
                             This is not part of the transaction, just kept in your wallet.
4. "comment-to"  (string, optional) A comment to store the name of the person or organization
                             to which you're sending the transaction. This is not part of the
                             transaction, just kept in your wallet.
5. subtractfeefromamount  (boolean, optional, default=false) The fee will be deducted from the amount being sent.
                             The recipient will receive less amount of Energi than you enter in the amount field.
6. "use_is"      (bool, optional) Send this transaction as InstantSend (default: false)
7. "use_ps"      (bool, optional) Use anonymized funds only (default: false)
```

#### Result:
```
"transactionid"  (string) The transaction id.
```

#### Examples:
```
> energi-cli sendtoaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 0.1
```
```
> energi-cli sendtoaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 0.1 "donation" "seans outpost"
```
```
> energi-cli sendtoaddress "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" 0.1 "" "" true
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendtoaddress", "params": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg", 0.1, "donation", "seans outpost"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## setaccount "energiaddress" "account"

DEPRECATED. Sets the account associated with the given address.

#### Arguments:
```
1. "energiaddress"  (string, required) The energi address to be associated with an account.
2. "account"         (string, required) The account to assign the address to.
```

#### Examples:
```
> energi-cli setaccount "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" "tabby"
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setaccount", "params": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg", "tabby"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## settxfee amount

Set the transaction fee per kB. Overwrites the paytxfee parameter.

#### Arguments:
```
1. amount         (numeric or sting, required) The transaction fee in NRG/kB
```

#### Result:
```
true|false        (boolean) Returns true if successful
```

#### Examples:
```
> energi-cli settxfee 0.00001
```
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "settxfee", "params": [0.00001] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```

## signmessage "energiaddress" "message"

Sign a message with the private key of an address

#### Arguments:
```
1. "energiaddress"  (string, required) The energi address to use for the private key.
2. "message"         (string, required) The message to create a signature of.
```

#### Result:
```
"signature"          (string) The signature of the message encoded in base 64
```

#### Examples:

Unlock the wallet for 30 seconds
```
> energi-cli walletpassphrase "mypassphrase" 30
```

Create the signature
```
> energi-cli signmessage "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" "my message"
```

Verify the signature
```
> energi-cli verifymessage "XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg" "signature" "my message"
```

As json rpc
```
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signmessage", "params": ["XwnLY9Tf7Zsef8gMGL2fhWA9ZmMjt4KPwg", "my message"] }' -H 'content-type: text/plain;' http://127.0.0.1:9796/
```
