# Secret Network
### Chain ID
`secret-4`

## Endpoint URLs

### Tendermint RPC
For use with SecretCLI

`https://secret-4.api.trivium.network:26657`

### Cosmos LCD / REST
REST API for use with SecretJS 0.17.x

`https://secret-4.api.trivium.network:1317`

### Cosmos gRPC-Web
gRPC-Web API for use with SecretJS 2.x.x

`https://secret-4.api.trivium.network:9091`


## Configuration Examples

### SecretCLI
```bash
secretcli config node https://secret-4.api.trivium.network:26657
secretcli config chain-id secret-4
```


### SecretJS 2.x.x
```js
const { SecretNetworkClient } = require('secretjs');

// Query-Only Client
const queryJs = await SecretNetworkClient.create({
  grpcWebUrl: 'https://secret-4.api.trivium.network:9091',
  chainId: "secret-4",
});

// Client with Keplr Signer
await window.keplr.enable('secret-4');
const [{ address: myAddress }] = await keplrOfflineSigner.getAccounts();

const secretJs = await SecretNetworkClient.create({
  grpcWebUrl: 'https://secret-4.api.trivium.network:9091',
  chainId: 'secret-4',
  wallet: window.getOfflineSignerOnlyAmino('secret-4'),
  walletAddress: myAddress,
  encryptionUtils: window.getEnigmaUtils('secret-4'),
});
```


### SecretJS 0.17.x
```js
const { CosmWasmClient, SigningCosmWasmClient } = require('secretjs');

// Query-Only Client
const queryJs = new CosmWasmClient('https://secret-4.api.trivium.network:1317')

// Client with Keplr Signer
await window.keplr.enable('secret-4');
const offlineSigner = window.getOfflineSigner('secret-4');
const enigmaUtils = window.getEnigmaUtils('secret-4');
const accounts = await offlineSigner.getAccounts();

const secretJS = new SigningCosmWasmClient(
    'https://secret-4.api.trivium.network:1317',
    accounts[0].address,
    offlineSigner,
    enigmaUtils
)
```