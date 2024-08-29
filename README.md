# Nillion-Verifier-Node
Nillion for Linux or WSL

- Add [Nillion Chain](https://chains.keplr.app/) to Keplr
- Search for `Nillion` in Keplr wallet, you will get `Nillion address`
- Get $NIL Token : [Faucet site](https://faucet.testnet.nillion.com/)


Upgrade System and Install Docker
```bash
sudo apt update -y && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common && sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && sudo apt update -y && apt-cache policy docker-ce && sudo apt install -y docker-ce && sudo usermod -aG docker ${USER} && su - ${USER} -c "groups" && docker --version
```

Pull image from the Nillion repo in Docker Hub.
```bash
docker pull nillion/retailtoken-accuser:v1.0.0
```

Create directory and initialise the accuser in the mounted directory.
```bash
mkdir -p nillion/accuser && docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 initialise
```

- After running commands you will see `Account_id` and `Public_key`

- Visit [Nillion Verifier Site](https://verifier.nillion.com/verifier) Put `Account_id` and `Public_key` in section 5.

- Visit [Faucet site](https://faucet.testnet.nillion.com/) to request faucet in your `Account_id` you copied earlier

- back to Terminal run commands below for get your accuser wallet private key

- Backup you private key

After 60 mins, run commands below
```bash
current_block=$(curl -s https://testnet-nillion-rpc.lavenderfive.com/abci_info | jq -r '.result.response.last_block_height'); block_start=$((current_block - 5)); docker run -v $(pwd)/nillion/accuser:/var/tmp nillion/retailtoken-accuser:latest accuse --rpc-endpoint "http://65.109.222.111:26657" --block-start $block_start
```
