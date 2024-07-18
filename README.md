<div align=center>
  <img src="https://github.com/TempGROX/TempGROX/blob/main/src/photos/images.jfif">
  <h1>Full-0G-DA-install-guide</h1>
  <br>
</div>

# DA CLIENT

## Hardware Requirement
|KEY|VALUE|
|:--|:----|
|**RAM**|8 GB|
|**CPU**|2 cores|
|**Bandwidth**|100Mbps for D/U|

## Install DA Client for Linux
1. Install Dependencies
  ```bash
  sudo apt-get update
  sudo apt-get install cmake
  ```
2. Install Go
  ```bash
  wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz
  rm -rf /usr/local/go && tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz
  ```
  Add to your env
  ```bash
  export PATH=$PATH:/usr/local/go/bin
  ```
3. Download the source code
   ```bash
   git clone -b v1.0.0-testnet https://github.com/0glabs/0g-da-client.git
   ```

## Build and Run
Build:
```bash
make build
```

Run:
```bash
./bin/combined \
    --chain.rpc https://rpc-testnet.0g.ai \
    --chain.private-key 0x00 \
    --chain.receipt-wait-rounds 180 \
    --chain.receipt-wait-interval 1s \
    --chain.gas-limit 2000000 \
    --combined-server.use-memory-db \
    --combined-server.storage.kv-db-path ./../run/ \
    --combined-server.storage.time-to-expire 300 \
    --disperser-server.grpc-port 51001 \
    --batcher.da-entrance-contract 0xDFC8B84e3C98e8b550c7FEF00BCB2d8742d80a69 \
    --batcher.da-signers-contract 0x0000000000000000000000000000000000001000 \
    --batcher.finalizer-interval 20s \
    --batcher.confirmer-num 3 \
    --batcher.max-num-retries-for-sign 3 \
    --batcher.finalized-block-count 50 \
    --batcher.batch-size-limit 500 \
    --batcher.encoding-interval 3s \
    --batcher.encoding-request-queue-size 1 \
    --batcher.pull-interval 10s \
    --batcher.signing-interval 3s \
    --batcher.signed-pull-interval 20s \
    --encoder-socket 52.198.175.144:34000 \
    --encoding-timeout 600s \
    --signing-timeout 600s \
    --chain-read-timeout 12s \
    --chain-write-timeout 13s \
    --combined-server.log.level-file trace \
    --combined-server.log.level-std  trace \
    --combined-server.log.path ./../run/run.log
```

# DA NODE
## Hardware Requirement

|KEY|VALUE|
|:--|:----|
|RAM|16 GB|
|Disk|1 TB NVME SSD|
|Bandwidth|100 MBps|

## Installation
```bash
git clone https://github.com/0glabs/0g-da-node.git
cargo build --release
./dev_support/download_params.sh
```

## Configuration
Create a `config.toml` file and set values:

```toml
log_level = "info"

data_path = "./db/"

# path to downloaded params folder
encoder_params_dir = "params/" 

# grpc server listen address
grpc_listen_address = "0.0.0.0:34000"
# chain eth rpc endpoint
eth_rpc_endpoint = "https://rpc-testnet.0g.ai"
# public grpc service socket address to register in DA contract
# ip:34000 (keep same port as the grpc listen address)
# or if you have dns, fill your dns
socket_address = "<public_ip/dns>:34000"

# data availability contract to interact with
da_entrance_address = ""
# deployed block number of da entrance contract
start_block_number = 0

# signer BLS private key
signer_bls_private_key = ""
# signer eth account private key
signer_eth_private_key = ""

# whether to enable data availability sampling
enable_das = "false"
```

**Generate key:**

```bash
cargo run --bin key-gen
```

## Run
```bash
./target/release/server --config cargo.toml
```

# The end!
If you liked this guide, please go to all my social networks)

<br>
<div id="badges" align="center">
  <a href="https://discord.com/users/961408999411048461">
    <img src="https://img.shields.io/badge/Discord-blue?style=for-the-badge&logo=https%3A%2F%2Fimg.icons8.com%2Fios%2F50%2Fmedium-logo.png&logoColor=white" alt="LinkedIn Badge"/>
  </a>
  <a href="https://medium.com/@James_Brandon">
    <img src="https://img.shields.io/badge/Medium-black?style=for-the-badge&logo=https%3A%2F%2Fimg.icons8.com%2Fios%2F50%2Fmedium-logo.png&logoColor=white" alt="Youtube Badge"/>
  </a>
  <a href="https://keybase.io/jamesbrandon">
    <img src="https://img.shields.io/badge/Keybase-orange?style=for-the-badge&logo=https%3A%2F%2Fimg.icons8.com%2Fios%2F50%2Fmedium-logo.png&logoColor=white">
  </a>
  <a href="https://x.com/JBTGrox">
    <img src="https://img.shields.io/badge/Twitter-blue?style=for-the-badge&logo=twitter&logoColor=white" alt="Twitter Badge"/>
  </a>
  <a href="https://linktr.ee/JBrandon_?utm_source=linktree_admin_share">
    <img src="https://img.shields.io/badge/Linktree-green?style=for-the-badge&logo=https%3A%2F%2Fimg.icons8.com%2Fios%2F50%2Fmedium-logo.png&logoColor=white">
  </a>
</div>
