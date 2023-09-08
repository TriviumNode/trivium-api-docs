# Secret Pulsar Testnet
### Chain ID
`pulsar-3`

## Endpoint URLs

### Tendermint RPC
For use with SecretCLI

`https://pulsar.api.trivium.network:26657`

### Cosmos LCD / REST
REST API for use with SecretJS 1.5+ and 0.17

`https://pulsar.api.trivium.network:1317`

### Cosmos gRPC-Web
gRPC-Web API for use with SecretJS <1.5

`https://pulsar.api.trivium.network:9091`


## Configuration Examples

### SecretCLI
```bash
secretcli config node https://pulsar.api.trivium.network:26657
secretcli config chain-id pulsar-3
```

### SecretJS 1.5+

See https://secretjs.scrt.network


### SecretJS <1.5
```js
const { SecretNetworkClient } = require('secretjs');

// Query-Only Client
const queryJs = await SecretNetworkClient.create({
  grpcWebUrl: 'https://pulsar.api.trivium.network:9091',
  chainId: "pulsar-3",
});

// Client with Keplr Signer
await window.keplr.enable('pulsar-3');
const [{ address: myAddress }] = await keplrOfflineSigner.getAccounts();

const secretJs = await SecretNetworkClient.create({
  grpcWebUrl: 'https://pulsar.api.trivium.network:9091',
  chainId: 'pulsar-3',
  wallet: window.getOfflineSignerOnlyAmino('pulsar-3'),
  walletAddress: myAddress,
  encryptionUtils: window.getEnigmaUtils('pulsar-3'),
});
```


### SecretJS 0.17
```js
const { CosmWasmClient, SigningCosmWasmClient } = require('secretjs');

// Query-Only Client
const queryJs = new CosmWasmClient('https://pulsar.api.trivium.network:1317')

// Client with Keplr Signer
await window.keplr.enable('pulsar-3');
const offlineSigner = window.getOfflineSigner('pulsar-3');
const enigmaUtils = window.getEnigmaUtils('pulsar-3');
const accounts = await offlineSigner.getAccounts();

const secretJS = new SigningCosmWasmClient(
    'https://pulsar.api.trivium.network:1317',
    accounts[0].address,
    offlineSigner,
    enigmaUtils
)
```

### Suggest to Keplr Wallet
Keplr wallet can be used with any Cosmos SDK based chain by suggesting the chain to Keplr.  
An example for pulsar-3 is below.  
  
Learn more about Keplr at [https://docs.keplr.app](https://docs.keplr.app)

```js
await window.keplr.experimentalSuggestChain({
    chainId: "pulsar-3",
    chainName: "Secret Pulsar Testnet",
    rpc: "https://pulsar.api.trivium.network:26657",
    rest: "https://pulsar.api.trivium.network:1317",
    bip44: {
        coinType: 529,
    },
    bech32Config: {
        bech32PrefixAccAddr: "secret",
        bech32PrefixAccPub: "secret" + "pub",
        bech32PrefixValAddr: "secret" + "valoper",
        bech32PrefixValPub: "secret" + "valoperpub",
        bech32PrefixConsAddr: "secret" + "valcons",
        bech32PrefixConsPub: "secret" + "valconspub",
    },
    currencies: [ 
        { 
            coinDenom: "SCRT", 
            coinMinimalDenom: "uscrt", 
            coinDecimals: 6, 
        }, 
    ],
    feeCurrencies: [
        {
            coinDenom: "SCRT",
            coinMinimalDenom: "uscrt",
            coinDecimals: 6,
        },
    ],
    stakeCurrency: {
        coinDenom: "SCRT",
        coinMinimalDenom: "uscrt",
        coinDecimals: 6,
    },
    coinType: 529,
    gasPriceStep: {
        low: 0.1,
        average: 0.25,
        high: 0.3,
    },
});
```