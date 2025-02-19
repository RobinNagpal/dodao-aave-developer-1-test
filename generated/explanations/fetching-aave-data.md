## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## Fetch and Show AAVE Data
 
 **Introduction**        
AAVE is a DeFi protocol that facilitates the lending and borrowing of cryptocurrency tokens using diverse algorithms and smart contracts without centralized intermediaries. 
It is a non-custodial liquidity protocol that allows users to participate as lenders or borrowers. Depositors provide liquidity to the market to earn a passive income, while borrowers are able to borrow in an overcollateralized manner.
Aave's GraphQL data layer is a great resource for developers, allowing developers to access data that may not have been available otherwise. This way developers can work with more data and create more advanced applications. 
Just like any decentralized blockchain application, Aave's data can be classified into three types: 
- **Real-time data or current information** - This includes the current state and the new events. With real-time data, you can use data visualisations that reflect changes as they occur in real-time. This means that dashboards are interactive and accurate at any given moment.
- **Historical** - This includes past state and events. With historical data, you can get a snapshot of information displayed in a chart.

As discussed above, there are multiple use cases of this data provided by Aave and varied applications (including read-only as well as read/write applications) can be built on top of it and we can examine this data to gain insights on how to update and continue to improve the application.

The focus of this chapter will be to use Aave's data and show it on the UI in a couple of use cases. 
- Creating a pie graph to review the aave treasury in USDT 
- Implementing a time series graph of how the holdings of different pools have changed over time.

Before moving on to the code, let's have a look at the importance of analytics.

**Importance of Analytics**
- Make informed decisions
- Improve efficiency
- Identify frauds
- Improve protocol governance
- Accelerate through uncertainty
- Tackle bugs and problems
- Transform raw data into more valuable information

Aave's data can be queried in the form of REST or GraphQL. Aave uses “The Graph” to index its data and anyone can query the subgraphs to get access to this information.
 
 **Realtime GraphQL Data**        
#### The Graph and GraphQL
The Graph is a decentralized protocol for indexing and querying data from Ethereum-based blockchains. That is, obtaining specific data from the blockchain is a more convenient approach while adhering to the web3 ethos and benefiting from decentralization and stability.

