# Tests

> The following are some sample tests. A lot of checking has been done everywhere to make sure that only the authorised users can execute key functions

### Test 1

On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await AModernWay.deployed();
instance.viewItems(); // should return an empty string
instance.addNewItem("netflix", "1 netflix screen", 555555, {from: accounts[1]});
instance.viewItems(); // should return the recently added Netflix Screen
```

This is a very simple test to check if the basic add and view operations work.

### Test 2

On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await AModernWay.deployed();
instance.viewItems(); // should return an empty string
instance.addNewItem("netflix", "1 netflix screen", 555555, {from: accounts[1]});
instance.addNewItem("hotstar", "hotstar premium", 11122222, {from: accounts[3]});
instance.addNewItem("prime video", "amazon prime", 456, {from: accounts[6]});
instance.viewItems(); // should return the three items that were added recently
const EthCrypto = await require('eth-crypto');
const identity = await EthCrypto.createIdentity();
instance.buyItem(2, identity.publicKey, {from: accounts[8], value: 456});
const identity2 = await EthCrypto.createIdentity();
instance.buyItem(0, identity2.publicKey, {from: accounts[3], value: 555555});
instance.viewItems(); // should only return the hotstar string which has not been bought by anyone
```

We had 3 items available for sale and two of them have been bought by different buyers.

```javascript
let publicKey = await instance.getPublicKey(2, {from: accounts[6]});
let primeString = "This is Amazon Prime Video";
let encStr = await EthCrypto.encryptWithPublicKey(publicKey, primeString);
let encryptedString = await JSON.stringify(encStr);
instance.deliverItem(2, encryptedString, {from: accounts[6]});
let buyerString = await instance.getItem(2, {from: accounts[8]});
let parsedString = await JSON.parse(buyerString);
let decStr = await EthCrypto.decryptWithPrivateKey(identity.privateKey, parsedString);

decStr
```

decStr will return **'This is Amazon Prime Video'**. This is how we are maintaing secrecy. The seller will encrypt the item string with the buyer's public key and send the encrypted string to the buyer. Then the buyer will decrypt the encrypted string using their private key to get the secret item string back.

> Now let's do the same for the buyer who bought the Netflix Screen!

```javascript
let publicKey2 = await instance.getPublicKey(0, {from: accounts[1]});
let netflixString = "This is Netflix";
let encStr2 = await EthCrypto.encryptWithPublicKey(publicKey2, netflixString);
let encryptedString2 = await JSON.stringify(encStr2);
instance.deliverItem(0, encryptedString2, {from: accounts[1]});
let buyerString2 = await instance.getItem(0, {from: accounts[3]});
let parsedString2 = await JSON.parse(buyerString2);
let decStr2 = await EthCrypto.decryptWithPrivateKey(identity2.privateKey, parsedString2);

decStr2
```

decStr will return **'This is Netflix'**.

> Now let's do some tests where we should get errors!

### Test 3


On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await AModernWay.deployed();
instance.viewItems(); // should return an empty string
instance.addNewItem("netflix", "1 netflix screen", 555555, {from: accounts[1]});
instance.viewItems(); // should return the recently added Netflix Screen
const EthCrypto = await require('eth-crypto');
const identity = await EthCrypto.createIdentity();
instance.buyItem(1, identity.publicKey, {from: accounts[3], value: 555555});
```

Boom, ERROR!!

This is where our require (assert) calls come handy. They checked that there is no item that has id = 1 and hence returned an error!

### Test 4


On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await AModernWay.deployed();
instance.viewItems(); // should return an empty string
instance.addNewItem("netflix", "1 netflix screen", 555555, {from: accounts[1]});
instance.viewItems(); // should return the recently added Netflix Screen
const EthCrypto = await require('eth-crypto');
const identity = await EthCrypto.createIdentity();
instance.buyItem(0, identity.publicKey, {from: accounts[3], value: 555555});
let publicKey = await instance.getPublicKey(0, {from: accounts[1]});
let netflixString = "This is Netflix";
let encStr = await EthCrypto.encryptWithPublicKey(publicKey, netflixString);
let encryptedString = await JSON.stringify(encStr);
instance.deliverItem(0, encryptedString, {from: accounts[5]});
```

Boom, ERROR!!

This is where our modifiers come in handy! They checked that the user that is calling the deliverItem function for item 0 is not the actual seller of that item, and hence it popped up an error.


### Test 5


On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await AModernWay.deployed();
instance.viewItems(); // should return an empty string
instance.addNewItem("netflix", "1 netflix screen", 555555, {from: accounts[1]});
instance.viewItems(); // should return the recently added Netflix Screen
const EthCrypto = await require('eth-crypto');
const identity = await EthCrypto.createIdentity();
instance.buyItem(0, identity.publicKey, {from: accounts[3], value: 111111});
```

Boom, ERROR!!

This is where our require (assert) calls come in handy! They checked that the buyer is not sending money that has been listed as the asking price and hence they will return an error.
