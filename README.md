# Optimizations in IBD - Initial Block Download

When you run bitcoin-core for the first time, to participate in bitcoin network, the node needs to first sync with the blockchain(aka bitcoin network) first
which includes downloading all the blocks. This is known as Initail Block Download.

# Major Challenges

- Downloading the entire blockchain data is time consuming as downloading the entire blockchain requires huge bandwidth and storage usage

# History for IBD improvements

- Headers first sync
- AssumeValid
- Assume UTXO
- Utreexo

- IBD Tracking Issue in Bitcoin Core [#32042](https://github.com/bitcoin/bitcoin/pull/32043)












