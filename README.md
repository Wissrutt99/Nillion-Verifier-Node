# Nillion's Verifier Program
Nillion's for Linux/WSL

- Add [Nillion Chain](https://chains.keplr.app/) to Keplr
- Search `Nillion` in Keplr wallet, you will get `Nillion address`
- Get $NIL Token : [Faucet site](https://faucet.testnet.nillion.com/)


### Upgrade System and Install Docker
```bash
sudo apt update -y && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common && sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && sudo apt update -y && apt-cache policy docker-ce && sudo apt install -y docker-ce && sudo usermod -aG docker ${USER} && su - ${USER} -c "groups" && docker --version
```

### Pull image from the Nillion repo in Docker Hub.
```bash
docker pull nillion/retailtoken-accuser:v1.0.0
```

### Create directory and initialise the accuser in the mounted directory.
```bash
mkdir -p nillion/accuser && docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 initialise
```

- After running commands you will see `Account_id` and `Public_key`

- Visit [Nillion Verifier Site](https://verifier.nillion.com/verifier) Put `Account_id` and `Public_key` in section 5.

- Visit [Faucet site](https://faucet.testnet.nillion.com/) to request faucet in your `Account_id` you copied earlier

- back to Terminal run commands below for get your accuser wallet private key

```bash
cat ~/nillion/accuser/credentials.json
```

- Backup you private key

### Run Accuser
Wait 30-60 mins to continue with the steps below. The secret verification is designed wait for a period of time before fully registering the accuser

```bash
docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 accuse --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com" --block-start 5125112
```

### check Logs

```console
docker ps
```

- copy ur container id

```console
docker logs -f <your container ID>
```
