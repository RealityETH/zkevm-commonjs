# Additional test information

## Steps to build the `e2e` tests
- Go to [contracts repository](https://github.com/RealityETH/subjectivocracy) and perform a deployment. One of the outcomes of the deployment will be a `genesis.json` file
- Copy the `genesis.json` file into the `e2e/state-transition.json` in the `genesis` object property
- Add in the genesis the accounts like this:
```
{
  "balance": "0",
  "nonce": "3",
  "address": "0xc949254d682d8c9ad5682521675b8f43b102aec4",
  "pvtKey": "0xdfd01798f92667dbf91df722434e8fbe96af0211d4d1b82bbbbc8f1def7a814f"
}
```
( To interact with the bridge:
- Check `PolygonZkEVMBridge proxy` smart contract address in the `genesis` and copy it into each transaction. Therefore, `to` value in each transaction must match `PolygonZkEVMBridge proxy` address)
- Use this genesis to create manually the state-transition.json file by providing genesis informaiton and txs for the transactions of the first batch, and txs2 with the transactions for the second batch.
- All other data, like stateRoots will be re-calculated and updates by running the scripts in the processor-forking.test.js.
- We create two batches, since the aggregator proofs needs two inputs according to my current understanding.


## Notes
- `contractName` string under genesis property in `state-transition.json` is taken in order to load ABI interface to interact with contracts afterwards
- if a proxy is used, `contractName` should have the following pattern as a name: `${contractName} ${proxy}`
  - ABI `${contractName}` will be loaded then