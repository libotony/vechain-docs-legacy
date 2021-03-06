# Setup & Walk Around

Author: A Byte Ahead https://medium.com/@laalaguer/how-to-develop-a-dapp-on-vechain-ii-setup-walk-around-109a01bf7ae9

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/34f7ee7-1_c2uuq00IOapunjTMQN3scw.png",
        "1_c2uuq00IOapunjTMQN3scw.png",
        1600,
        692,
        "#f1f1f3"
      ],
      "caption": "[Sync: Desktop VeChain DApp environment](https://env.vechain.org/)."
    }
  ]
}
[/block]
## **Setup in 3 minutes** 

Great! I see you have survived the last tutorial, now it is time to start programming. The first thing we need is a [Sync](https://env.vechain.org/) environment.

Okay now let’s clone the Sync project source code in a terminal and spin it up in ***dev mode***:
[block:code]
{
  "codes": [
    {
      "code": ">mkdir playgrounds\n>cd playgrounds/\n>git clone https://github.com/vechain/thor-sync.electron\n>cd thor-sync.electron/\n>node -v # Make sure you have node.js >V10.0.0 installed\n>npm install # Install dependencies\n>npm run dev # Boot the Sync in dev mode",
      "language": "text",
      "name": "Sync project source code"
    }
  ]
}
[/block]
When you see the Sync electron window popping up, we are all set!
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0eef449-1_FacLnaprgduDltjvHP4w_w.png",
        "1_FacLnaprgduDltjvHP4w_w.png",
        1600,
        1094,
        "#eeeeee"
      ],
      "caption": "Boot up: npm run dev"
    }
  ]
}
[/block]
## **Poke around: Familiar with Sync** 

Okay, now let us put aside the terminal and focus more on the GUI window. Sync is a browser-like wallet that embedded with Connex.js library which can offer the web page running inside it the ability to communicate with VeChain blockchain.

### Create a Testing Wallet

First, Let us set up a testing wallet for ourselves:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0b2e702-1_vfVH2dlr_32_sno4-0HZLg.jpeg",
        "1_vfVH2dlr_32_sno4-0HZLg.jpeg",
        1600,
        1296,
        "#ececec"
      ],
      "caption": "Go to wallet panel to view existing wallets."
    }
  ]
}
[/block]
Great, now click on the upper-right “**wallets**” icon, if you are on test net, there are already 3 wallets available for testing: “Foo”, “Baz” and “Bar”. Leave them alone, let us click the “**Create**” button to create a fresh one.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9e6c9cf-WeChat_Image_20190322104818.png",
        "WeChat Image_20190322104818.png",
        1805,
        645,
        "#f3f3f3"
      ],
      "caption": "Create a new wallet for our testing"
    }
  ]
}
[/block]
> *You can also import your existing wallet of Ethereum into Sync, as well as using a third party generator to create a wallet, like [VeChain Address Generator](https://laalaguer.github.io/VeChain-Address/) on github.* 

Follow the instructions on Sync now I have a wallet with a public address, it currently contains 0 VET and 0 VTHO: 
> *0xa7a609b928c4eac077d0e5640f3fa650746c4fcf* 

### **Fuel the wallet with VTHO** 

**Next**, we fill up the newly created wallet by adding some VTHO funds to it. VTHO is used as the fee fueling the transactions and on test net. Where to get it? The VeChain core team’s DApp demo: **VET/VTHO faucet**!

Go on, visit the web URL: https://faucet.vecha.in in Sync, and you will see an interesting web page that gives out VTHO on test net for free:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8721f65-WeChat_Image_20190322105508.png",
        "WeChat Image_20190322105508.png",
        1807,
        696,
        "#eae9ea"
      ],
      "caption": "Get free VET/VTHO on test net"
    }
  ]
}
[/block]
Follow the “**Claim Tokens**” button in the middle of the web page and let’s get some free VET/VTHO for testing. Do remember to choose the wallet you created, and input the password accordingly to claim the tokens. I have already claimed 500 VET with 500 VTHO. 😉
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c120b33-1_tMo5kR-BoY9ATD7AEb1XxA.jpeg",
        "1_tMo5kR-BoY9ATD7AEb1XxA.jpeg",
        908,
        864,
        "#deddde"
      ]
    }
  ]
}
[/block]
## **Play with Connex.js APIs** 

