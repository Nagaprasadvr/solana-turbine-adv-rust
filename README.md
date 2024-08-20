# solana-turbine-adv-rust

## Few Concepts covered during Advance Rust Cohort
1.How does process_instruction (entrypoint of a solana program logic works) covered topics :
  a. Transaction Context
  b. Invoke Context
  c. processing accounts , ix_data and checking for signatures, loading program to eBPF and vm

## 2.Replay Stage - A stage involving validators receiving bloks (including forks) in shars and how these shards are processed ot txs and loaded to bank for processing these txs

## Few Optimizations I worked on - 
## 1. P2P sharding of solana chain Snapshot (recent txs , accounts req to kickstart a new validator) 
## Currently a validator node trying to join a network needs to download the account data and snapshot data , downloading the same from a single peer node could be a lot of data and time consuming
## Instead rpc/validator trying to join can fan out requests and download shards from multiple sources without burdening a single node.
## Keeping in mind security and speed this can be achieved with p2p sharding and merkel tree of account data shards and snapshot shards
## If a validator node or an rpc node wants to join the network then they can request shards from peers and also a merkel tree of all shards (peers will already have all shards)
## This way the new validator can download shards alike bittorrent or ipfs (concurrently) also verify if these shards are valid by constructing the Merkel tree from these shards and comparing this against the merkle tree which is common among super majority.
## We can even know which validator node is serving bad shards and eliminate them and request from a different validator

## 3. a P2P cli client for state channels using solana svm (WIP) - [(https://github.com/Nagaprasadvr/solana-state-channels-pubsub)
