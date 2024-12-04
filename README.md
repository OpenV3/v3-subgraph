# Uniswap V3 Subgraph

### Subgraph Endpoint

Synced at: https://thegraph.com/hosted-service/subgraph/ianlapham/uniswap-v3-subgraph?selected=playground

Pending Changes at same URL

### Running Unit Tests

1. Install [Docker](https://docs.docker.com/get-docker/) if you don't have it already
2. Install postgres: `brew install postgresql`
3. `yarn run build:docker`
4. `yarn run test`

### Adding New Chains

1. Create a new subgraph config in `src/utils/chains.ts`. This will require adding a new `<NETWORK_NAME>_NETWORK_NAME` const for the corresponding network.
2. Add a new entry in `networks.json` for the new chain. The network name should be derived from the CLI Name in The Graph's [supported networks documenation](https://thegraph.com/docs/en/developing/supported-networks/). The factory address can be derived from Uniswap's [deployments documentation](https://docs.uniswap.org/contracts/v3/reference/deployments/ethereum-deployments).
3. To deploy to Alchemy, run the following command:

```
yarn run deploy:alchemy --
  <SUBGRAPH_NAME>
  --version-label <VERSION_LABEL>
  --deploy-key <DEPLOYMENT_KEY>
  --network <NETWORK_NAME>
```

## GoldSky Graph Deployment

```shell
# since goldsky does not work with the networks.json file like the graph cli we can do the following

# as before make sure deps are installed
yarn install

# to overwrite the subgraph.yaml with the network config
npx mustache config/<network-name>.json subgraph.template.yaml > subgraph.yaml

# you can then normally codgen and build
yarn codegen
yarn buildonly

# specific to GoldSky:

# deploy subgraph to GoldSky
goldsky subgraph deploy <subgraph-name>/<version> --path .
## for example:
goldsky subgraph deploy open-v3/1.0.0 --path .

## create a tag for a subgraph
goldsky subgraph tag create <subgraph-name>/<version> --tag <tag-string>
## for example:
goldsky subgraph tag create open-v3/1.0.0 --tag prod

```


