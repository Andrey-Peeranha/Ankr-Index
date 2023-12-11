# Fetch the list of cryptocurrencies launched on a particular Blockchain using Ankr’s Token API
## How to Query Cryptocurrencies by Chain using Advanced Token API

In this tutorial, we’ll be fetching the list of cryptocurrencies launched on a particular Blockchain using [Ankr's Advanced Multichain Token API](https://www.ankr.com/advanced-api/)

# Refresher on Ankr Advanced APIs
Ankr's Advanced Multichain APIs are the collection of RPC methods created to simplify querying blockchain data. These APIs do all the heavy lifting for us so that we can query on-chain data in a matter of seconds.
Currently, it supports eight EVM-compatible chains: Ethereum, Fantom, Binance Smart Chain, Polygon, Avalanche, Arbitrum, with more EVM and non-EVM chains coming soon. To interact with Ankr's Advanced APIs, we are going to use a JavaScript library named [Ankr.js](https://www.npmjs.com/package/@ankr.com/ankr.js)

# Getting Started
Prerequisite: To successfully finish this guide, you'll need Node.js↗ and Yarn↗ installed on your machine.

## Step 1: Setting Up Next.js Starter Application
First up, navigate into the directory of your choice where you want to initiate this project and run the following command in your terminal to set up a new Next.js starter page:

yarn create next-app --ts ankrjs-cryptolist
You'll be able to see a couple of files and folders being created for you. Let's dive into the newly created directory and start the development server on localhost:3000.

cd ankrjs-cryptolist

yarn dev
Visit localhost:3000 to view the starter application 


## Step 2: Installing and Setting Up Ankr.js
In this section, we will install and set up Ankr.js for querying crypto tokens by blockchain.

We will start by installing the ankr.js package from npm:

yarn add @ankr.com/ankr.js
Now that we have installed the Ankr.js library, let's set up Ankr.js by creating a new file named apis.ts at the root of your project directory. We will initialize Ankr.js in this file.

File: ./apis.ts

Explain
import AnkrscanProvider from '@ankr.com/ankr.js';
import type { Blockchain } from '@ankr.com/ankr.js/dist/types';

const provider = new AnkrscanProvider('');
To interact with Ankr's Advanced APIs, we have created a provider instance that will serve as an interface to the APIs required to fetch data.

## Step 3: Create Function to Fetch Cryptocurrencies
In this step, we will first create a getCurrencies function in the ./apis.ts file, which will accept the blockchain, and return us the list of cryptocurrencies and the respective details about each token. Here we are going to use the getCurrencies↗ method provided by Ankr.js.

File: ./apis.ts

Explain
import AnkrscanProvider from '@ankr.com/ankr.js';
import type { Blockchain } from '@ankr.com/ankr.js/dist/types';

const provider = new AnkrscanProvider('');

//defining the list of supported blockchains
const listOfChains: Blockchain[] = ['eth', 'arbitrum', 'avalanche', 
'bsc', 'fantom', 'polygon', 'syscoin', 'optimism',];

//key-value pair mapping of chains to their native symbols
export const chainsToNativeSymbols: { [key in Blockchain]: string } = {
  eth: 'ETH',
  arbitrum: 'ETH',
  avalanche: 'AVAX',
  bsc: 'BNB',
  fantom: 'FTM',
  polygon: 'MATIC',
  syscoin: 'SYS',
  optimism: 'Opt',
};

//getCurrencies function
export const getCurrencies = async (

  blockchain: Blockchain
) => {
  return provider.getCurrencies({

    blockchain,
  });
};
Let's call this function on our page i.e. ./pages/index.tsx to check the list. To do so, clear the code from the index.tsx file and replace it with the one given below:

File: ./pages/index.tsx



Explain
import { useEffect } from 'react';

import {
  getCurrencies,
} from '../apis';

function App() {

  useEffect(() => {
    (async () => {
      const  total  = await getCurrencies(
        "eth"
      );
      console.log({ total });
    })();
  }, []);

  return (
    <div className='p-10 flex flex-col items-center'>
      <h1 className='text-3xl font-bold'>Cryptolist</h1>
    </div>
  );
}

export default App;
Now, let's see the fetched list of cryptocurrencies of an inputted blockchain in the developer console of a browser.

Head over to your localhost and use Option + ⌘ + J (on macOS), or Shift + CTRL + J (on Windows/Linux).
You should be able to see the list of cryptocurrencies with their contract addresses, name, symbol and thumbnail.
