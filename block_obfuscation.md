# Block Obfuscation (https://github.com/bitcoin/bitcoin/pull/6650)

Block Obfuscations in Bitcoin Core is a mechanism designed to prevent certain data patterns from being misidentified by antivirus software as malicious. This is basically achieved by applying a simple XOR operation using the obfuscation key derived from cryptographically random number which also acts as key in the leveldb database.

## Purpose of Obfuscation

Initially, Bitcoin Core's `chainstate` database, which maintains the Unspent Transaction Output (UTXO) set, occasionally triggered false positives in antivirus programs due to recognizable byte patterns. To mitigate this, Bitcoin Core introduced an obfuscation scheme where a randomly generated 64-bit key is XORed with the data, effectively masking these patterns without adding significant computational overhead. 

In v28.0, this feature was extended to `blocks` directory as well through -blocksxor option, see https://github.com/bitcoin/bitcoin/pull/28052. The xor key is stored in the `blocks` folder so that the node can undo it when reading.