The underlying query language used in The Graph is GraphQL. What is the distinction between RESTFUL API calls and GraphQL calls? Traditional APIs, on the other hand, require developers to define unique endpoints for users that return specified data. If the user requires further information, they may need to make repeated API calls, potentially hundreds of API calls, to obtain it. As long as the developer has established a flexible schema, The Graph (which uses GraphQL) just requires one call to a subgraph.
See this [GraphQL primer](https://medium.com/graphprotocol/graphql-will-power-the-decentralized-web-d7443a69c69a) for additional information on The Graph and the underlying GraphQL.

#### Source of Aave Subgraphs
To view the source of the subgraphs, see our [Github repo](https://github.com/aave/protocol-v2-subgraph).

Production Network: [Polygon](https://thegraph.com/hosted-service/subgraph/aave/protocol-v3-polygon)

#### How to Make Use of the Playground

- If you use your browser to navigate to the above playground links, you will be directed to The Graph's playground, where you can simply write and test GraphQL queries.
- Select the purple play button to run your query.
- In the middle column, the query results will be returned.
- Use the 'Schema' column on the right to see what data is available, which may be investigated to discover the underlying data.
- You can also type in the left column and use the auto-complete feature to identify the appropriate query/types.

#### Points to keep in mind
- All address values (for example, when used for id) must be in lowercase.
- In lowercase, the ID of reserves is the asset's address and the address of the market's LendingPoolAddressProvider.
- When utilizing the raw endpoints, the numeric number queried will be returned in either wei units (i.e. 10^18), the decimals of the asset itself (i.e. 10^6 for USDC), or ray units (i.e. 10^27).
- By default, each 'page' of results returns 100 entries. This is expandable to a maximum of 1000 entries per page.
- To list the following 1000 entries, for example, put something like: (skip:1000, first: 1000) to your query's arguments.
- This is also true for nested entries, such as arrays.

This Graph endpoint contains only static data. To obtain a user's most recent balance (including interest earned up to that moment), you must either compute it yourself or make a balanceOf() call to the aToken contract.

| Return Data Type           | Subgraph Address                                                       |
| -------------------------- | ---------------------------------------------------------------------- | 
| Mainnet                    | https://thegraph.com/explorer/subgraph/aave/aave-v2-matic              |
| Görli (Goerli) Testnet     | https://thegraph.com/hosted-service/subgraph/aave/protocol-v3-goerli   |

Goerli is an Ethereum test network that allows blockchain development testing prior to deployment on the main Ethereum network, Mainnet. Görli (Goerli) Testnet is the first proof-of-authority cross-client testnet, synching Parity Ethereum, Geth, Nethermind, Hyperledger Besu (formerly Pantheon), and EthereumJS. This testnet is a community-based project, completely open-source, naturally. It was born in September 2018 during ETHBerlin and has been growing in contributors ever since.

#### Using your app to access GraphQL data

The preferred method is to utilize a client library that can handle the 'plumbing' to ensure you have up-to-date data (with caching sometimes included). Apollo is used internally, but there are several choices depending on your programming language; read the official GraphQL page for more information.
If you are unable to utilize a client library (for example, while querying using Postman), you can send a POST request to our subgraph's HTTP endpoint with the header: "Content-Type: application/json" and the body comprising of your query on one line in quotations. As an example:
```
{"query": "{ reserves (where: {usageAsCollateralEnabled: true})  { id name price {id} liquidityRate variableBorrowRate stableBorrowRate}}" }
```

 
 **Historical Rest Data**        
Now we will use the [Aave Protocol API](https://aave-api-v2.aave.com/) to create a time series graph.
We will use the same react application to create the time series graph too, so if you still haven't create a react app by following the previous steps.

Since the the [Aave Protocol API](https://aave-api-v2.aave.com/) is for v2 mainnet so now we need to query the Aave v2 mainnet subgraph.

We need to make the fetch requests from https://aave-api-v2.aave.com/#/data/get_data_rates_history to get the time series data for any Aave reserve. 
If you visit the above link, you can see that we require a reserveID to fetch the data (there is a sample reserveID already provided in case you want to try it out). So to get this reserveID, we will query the Aave v2 mainnet subgraph (https://thegraph.com/hosted-service/subgraph/aave/protocol-v2 ). We have already queried the reserveIDs for ChainLink Token (0x514910771af9ca656af840dff83e8264ecf986ca0xb53c1a33016b2dc2ff3653530bff1848a515c8c5) and TrueUSD (0x0000000000085d4780b73119b644ae5ecd22b3760xb53c1a33016b2dc2ff3653530bff1848a515c8c5) which we will be using to plot the graph. 

If you want to query the reserveID yourself, you can try this:
```graphql
{
  pools {
    reserves {
      id
      name
      symbol
    }
  }
}
```

This query returns us an array of objects which contains the pools with the reserves id, name and symbol.

Also, in the GET request we need to provide the start date (from) and time interval (resolutionInHours) to fetch the data. You can use [this](https://www.epochconverter.com/) UNIX timestamp convertor to change the date.
So now you can visit the aave protocol api and playaround with different reserveID, from and resolutionInHours.

Now, let's visit our App.js and add some changes to code to get our desired graph.

* Let's add some import statements as we need to use Line Chart this time to represent the time series data. So you can update your import statements to the following:
  ```javascript
  import React, {useEffect, useState} from 'react';
  import { useQuery, gql } from '@apollo/client';
  import { Chart as ChartJS, ArcElement, Tooltip, Legend, CategoryScale, LinearScale, PointElement, LineElement, Title, } from 'chart.js';

  import { Pie, Line } from 'react-chartjs-2';
  import './App.css';

  ChartJS.register(ArcElement, 
      CategoryScale,
      LinearScale,
      PointElement,
      LineElement,
      Title,
      Tooltip,
      Legend
  );
  ```

* Now, we need to fetch the get requests so for that we will use the useEffect hook from React and store the data using useState hook. So add the following code to your DisplayGraphs functions:
  ```javascript
  const [linedata1, setLinedata1] = useState([]);
      const [linedata2, setLinedata2] = useState([]);

      useEffect(() => {
          Promise.all([
              fetch('https://aave-api-v2.aave.com/data/rates-history?reserveId=0x514910771af9ca656af840dff83e8264ecf986ca0xb53c1a33016b2dc2ff3653530bff1848a515c8c5&from=1667952000&resolutionInHours=6'),
              fetch('https://aave-api-v2.aave.com/data/rates-history?reserveId=0x0000000000085d4780b73119b644ae5ecd22b3760xb53c1a33016b2dc2ff3653530bff1848a515c8c5&from=1667952000&resolutionInHours=6'),
          ])
          .then(([resData1, resData2]) => 
              Promise.all([resData1.json(), resData2.json()])
          )
          .then(([data1, data2]) => {
              console.log(data1, data2);
              setLinedata1(data1);
              setLinedata2(data2);
          })
          .catch(([err1, err2]) => {
              console.log(err1.message, err2.message);
          });
      }, []);
  ```

  The Get request also returns some unwanted data and the timestamp is in a format which we don't like much, so let's update it:
  ```javascript
  let timestamps = linedata1.map(a => (a.x.year + '/' + a.x.month + '/' + a.x.date + ' ' + a.x.hours + ' hours'));
      let utilization1 = linedata1.map(a => a.utilizationRate_avg);
      let utilization2 = linedata2.map(a => a.utilizationRate_avg);

      timestamps.forEach((element, index) => {
          timestamps[index] = element.toString();
      });
  ```
* Now, let's create the Line chart using the following code:
  ```javascript
  const optionsLineChart = {
          responsive: true,
          plugins: {
            legend: {
              position: 'top',
            },
            title: {
              display: true,
              text: 'Avg Utilization Rate',
            },
          },
      };
        
  const linedata = {
      labels: timestamps,
      datasets: [
        {
          label: 'ChainLink Token',
          data: utilization1,
          borderColor: 'rgb(255, 99, 132)',
          backgroundColor: 'rgba(255, 99, 132, 0.5)',
        },
        {
          label: 'TrueUSD',
          data: utilization2,
          borderColor: 'rgb(53, 162, 235)',
          backgroundColor: 'rgba(53, 162, 235, 0.5)',
        },
      ],
  };

  return (
      <div className="Chart-container">
          <div className="Pie-container">
              <Pie options={optionsPieChart} data={piedata} />
          </div>
          <div className="Line-container">
              <Line options={optionsLineChart} data={linedata} />
          </div> 
      </div>
  );
  ```

This will provide us with the following time series graph:

You can get the complete code [here](https://github.com/DoDAO-io/aava-analytics-sample-app). 
 
 **Graphql Queries**        

#### Examples of Queries

We'll be using the mainnet Big uints GraphQL endpoints in the queries below. These queries can be copied and pasted into the Graph playground links.

##### Reserve Data
If we want to receive a list of all the reserves that can be used as collateral, as well as the interest rates for each reserve, we can use the following query:
```graphql
{
  reserves (where: {
    usageAsCollateralEnabled: true
  }) {
    id
    name
    price {
      id
    }
    liquidityRate
    variableBorrowRate
    stableBorrowRate
  }
}
```

We would utilise the reserves ERC20 token address to retrieve data for a certain reserve. For the Chainlink reserve, for example:

```graphql
{
  reserve(id: "0x514910771af9ca656af840dff83e8264ecf986ca0x24a42fd28c976a61df5d00d0599c34c4f90748c8") { // LINK
    symbol
    price
    aToken {
      id
    }
  }
}
```

If we wish to retrieve historical interest rate data for a specific reserve and paginate through the records, our query may look like this:
```graphql
{
  reserve (id: "0x0000000000085d4780b73119b644ae5ecd22b3760x24a42fd28c976a61df5d00d0599c34c4f90748c8") { // TUSD
    id
    paramsHistory(skip:1000, first: 1000) {
      id
      variableBorrowRate
      utilizationRate
      liquidityRate
      timestamp
    }
  }
}
```

##### User Data
When an address communicates with the Aave Protocol, a UserReserve is generated, with the user ID equal to the user's address plus the reserve's ID (which is the ERC20 token address).
To obtain information on a certain UserReserve:
```graphql
{
  userReserve(id: "USER_ADDRESS_AND_RESERVE_ADDRESS") {
    reserve {
      id
      symbol
    }
    user {
      id
    }
  }
}
```

To retrieve all reserves (i.e. positions) held by a specific user (notice that the user address must be lower case):
```graphql
{
  userReserves(where: { user: "USER_ADDRESS"}) {
    id
    reserve{
      id
      symbol
    }
    user {
      id
    }
  }
}
```

##### Deposit data
To obtain recent deposits for a certain asset:
```graphql
{
  deposits (orderBy: timestamp, orderDirection: desc, where: { 
    reserve: "0xdac17f958d2ee523a2206206994597c13d831ec70x24a42fd28c976a61df5d00d0599c34c4f90748c8" // USDT
  }) {
    id
    amount
    timestamp
  }
}
```

##### Borrow data
To obtain recent borrows for a certain asset:
```graphql
{
  borrows (orderBy: timestamp, orderDirection: desc, where: { 
    reserve: "0xdac17f958d2ee523a2206206994597c13d831ec70x24a42fd28c976a61df5d00d0599c34c4f90748c8" // USDT
  }) {
    id
    amount
    timestamp
  }
}
```

##### Flash loan data
For instance, consider the following query for analysing the five most recent Flash Loans:
```graphql
{ 
  flashLoans( 
    first: 5 
    orderBy: timestamp 
    orderDirection: desc 
  ) { 
    id 
    reserve { 
      id 
      name 
      symbol 
    } 
    amount 
    totalFee 
    timestamp 
  } 
} 
``` 
 **Querying Aave's GraphQL database using React and implementing a Pie chart**        
* **Initial Setup**
  First, let's create a React project, you can refer [this](https://create-react-app.dev/docs/getting-started/) documentation.
  ```
  npx create-react-app aave-analytics-sample-app
  ```
  Run npm start to check if the project runs fine.

* **Integrate ApolloClient**
  Let's integrate the Apollo client library. We can install and setup the client using [this](https://www.apollographql.com/docs/react/get-started/) documentation.
  ```shell
  npm install @apollo/client graphql
  ```
  We can use the sample code to fetch the data and test our setup.

* **Initialize the ApolloClient**
  With our dependencies already set up, we can now create an ApolloClient instance.
  Let's start by importing the symbols we require from @apollo/client into index.js:
  ```javascript
  import { ApolloClient, InMemoryCache, ApolloProvider, gql } from '@apollo/client';
  ```
  Next, we'll initialize ApolloClient by handing it a configuration object including the uri and cache fields:
  ```javascript
  const client = new ApolloClient({
    uri: 'https://api.thegraph.com/subgraphs/name/aave/protocol-v3-goerli',
    cache: new InMemoryCache(),
  });
  ```

* **Connect the client to React**
  We can connect Apollo Client to React with the ApolloProvider component. Similar to React's Context.Provider, ApolloProvider wraps our React app and places Apollo Client on the context, enabling us to access it from anywhere in our component tree.

  In index.js, let's wrap our React app with an ApolloProvider
  ```javascript
  import React from 'react';
  import * as ReactDOM from 'react-dom/client';
  import { ApolloClient, InMemoryCache, ApolloProvider } from '@apollo/client';
  import App from './App';

  const client = new ApolloClient({
    uri: 'https://api.thegraph.com/subgraphs/name/aave/protocol-v3-goerli',
    cache: new InMemoryCache(),
  });

  const root = ReactDOM.createRoot(document.getElementById('root'));

  root.render(
    <ApolloProvider client={client}>
      <App />
    </ApolloProvider>,
  );
  ```

* **Fetching data with useQuery**
  After the ApolloProvider is hooked up, we can start requesting data with useQuery. The useQuery hook is a React hook that shares GraphQL data with your UI.
  Switching over to our App.js file, we'll start by replacing our existing file contents with the code snippet below:
  ```javascript
  import { useQuery, gql } from '@apollo/client';

  export default function App() {
  return (
      <div className="App">
          <h2 className="App-header">AAVE Analytics</h2>
          <br/>
          <DisplayGraphs />
      </div>
  );
  }
  ```
  We can define the query we want to execute by wrapping it in the gql template literal:
  ```graphql
  const GET_QUERY = gql`
  {
      reserves {
          id
          symbol
          name
    
          totalLiquidity
      }
  }
  `;
  ```
  Next, let's define a component named DisplayGraphs that executes our GET_QUERY query with the useQuery hook:
  ```javascript
  function DisplayLocations() {
    const { loading, error, data } = useQuery(GET_QUERY);

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error :(</p>;

    let names = data.reserves.map(a => a.name);
      let total = data.reserves.map(a => a.totalLiquidity);
      let utilization = data.reserves.map(a => a.utilizationRate);

      total.forEach((element, index) => {
          total[index] = element % 10^18;
      });
  ….
  }
  ```

* **Implementing the Pie Chart**
  Now, our aim is to create a pie chart using the data we receive. So now we'll use [react-chartjs-2](https://react-chartjs-2.js.org/).
  ```
  npm install --save chart.js react-chartjs-2
  ```
  Then we will import it in our App.js:
  ```
  import { Pie } from 'react-chartjs-2';
  ```
  Now we need to initialize our code to get a Pie chart:
  ```
  ChartJS.register(ArcElement, Tooltip, Legend);
  ```

* Finally we will add the code to get our Pie chart:
  ```javascript
  const piedata = {
          labels: names,
          datasets: [
            {
              label: 'percentage',
              data: total,
              backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)',
                'rgba(255, 140, 64, 0.2)',
                'rgba(205, 159, 64, 0.2)',
              ],
              borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)',
                'rgba(205, 159, 64, 1)',
                'rgba(255, 149, 64, 1)',
              ],
              borderWidth: 1,
            },
          ],
      };

  const optionsPieChart = {
          responsive: true,
          plugins: {
            legend: {
              position: 'top',
            },
            title: {
              display: true,
              text: 'Total Liquidity',
            },
          },
      };

    return (
          <div className="Chart-container">
              <div className="Pie-container">
                  <Pie options={optionsPieChart} data={piedata} />
              </div>
          </div>
      );
  ```

  This will give us a Pie chart in our React app.

  You can get the complete code [here](https://github.com/DoDAO-io/aava-analytics-sample-app).
 
 
