
# MintFi

## Overview

MintFi leverages cutting-edge cryptographic techniques, such as Groth16 and Pairing-Based Cryptography, to enhance the security and efficiency of decentralized finance on the Zulu Network. This project focuses on the application of Zero-Knowledge Proofs (ZKPs) to validate complex operations while maintaining privacy and minimizing computational overhead.

## Getting Started

### Running Proof-of-Concept (PoC)

To execute the Proof-of-Concept for Pairing-Based Cryptography:

```bash
cargo test test_dual_miller_loop_with_c_wi_fixed -- --nocapture
```

### Running Groth16 Verifier

To run the Groth16 verifier that leverages the power of 'prove-on-pairing':

```bash
cargo test test_groth16_verifier -- --nocapture
```

## Bitcoin Script Integration

MintFi integrates Bitcoin scripts directly in Rust for enhanced flexibility and security in smart contract operations.

### Usage

The crate exports a `script!` macro to build Bitcoin scripts, returning the [`Script`](https://docs.rs/bitcoin/latest/bitcoin/struct.ScriptBuf.html) type from the [`bitcoin`](https://github.com/rust-bitcoin/rust-bitcoin) crate.

**Example:**

```rust
#![feature(proc_macro_hygiene)]

use bitcoin_script::bitcoin_script;

let htlc_script = script! {
    OP_IF
        OP_SHA256 <digest> OP_EQUALVERIFY OP_DUP OP_SHA256 <seller_pubkey_hash>
    OP_ELSE
        100 OP_CSV OP_DROP OP_DUP OP_HASH160 <buyer_pubkey_hash>
    OP_ENDIF
    OP_EQUALVERIFY
    OP_CHECKSIG
};
```

### Syntax and Optimization

Scripts follow standard Bitcoin syntax and optimize opcode sequences, ensuring efficient and secure execution on the Zulu Network.

## zkSync2-js JavaScript SDK

MintFi integrates the `zksync2-js` JavaScript SDK for seamless interaction with the zkSync Era on the Zulu Network.

### Installation

Ensure you have Node.js v18 or later and install the required dependencies:

```bash
yarn add zksync2-js
yarn add ethers@6
```


**Connecting to zkSync Era Network:**

```ts
import {Provider, utils, types} from "zksync2-js";
import {ethers} from "ethers";

const provider = Provider.getDefaultProvider(types.Network.Goerli); // zkSync Era testnet (L2)
const ethProvider = ethers.getDefaultProvider("goerli"); // goerli testnet (L1)
```

**Transfer Funds on L2:**

```ts
const transfer = await wallet.transfer({
    to: receiver,
    token: utils.ETH_ADDRESS,
    amount: ethers.parseEther("1.0"),
});
```
