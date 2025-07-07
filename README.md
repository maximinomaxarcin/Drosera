
# 🌿 Drosera Node Migration Guide

> **Version:** v1.20.0  
> **Network Change:** Holesky ➜ Hoodi  
> **Last Updated:** July 2025

---

## 🚀 Quick Links

- 🌐 [Faucet (Get Testnet ETH)](#faucet-get-testnet-eth)
- 🛠️ [System Preparation](#system-preparation--firewall-setup)
- 🧯 [Stop Current Node](#stop-current-drosera-node)
- ⬆️ [Install/Update CLI](#install--update-drosera-cli)
- ⚙️ [Configure drosera.toml](#️configure-droseratoml)
- 💾 [Update docker-compose.yaml](#️edit-your-docker-composeyaml)
- 🧪 [Setup & Register Trap](#setup-your-trap)
- 🌸 [Bloom Boost](#send-bloom-boost-your-trap)
- ✅ [Run Node](#running-your-node)
- 🧰 [Command Reference](#command-help)

---

## 🚰 Faucet (Get Testnet ETH)
- 🔹 [QuickNode Faucet](https://faucet.quicknode.com/ethereum/hoodi)
- 🔹 [Stakely Faucet](https://stakely.io/faucet/ethereum-hoodi-testnet-eth)

---

## 🛠️ System Preparation & Firewall Setup

```bash
sudo apt update && sudo apt upgrade -y && \
sudo apt autoremove -y && \
sudo ufw allow ssh && \
sudo ufw allow 22 && \
sudo ufw allow 31313/tcp && \
sudo ufw allow 31314/tcp && \
sudo ufw enable
```

---

## 🛑 Stop Current Drosera Node

```bash
cd ~/Drosera-Network && sudo docker compose down -v
```

---

## ⬆️ Install / Update Drosera CLI

```bash
curl -L https://app.drosera.io/install | bash
source ~/.bashrc
droseraup
```

---

## ✏️ Configure `drosera.toml`

```bash
cd ~/my-drosera-trap && nano drosera.toml
```

Paste and customize the configuration.

🔗 Replace:
- `YOUR-ETH-ADDRESS` with your wallet address.
- `TRAP-ADDRESS` from: [https://app.drosera.io/?filters=withTrapsOwned&userAddress=YOUR-ETH-ADDRESS](https://app.drosera.io/?filters=withTrapsOwned&userAddress=YOUR-ETH-ADDRESS)

<details>
<summary>Click to expand sample config</summary>

```toml
ethereum_rpc = "https://ethereum-hoodi-rpc.publicnode.com"
drosera_rpc = "https://relay.hoodi.drosera.io"
eth_chain_id = 560048
drosera_address = "0x91cB447BaFc6e0EA0F4Fe056F5a9b1F14bb06e5D"

[traps]

[traps.mytrap]
path = "out/HelloWorldTrap.sol/HelloWorldTrap.json"
response_contract = "0x183D78491555cb69B68d2354F7373cc2632508C7"
response_function = "helloworld(string)"
cooldown_period_blocks = 33
min_number_of_operators = 1
max_number_of_operators = 2
block_sample_size = 10
private_trap = true
whitelist = ["YOUR-ETH-ADDRESS"]
address = "TRAP-ADDRESS"

[traps.mytrap2]
# Duplicate trap config if you have multiple traps
```

</details>

---

## 🔄 Update Trap Config

```bash
DROSERA_PRIVATE_KEY=EVM-PRIVATE-KEY drosera apply
```

---

## 🌸 Send Bloom Boost Your Trap

- [Bloom Boost UI](https://app.drosera.io/?filters=withTrapsOwned&userAddress=YOUR-ETH-ADDRESS)

OR CLI:

```bash
drosera bloomboost --private-key <EVM-PRIVATE-KEY> --trap-address <TRAP-ADDRESS> --eth-amount <ETH-AMOUNT-TO-STAKE>
```

---

## 🐳 Edit your `docker-compose.yaml`

```bash
cd ~/Drosera-Network && nano docker-compose.yaml
```

[Full Docker Compose Example](#️edit-your-docker-composeyaml)  
*(Make sure to update `${ETH_PRIVATE_KEY}` and `${VPS_IP}`)*

---

## 📦 Update Operator Image

```bash
sudo docker pull ghcr.io/drosera-network/drosera-operator:latest
```

---

## 🧪 Setup Your Trap

```bash
drosera-operator register \
  --eth-rpc-url https://0xrpc.io/hoodi \
  --eth-private-key EVM-PRIVATE-KEY \
  --drosera-address 0x91cB447BaFc6e0EA0F4Fe056F5a9b1F14bb06e5D
```

> If error, fallback:

```bash
docker run -it ghcr.io/drosera-network/drosera-operator:latest register \
  --eth-rpc-url https://0xrpc.io/hoodi \
  --eth-private-key EVM-PRIVATE-KEY \
  --drosera-address 0x91cB447BaFc6e0EA0F4Fe056F5a9b1F14bb06e5D \
  --trap-config-address TRAP-ADDRESS
```

---

## ✅ Opt-in Operator

Repeat for each operator (with different private keys):

```bash
docker run -it ghcr.io/drosera-network/drosera-operator:latest optin \
  --eth-rpc-url https://0xrpc.io/hoodi \
  --eth-private-key EVM-PRIVATE-KEY \
  --drosera-address 0x91cB447BaFc6e0EA0F4Fe056F5a9b1F14bb06e5D \
  --trap-config-address TRAP-ADDRESS
```

---

## ▶️ Running Your Node

```bash
sudo docker compose up -d
```

---

## 🧰 Command Help

| Command                  | Description           |
|--------------------------|------------------------|
| `sudo docker compose up -d` | Start node |
| `sudo docker compose down -v` | Stop node |
| `sudo docker compose logs -f` | View logs |

---

> Made with ❤️ by Drosera Contributors

