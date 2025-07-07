
# 🌿 Drosera Node v1.20.0 — Migration from Holesky to Hoodi

## 🚰 Faucet (Get Testnet ETH)
- [QuickNode Faucet](https://faucet.quicknode.com/ethereum/hoodi)
- [Stakely Faucet](https://stakely.io/faucet/ethereum-hoodi-testnet-eth)

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

Paste and edit the config:

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
```

🔗 Replace:
- `YOUR-ETH-ADDRESS` and `TRAP-ADDRESS` from:  
  [https://app.drosera.io/?filters=withTrapsOwned&userAddress=YOUR-ETH-ADDRESS](https://app.drosera.io/?filters=withTrapsOwned&userAddress=YOUR-ETH-ADDRESS)

...

> Made with ❤️ for Drosera Operators
