# Secret Pulsar Testnet
### Chain ID
`pulsar-2`

## Endpoint URLs

### Tendermint RPC
For use with SecretCLI

`https://pulsar-2.api.trivium.network:26657`

### Cosmos LCD / REST
REST API for use with SecretJS 0.17.x

`https://pulsar-2.api.trivium.network:1317`

### Cosmos gRPC-Web
gRPC-Web API for use with SecretJS 1.x.x

`https://pulsar-2.api.trivium.network:9091`


## Configuration Examples

### SecretCLI
```bash
secretcli config node https://pulsar-2.api.trivium.network:26657
secretcli config chain-id pulsar-2
```


### SecretJS 1.x.x
```js
const { SecretNetworkClient } = require('secretjs');

// Query-Only Client
const queryJs = await SecretNetworkClient.create({
  grpcWebUrl: 'https://pulsar-2.api.trivium.network:9091',
  chainId: "pulsar-2",
});

// Client with Keplr Signer
await window.keplr.enable('pulsar-2');
const [{ address: myAddress }] = await keplrOfflineSigner.getAccounts();

const secretJs = await SecretNetworkClient.create({
  grpcWebUrl: 'https://pulsar-2.api.trivium.network:9091',
  chainId: 'pulsar-2',
  wallet: window.getOfflineSignerOnlyAmino('pulsar-2'),
  walletAddress: myAddress,
  encryptionUtils: window.getEnigmaUtils('pulsar-2'),
});
```


### SecretJS 0.17.x
```js
const { CosmWasmClient, SigningCosmWasmClient } = require('secretjs');

// Query-Only Client
const queryJs = new CosmWasmClient('https://pulsar-2.api.trivium.network:1317')

// Client with Keplr Signer
await window.keplr.enable('pulsar-2');
const offlineSigner = window.getOfflineSigner('pulsar-2');
const enigmaUtils = window.getEnigmaUtils('pulsar-2');
const accounts = await offlineSigner.getAccounts();

const secretJS = new SigningCosmWasmClient(
    'https://pulsar-2.api.trivium.network:1317',
    accounts[0].address,
    offlineSigner,
    enigmaUtils
)
```

### Suggest to Keplr Wallet
Keplr wallet can be used with any Cosmos SDK based chain by suggesting the chain to Keplr.  
An example for pulsar-2 is below.  
  
Learn more about Keplr at [https://docs.keplr.app](https://docs.keplr.app)

```js
await window.keplr.experimentalSuggestChain({
    chainId: "pulsar-2",
    chainName: "Secret Pulsar Testnet",
    rpc: "https://pulsar-2.api.trivium.network:26657",
    rest: "https://pulsar-2.api.trivium.network:1317",
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