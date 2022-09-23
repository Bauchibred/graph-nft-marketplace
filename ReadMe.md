# Graph NFT Marketplace FCC

_Be sure to double check if Rinkeby or Goerli is best for learning as Rinkeby is getting sunset_

# Quickstart

1. Install Subgraph CLI

```
yarn global add @graphprotocol/graph-cli
```

2. Log into [the graph UI](https://thegraph.com/studio/subgraph) and create a new Subgraph.

Use Goerli as the network.

3. Initialize Subgraph

```
graph init --studio nft-marketplace
```

4. Authenticate CLI

```
graph auth  --studio YOUR_DEPLOY_KEY_HERE
```

5. Update your `subgraph.yaml`

- Update the `address` with your NftMarketplace Address
- Update the `startBlock` with the block right before your contract was deployed

6. Build graph locally

```
graph codegen && graph build
```

- `graph codegen`: Generates code in the `generated` folder based on your `schema.graphql`
- `graph build`: Generates the build that will be uploaded to the graph

7. Deploy subgraph

Replace `VERSION_NUMBER_HERE` with a version number like `0.0.1`.

```
graph deploy --studio nft-marketplace -l VERSION_NUMBER_HERE
```

8. View your UI

Back in your hardhat project, mint and list an NFT with:

```
yarn hardhat run scripts/mint-and-list-item.js --network goerli
```

After yarn adding the CLI using yarn global add @graphprotocol/graph-cli
we then init our graph using graph init --studio nft-marketplace
And then fill in the necessary details
../NftmarketPlace-moralis/constants/NftMaretPlace.json ../NftmarketPlace-moralis/constants
To get through this we would have to learn a little bit of typescript to go through this session, the schema is similar to graphql which is a query language for our api
subgraph.yaml tells our subgraph how to use all our files
Install the graphql extension

We are going to query on our Active item, we need Id! , buyer, seller, nftaddress, tokenId, and a price
Then after producing all these information we are done with our schema.graphql file.
Then we move forward to the contract.ts as this is the file that tells our subgraph how to actually store all the event information that we have
graph codegen helps us write typescript, any time we update schema we have to run graph codegen
Little note for or contracts.ts:

- Each item needs a unique ID that we have to create
  -we have to save any event to our graph
  -update our actuveItem
  In typeScript we have to define the type of our params e.g tokenId: BigInt and add what it returns
  So we have to create an iteemnought object for our itembought event, in type script these are 2 different types and we hahve to make the necessary imports of events then make the object, and we update our new buyer whenever someone makes a new purchase, for itemlisted if item exists already and we are updating we dont create a new item otherwise we do.
  Lastly for itemcanceled it's similar to our itembought we get the id using the same methodology we've been using, we give the canceled item an owner of as the deadAddress that way we know when an item is canceled or sold cause if it was sold we'd have a real owner as the owner address.
  So now we justt have to edit our subgraph.yaml to start reading right before our contract was deployed, so to do this we get our affress and get the block number the contract was deployed and we can use this as our starting block (value - 1)
  Deploying our subgraph
  so we authenticate
  graph auth --studio 15d66204493ae75e6610162ff6a25fe9
  run graph codegen, then we
  graph build
  this creates a sudo file that we push to he graph studio, after this we can then deploy with
  graph deploy --studio nft-marketplace
  then we have the link to our subgraph on our ipfs, and if we refresh our page on the graph platform we can see that it's now listening and syncing for events, so if we mint and list from the backend we can get it on the graph,
  reading from the graph so now we can now go to our index.js to get it to start reading form the graph and not the moralis server in our next app we crreate it on the graphexample.js under our pages/api
  we use apollo so we need to add it using
  yarn add @apollo/client
  and also we need to add the graphql
  and apollo client is what we use to make queries to our graphql
  then we add the graphql to our file and query our file then we go to our app.js whwere we are wrapping everything with moralis and we need to wrap it also in apollo and we intialise using apollo so we have to import from @apollo/client
  We define our client
