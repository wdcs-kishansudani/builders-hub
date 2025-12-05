# Avalanche Cheatsheet

This cheatsheet provides a quick reference for common commands and configuration snippets.

## Avalanche-CLI

| Command | Description |
| --- | --- |
| `avalanche network start` | Start a local testnet |
| `avalanche network stop` | Stop a local testnet |
| `avalanche network status` | Get the status of a local testnet |
| `avalanche key create <keyName>` | Create a new key |
| `avalanche key list` | List the keys in your wallet |
| `avalanche subnet create <subnetName>` | Create a new Subnet |
| `avalanche subnet deploy <subnetName>` | Deploy a Subnet |
| `avalanche subnet addValidator <subnetName>` | Add a validator to a Subnet |

## AvalancheGo

| Command | Description |
| --- | --- |
| `/home/ubuntu/.avalanchego/build/avalanchego` | Start an AvalancheGo node |

## RPC

| Method | Description |
| --- | --- |
| `eth_blockNumber` | Get the latest block number on the C-Chain |
| `avm.getBalance` | Get the balance of an address on the X-Chain |
| `platform.getCurrentValidators` | Get the current validators on the P-Chain |

## Configuration Snippets

### Hardhat

```javascript
// hardhat.config.js
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();

module.exports = {
    solidity: "0.8.0",
    networks: {
        local: {
            url: "http://127.0.0.1:9650/ext/bc/C/rpc",
            accounts: [process.env.PRIVATE_KEY]
        }
    }
};
```

### GitHub Actions

```yaml
# .github/workflows/main.yml
name: CI/CD
on:
    push:
        branches:
            - main
jobs:
    build:
        runs-on: ubuntu-latest
        steps:
            - uses: actions/checkout@v2
            - name: Run tests
              run: |
                # Run your tests here
            - name: Deploy to staging
              run: |
                # Deploy to your staging environment here
```
