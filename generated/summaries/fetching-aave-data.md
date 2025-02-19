## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## Fetch and Show AAVE Data
 
 **Introduction**        
* AAVE is a DeFi protocol that facilitates the lending and borrowing of cryptocurrency tokens using diverse algorithms and smart contracts without centralized intermediaries. 
* It is a non-custodial liquidity protocol that allows users to participate as lenders or borrowers. Depositors provide liquidity to the market to earn a passive income, while borrowers are able to borrow in an over-collateralized manner.
* Aave's GraphQL data layer is a great resource for developers, allowing developers to access data that may not have been available otherwise. This way developers can work with more data and create more advanced applications. 
* Just like any decentralized blockchain application, Aave's data can be classified into three types: 
  - **Real-time data or current information** - This includes the current state and the new events. With real-time data, you can use data visualisations that reflect changes as they occur in real-time. This means that dashboards are interactive and accurate at any given moment.
  - **Historical** - This includes past state and events. With historical data, you can get a snapshot of information displayed in a chart.

* There are multiple use cases of this data provided by Aave and varied applications (including read-only as well as read/write applications) can be built on top of it and we can examine this data to gain insights on how to update and continue to improve the application.

* The focus of this chapter will be to use Aave's data and show it on the UI in a couple of use cases. 
  - Creating a pie graph to review the Aave treasury in USDT 
  - Implementing a time series graph of how the holdings of different pools have changed over time.

* **Importance of Analytics**
  - Make informed decisions
  - Improve efficiency
  - Identify frauds
  - Improve protocol governance
  - Accelerate through uncertainty
  - Tackle bugs and problems
  - Transform raw data into more valuable information

* Aave's data can be queried in the form of REST or GraphQL. Aave uses “The Graph” to index its data and anyone can query the subgraphs to get access to this information.
 
 **Realtime GraphQL Data**        
#### The Graph and GraphQL
* The Graph is a decentralized protocol for indexing and querying data from Ethereum-based blockchains. That is, obtaining specific data from the blockchain is a more convenient approach while adhering to the web3 ethos and benefiting from decentralization and stability.

