# Everything about Assume UTXO

[Proposal](https://github.com/jamesob/assumeutxo-docs/tree/2019-04-proposal/proposal)

Assume UTXO is feature introduced in Bitcoin Core back in 2019 by [jamesob](github.com/jamesob) to make running a full node easier. 


AssumeUTXO is another idea introduced in Bitcoin core to make a running node easier by using UTXO snapshots. This snapshot is like a pre-made list of all the "coins" available to spend at a specific point in the blockchain. 

## How Does It Work?
A node downloads a UTXO snapshot (about 3.2 GB) from a trusted source, like a CDN or another node.
It uses a hardcoded hash in Bitcoin Core to verify the snapshot's integrity.
The node can then immediately start validating new blocks and transactions, while it verifies older blocks in the background.
This background process ensures the node eventually fully validates the blockchain, maintaining security.
UTXO Snapshot: This is a serialized version of the UTXO set, including metadata such as total coins and the latest block header. The size is approximately 3.2 GB, significantly smaller than the full blockchain.

**Hardcoded assumeutxo Hash**: A SHA256 hash of the UTXO set at a specific height is hardcoded into Bitcoin Core. This hash is reviewed and verified by developers during code review to ensure it corresponds to a valid UTXO set. The node uses this hash to verify the integrity of the downloaded snapshot.

bitcoin-cli dumptxoutset  <output file location>/snapshots.dat - for creating utxo snapshots

bitcoin-cli loadtxoutset "path" - for loading the utxo snapshots

### Open PR [here](https://github.com/bitcoin/bitcoin/pull/15606)










