# Cobra node

## Local Development

Follow these steps to prepare a local Substrate development environment :hammer_and_wrench:

### Simple Setup

Install all the required dependencies with a single command (be patient, this can take up to 30
minutes).

```bash
curl https://getsubstrate.io -sSf | bash -s -- --fast
```

### Manual Setup

Find manual setup instructions at the
[Substrate Developer Hub](https://substrate.dev/docs/en/knowledgebase/getting-started/#manual-installation).

### Build

Once the development environment is set up, build the node. This command will build the
[Wasm](https://substrate.dev/docs/en/knowledgebase/advanced/executor#wasm-execution) and
[native](https://substrate.dev/docs/en/knowledgebase/advanced/executor#native-execution) code:

```bash
cargo build --release
```

## Run

### Rococo local testnet

Relay chain repository (polkadot) has to be built in `../polkadot`
Uses `polkadot-launch` utility that has to installed from latest sources

```
git clone https://github.com/paritytech/polkadot-launch.git
cd polkadot-launch
yarn
yarn build
chmod +x dist/index.js
npm link
```

Starts local testnet with 4 relay chain validators and Basilisk as parachain

```
cd rococo-local
polkadot-launch config.json
```

Observe Basilisk logs

```
multitail 99*.log
```

### Interaction with the node

Go to the Polkadot apps at https://dotapps.io

Then open settings screen -> developer and paste

*NOTE - FixedU128 type is not yet implemented for polkadot apps. Balance is a measure so price can be reasonably selected. If using polkadot apps to create pool:*
- 1 Mega Units equals 1:1 price
- 20 Mega Units equals 20:1 price
- 50 Kilo Units equals 0.05:1 price

```
{
  "Amount": "i128",
  "AmountOf": "Amount",
  "Address": "AccountId",
  "BalanceInfo": {
    "amount": "Balance",
    "assetId": "AssetId"
  },
  "CurrencyId": "AssetId",
  "CurrencyIdOf": "AssetId",
  "Intention": {
    "who": "AccountId",
    "asset_sell": "AssetId",
    "asset_buy": "AssetId",
    "amount": "Balance",
    "discount": "bool",
    "sell_or_buy": "IntentionType"
  },
  "IntentionId": "u128",
  "IntentionType": {
    "_enum": [
      "SELL",
      "BUY"
    ]
  },
  "LookupSource": "AccountId",
  "Price": "Balance"
}
```

Connect to the `wss://basilisk.hydradx.io:9944` or local node.