* The underlying query language used in The Graph is GraphQL. What is the distinction between RESTFUL API calls and GraphQL calls? Traditional APIs, on the other hand, require developers to define unique endpoints for users that return specified data. If the user requires further information, they may need to make repeated API calls, potentially hundreds of API calls, to obtain it. As long as the developer has established a flexible schema, The Graph (which uses GraphQL) just requires one call to a subgraph.
* See this [GraphQL primer](https://medium.com/graphprotocol/graphql-will-power-the-decentralized-web-d7443a69c69a) for additional information on The Graph and the underlying GraphQL.

#### Source of Aave Subgraphs
* To view the source of the subgraphs, see our [Github repo](https://github.com/aave/protocol-v2-subgraph).

Production Network: [Polygon](https://thegraph.com/hosted-service/subgraph/aave/protocol-v3-polygon)

#### How to Make Use of the Playground

* If you use your browser to navigate to the above playground links, you will be directed to The Graph's playground, where you can simply write and test GraphQL queries.
* Select the purple play button to run your query.
* In the middle column, the query results will be returned.
* Use the 'Schema' column on the right to see what data is available, which may be investigated to discover the underlying data.
* You can also type in the left column and use the auto-complete feature to identify the appropriate query/types.

#### Points to keep in mind
* All address values (for example, when used for id) must be in lowercase.
* In lowercase, the ID of reserves is the asset's address and the address of the market's LendingPoolAddressProvider.
* When utilizing the raw endpoints, the numeric number queried will be returned in either wei units (i.e. 10^18), the decimals of the asset itself (i.e. 10^6 for USDC), or ray units (i.e. 10^27).
* By default, each 'page' of results returns 100 entries. This is expandable to a maximum of 1000 entries per page.
* To list the following 1000 entries, for example, put something like: (skip:1000, first: 1000) to your query's arguments.
* This is also true for nested entries, such as arrays.

* This Graph endpoint contains only static data. To obtain a user's most recent balance (including interest earned up to that moment), you must either compute it yourself or make a balanceOf() call to the aToken contract.

| Return Data Type           | Subgraph Address                                                       |
| -------------------------- | ---------------------------------------------------------------------- | 
| Mainnet                    | https://thegraph.com/explorer/subgraph/aave/aave-v2-matic              |
| Görli (Goerli) Testnet     | https://thegraph.com/hosted-service/subgraph/aave/protocol-v3-goerli   |

* Goerli is an Ethereum test network that allows blockchain development testing prior to deployment on the main Ethereum network, Mainnet. Görli (Goerli) Testnet is the first proof-of-authority cross-client testnet, synching Parity Ethereum, Geth, Nethermind, Hyperledger Besu (formerly Pantheon), and EthereumJS. This testnet is a community-based project, completely open-source, naturally. It was born in September 2018 during ETHBerlin and has been growing in contributors ever since.

#### Using your app to access GraphQL data

* The preferred method is to utilize a client library that can handle the 'plumbing' to ensure you have up-to-date data (with caching sometimes included).  Apollo is used internally, but there are several choices depending on your programming language; read the official GraphQL page for more information.
* If you are unable to utilize a client library (for example, while querying using Postman), you can send a POST request to our subgraph's HTTP endpoint with the header: "Content-Type: application/json" and the body comprising of your query on one line in quotations. As an example:
```
{"query": "{ reserves (where: {usageAsCollateralEnabled: true})  { id name price {id} liquidityRate variableBorrowRate stableBorrowRate}}" }
```
 
 **Querying Aave's GraphQL database using React and implementing a Pie chart**        
* **Initial Setup**
  First, we create a React project, you can refer [this](https://create-react-app.dev/docs/getting-started/) documentation.
  Run npm start to check if the project runs fine.

* **Integrate ApolloClient**
  Then we integrate the Apollo client library. We can install and setup the client using [this](https://www.apollographql.com/docs/react/get-started/) documentation.
  We can use the sample code to fetch the data and test our setup.

* **Initialize the ApolloClient**
  With our dependencies already set up, we can now create an ApolloClient instance.
  We start by importing the symbols we require from @apollo/client into index.js.
  Next, we initialize ApolloClient by handing it a configuration object including the uri and cache fields.

* **Connect the client to React**
  We can connect Apollo Client to React with the ApolloProvider component. Similar to React's Context.Provider, ApolloProvider wraps our React app and places Apollo Client on the context, enabling us to access it from anywhere in our component tree.
  In index.js, we wrap our React app with an ApolloProvider.

* **Fetching data with useQuery**
  After the ApolloProvider is hooked up, we can start requesting data with useQuery. The useQuery hook is a React hook that shares GraphQL data with your UI.
  We can define the query we want to execute by wrapping it in the gql template literal.
  Next, we define a component named DisplayGraphs that executes our GET_QUERY query with the useQuery hook:

* **Implementing the Pie Chart**
  Now, our aim is to create a pie chart using the data we receive. So now we use [react-chartjs-2](https://react-chartjs-2.js.org/). We will import it in our App.js.
  Then we initialize our code to get a Pie chart. Finally we will add the code to get our Pie chart.

* This will give us a Pie chart in our React app.
* You can get the complete code [here](https://github.com/DoDAO-io/aava-analytics-sample-app).
 
 **Historical Rest Data**        
* Now we will use the [Aave Protocol API](https://aave-api-v2.aave.com/) to create a time series graph.
* We will use the same react application to create the time series graph too, so if you still haven't create a react app by following the previous steps.
* Since the the [Aave Protocol API](https://aave-api-v2.aave.com/) is for v2 mainnet so now we need to query the Aave v2 mainnet subgraph.
* We need to make the fetch requests from https://aave-api-v2.aave.com/#/data/get_data_rates_history to get the time series data for any Aave reserve. 
* If you visit the above link, you can see that we require a reserveID to fetch the data (there is a sample reserveID already provided in case you want to try it out). So to get this reserveID, we will query the Aave v2 mainnet subgraph (https://thegraph.com/hosted-service/subgraph/aave/protocol-v2 ). We have already queried the reserveIDs for ChainLink Token (0x514910771af9ca656af840dff83e8264ecf986ca0xb53c1a33016b2dc2ff3653530bff1848a515c8c5) and TrueUSD (0x0000000000085d4780b73119b644ae5ecd22b3760xb53c1a33016b2dc2ff3653530bff1848a515c8c5) which we will be using to plot the graph. 
* We query an array of objects which contains the pools with the reserves id, name and symbol.
* Also, in the GET request we need to provide the start date (from) and time interval (resolutionInHours) to fetch the data. You can use [this](https://www.epochconverter.com/) UNIX timestamp convertor to change the date.
* So now you can visit the aave protocol api and playaround with different reserveID, from and resolutionInHours.
* Now, we visit our App.js and add some changes to code to get our desired graph and add some import statements as we need to use Line Chart this time to represent the time series data.
* Now, we need to fetch the get requests so for that we will use the useEffect hook from React and store the data using useState hook. So add the following code to your DisplayGraphs functions.
* The Get request also returns some unwanted data and the timestamp is in a format which we don't like much, so we update it.
* Finally, we create the Line chart.
* You can get the complete code [here](https://github.com/DoDAO-io/aava-analytics-sample-app). 
 
 
