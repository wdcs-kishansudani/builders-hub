# 5-Minute Quickstart Guide

This guide provides a fast path to getting an Avalanche development environment running. In about 5 minutes, you will install the necessary tools, run a local node, send a transaction, and create your first Subnet.

## Prerequisites

*   **Operating System:** Ubuntu 22.04 LTS (or other Linux distro with `glibc >= 2.31`)
*   **Dependencies:** `curl`, `git`
*   **Node.js:** v18.x or higher

## Environment Setup

Before you begin, ensure you have the required dependencies installed.

```bash
# Update package list
sudo apt-get update

# Install curl and git
sudo apt-get install curl git

# Install Node.js (we recommend using nvm)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
nvm install --lts
nvm use --lts
```

---

## The 5-Minute Checklist

### 1. Install AvalancheGo

AvalancheGo is the official node implementation for Avalanche.

```bash
# Download the latest version of AvalancheGo
wget -nd -m https://api.github.com/repos/ava-labs/avalanchego/releases/latest -O - \
| grep -E 'browser_download_url.*(linux_amd64.tar.gz)$' \
| cut -d \" -f 4 \
| xargs wget -O avalanchego.tar.gz

# Unpack the archive
tar -xvf avalanchego.tar.gz

# Move the binaries to a common location
sudo mv avalanchego-*/avalanchego /usr/local/bin/
```

### 2. Install Avalanche-CLI

The Avalanche-CLI is the easiest way to manage local networks and Subnets.

```bash
npm install -g @avalabs/avalanche-cli
```

### 3. Run a Local Testnet

This command will start a five-node local testnet.

```bash
avalanche network start
```

You can check the status of your local network with:

```bash
avalanche network status
```

### 4. Create a Wallet and Get Funds

The CLI comes with a default funded wallet for local development.

```bash
# Create a new key
avalanche key create mykey

# Get the C-Chain address
avalanche key list
```

**DANGEROUS:** The `avalanche key create` command will output a private key. Store this key securely. Anyone with access to this key can control your assets. There is no way to recover a lost private key.

### 5. Send a Transaction

Let's send some test AVAX on the local C-Chain.

```bash
# Send 1 AVAX from the default wallet to your new wallet
avalanche transaction transfer --from default --to mykey --amount 1 --asset AVAX
```

### 6. Create a Minimal Subnet

Now, let's create a Subnet using the Subnet-EVM.

```bash
# Create a new Subnet configuration file
avalanche subnet create mySubnet --vm Subnet-EVM
```

This will create a `subnets/mySubnet.json` file that defines your Subnet.

### 7. Deploy the Subnet

Finally, deploy your Subnet to the local testnet.

```bash
avalanche subnet deploy mySubnet --network local
```

Congratulations! You have successfully run a local node, sent a transaction, and created your first Subnet.

## Next Steps

You are now ready to dive deeper into the Avalanche ecosystem. Head back to the [Table of Contents](./TOC.md) to continue your learning journey.
