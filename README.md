# wallet-mnemonic
wallet Mnemonic library

# install

   ```ts
   npm install @satwallet/wallet-mnemonic 

   or

   yarn add @satwallet/wallet-mnemonic

   ```

# use-age

generate mnemonic 

```ts
import {RGN,generateMnemonics} from "@satwallet/wallet-mnemonic"

// RGN random bip39, default 12 words
let mnemonics = generateMnemonics(RGN)
console.log(mnemonics)
// input fit age retreat ship problem warm cargo census genre trash exact

// generate 24 words
let mnemonic1 = generateMnemonics(RGN,256)
console.log(mnemonic1)

```
 
 generate seed use mnemonic

 ```ts
 import {generateMnemonicsToSeedSync} from "@satwallet/wallet-mnemonic"

 let mnemonic = "input fit age retreat ship problem warm cargo census genre trash exact"

 let seed = generateMnemonicsToSeedSync(mnemonics,password)
console.log(seed)
```

generate eth address

```ts
let mnemonic ="input fit age retreat ship problem warm cargo census genre trash exact"
// eth
let path: string = `m/44'/60'/0'/0/0`

async function generateEthAddress(){
    let seed = generateMnemonicsToSeedSync(mnemonic,"")
    const privatekey = await generatePrivateKey(seed,path)
    const pair =  generateKeyPair(privatekey)
    console.log(pair.getPrivate().toString("hex"))
    const Key = getKey(privatekey)
    console.log("privatekey",Key.privateKey)
   
    
    let EthAddress=getEthAddress(new Uint8Array(Key.pubKey))
    const hex = Buffer.from(EthAddress).toString("hex");
    console.log("0x"+hex)
}
```

generate cosmos address

```ts
async function generateComos(){

    let seed = generateMnemonicsToSeedSync(mnemonic)
    const privatekey = await generatePrivateKey(seed)

    const Key = getKey(privatekey)
    let prefix ="cosmos"
    let address = getCosmosAddress(Buffer.from(Key.pubKey))

    let bech32 = toBech32(address,prefix)
    console.log("cosmos......")
    console.log(bech32)
  
    let bech321 = toBech32(address,"osmo")
    console.log("osmo......")
    console.log(bech321)
   
    let bech322 = toBech32(address,"akash")
    console.log("akash......")
    console.log(bech322)
}
```
generate btc address

```ts
async function generateBtcAddress(){
    let mnemonic = "run concert lake also suffer oppose mind order liberty order glory album"
    
    const address = getBtcAddress(mnemonic,AddressType.P2PKH,"m/44'/0'/0'/0",NetworkType.TESTNET,"",0)
    
    console.log(address)
    
}
```