Now that we have money on test net, let's move on to explore the blockchain functionalities provided by Sync, the **connex.js** library. Let us **open up a new blank tab**, then toggle the developer tools to see what is connex used for:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bc75f06-WeChat_Image_20190322105751.png",
        "WeChat Image_20190322105751.png",
        1801,
        647,
        "#f2f1f0"
      ],
      "caption": "Open Developer Tools to visit Connex."
    }
  ]
}
[/block]
Once on the console of the developer tools (Just like Chrome developer tools), type in following code:
[block:code]
{
  "codes": [
    {
      "code": "> connex\n {version: \"1.2.0\", thor: {…}, vendor: {…}}\nthor:{ticker: ƒ, account: ƒ, block: ƒ, …}\nvendor:{sign: ƒ, owned: ƒ}\nversion:\"1.2.0\"\n__proto__:Object",
      "language": "text",
      "name": "Connex"
    }
  ]
}
[/block]
Yep, each and every window **has already implanted the connex object** in the web page. And this connex object can do a lot of things with VeChain network, Let us explore some simple ones:

### **Play with account()** 
[block:code]
{
  "codes": [
    {
      "code": "> var acc = connex.thor.account('0xa7a609b928c4eac077d0e5640f3fa650746c4fcf')\n> acc.get().then(info=>{console.log(info)})\nPromise {<pending>}\n{balance: \"0x1b1ae4d6e2ef500000\", energy: \"0x1b1af7398584067000\", hasCode: false}\n> parseInt('0x1b1ae4d6e2ef500000') \n500000000000000000000\n> parseInt('0x1b1af7398584067000')\n500005175000000000000",
      "language": "text"
    }
  ]
}
[/block]
Here I just queried my newly created wallet, which results in a response object of “balance”, “energy” and “hasCode” fields. “balance” is the VET this account holds, and “energy” is the VTHO amount.

### **Play with ticker()** 
In VeChain network, we don’t know exactly ***when*** a new block is produced, but we surely want to be notified when it is produced. `ticker` gives us this peek hole to get notified. We still use the debug console in Sync:
[block:code]
{
  "codes": [
    {
      "code": "> var t = connex.thor.ticker()\nundefined\n> t.next().then(()=>{console.log('new block!')})\nnew block!",
      "language": "text"
    }
  ]
}
[/block]
Cool right? After around 3–10 seconds this “new block!” message is printed and we know there is a new block added to the top of the chain.

> `ticker` is a Promise that is never rejected, so we only need to supply a resolve function. We no longer need `setTimeout` function!

### **Play with call()** 
Actually, the **VTHO contract itself is an [ERC20](https://en.wikipedia.org/wiki/ERC-20)/[VIP180 ](https://github.com/vechain/VIPs/blob/master/VIP-180-EN.md) compatible contract** living on the VeChain! And you know what, I happen to know the address of it on the test net: 😜

> *0x0000000000000000000000000000456e65726779* 

For those who don’t understand ERC20/VIP180, a contract is a long living object on the blockchain. Thinking of it as a set of program instructions and a simple free-form permanent storage that the program controls it. ERC20/VIP180 contracts are simple “virtual bank” program which keeps track on each client and his balance of a specific virtual coin/token.

So, we have the address of a contract, how do we call it? Very simple.
[block:code]
{
  "codes": [
    {
      "code": "> const balanceOfABI = {\n  'constant': true,\n  'inputs': [\n    { \n      'name': '_owner',\n      'type': 'address'\n    }\n  ],    \n  'name': 'balanceOf',\n  'outputs': [\n    { \n     'name': 'balance',\n     'type': 'uint256'\n    }\n  ],\n  'payable': false,\n  'stateMutability': 'view',\n  'type': 'function'\n}\n> const balanceOfMethod = connex.thor.account('0x0000000000000000000000000000456e65726779').method(balanceOfABI)\n> const balanceInfo = await balanceOfMethod.call('0xa7a609b928c4eac077d0e5640f3fa650746c4fcf')\n> console.log(balanceInfo)\n{data: \"0x00000000000000000000000000000000000000000000001b1b428acf29437000\", events: Array(0), transfers: Array(0), gasUsed: 870, reverted: false, …}\n",
      "language": "text"
    }
  ]
}
[/block]
We first supply the contract method ABI (function signature) and then create a handler with the contract deploy address. Finally, we call the contract method with `call()` and supply it with a parameter, an address of the account we are interested. Great! Now we have the result!

## **Summary** 

Enough for today’s study!

To recap, we have:

1. Walked you through the installation of Sync.
2. Run an example DApp in Sync and get some free VET/VTHO.
3. Play with VeChain blockchain with the pre-implanted `connex` javascript object.

Starting from the next tutorial, we will use our knowledge learned today and build a web page (front-end) of ***an existing smart contract***, VTHO contract (Yes, some good guy has done it for us, we simply borrow it). Be ready and let’s go!