### How To Interact


The following are some sample tests on how to use the smart contract. A lot of checking has been done everywhere to make sure that only the authorised users can execute key functions.


You need to have [NodeJS](https://nodejs.org/en/download/package-manager/) and [Truffle](https://www.trufflesuite.com/docs/truffle/getting-started/installation) installed. Instructions are present in the links attached.

#### Required Packages

On the terminal, type
```bash
npm install package.json
```
#### Steps to Run

On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await FantasySports.deployed();
```
After creating the instance, you can interact with the smart contract by calling the available functions.

#### Test 1

On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await FantasySports.deployed();
instance.startGame(2, 1, 50);
instance.addPlayerToGame("Player1");
instance.addPlayerToGame("Player2");
instance.addPlayerToGame("Player3");
instance.addPlayerToGame("Player4");
instance.playersAddedToGame();
instance.addFantasyTeam("Team1", {from: accounts[0]});
instance.addFantasyTeam("Team2", {from: accounts[1]});
instance.addPlayerToFantasyTeam(0, {from: accounts[0]});
instance.addPlayerToFantasyTeam(1, {from: accounts[0]});
instance.addPlayerToFantasyTeam(2, {from: accounts[1]});
instance.addPlayerToFantasyTeam(3, {from: accounts[1]});
instance.setCaptains(0, 1, {from: accounts[0]});
instance.setCaptains(2, 3, {from: accounts[1]});
instance.bid({from: accounts[0], value: 10000000000000000000});
instance.bid({from: accounts[1], value: 10000000000000000000});
instance.gameBegins();
instance.setplayerStats(0, 10, 20);
instance.setplayerStats(1, 1, 2);
instance.setplayerStats(2, 1, 2);
instance.setplayerStats(3, 1, 2);
instance.gameStops();
instance.calculateTeamsScore();
web3.eth.getBalance(accounts[0]);
web3.eth.getBalance(accounts[1]);
```

This is a very simple test to check if the basic add and view operations work and one can observe that correct reward amount is bieng transferred to the owners.


#### Test 2

On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await FantasySports.deployed();
instance.startGame(2, 1, 50);
instance.addPlayerToGame("Player1");
instance.addPlayerToGame("Player2");
instance.addPlayerToGame("Player3");
instance.addPlayerToGame("Player4");
instance.playersAddedToGame();
instance.addFantasyTeam("Team1", {from: accounts[0]});
instance.addFantasyTeam("Team2", {from: accounts[1]});
instance.addPlayerToFantasyTeam(0, {from: accounts[0]});
instance.addPlayerToFantasyTeam(1, {from: accounts[0]});
instance.addPlayerToFantasyTeam(2, {from: accounts[1]});
instance.addPlayerToFantasyTeam(3, {from: accounts[1]});
instance.setCaptains(0, 1, {from: accounts[0]});
instance.setCaptains(2, 3, {from: accounts[1]});
instance.bid({from: accounts[0], value: 10000000000000000000});
instance.bid({from: accounts[1], value: 10000000000000000000});
instance.gameBegins();
instance.setplayerStats(0, 0, 0);
instance.setplayerStats(1, 0, 0);
instance.setplayerStats(2, 0, 0);
instance.setplayerStats(3, 0, 0);
instance.gameStops();
instance.calculateTeamsScore();
web3.eth.getBalance(accounts[0]);
web3.eth.getBalance(accounts[1]);
```

This is a test case where all the fantasy teams score 0 points. In such a case all the owners will be returned their bids. 


#### Test 3

On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await FantasySports.deployed();
instance.startGame(2, 1, 50);
instance.addPlayerToGame("Player1");
instance.addPlayerToGame("Player2");
instance.addPlayerToGame("Player3");
instance.addPlayerToGame("Player4");
instance.playersAddedToGame();
instance.addFantasyTeam("Team1", {from: accounts[0]});
instance.addFantasyTeam("Team2", {from: accounts[1]});
instance.addPlayerToFantasyTeam(0, {from: accounts[0]});
instance.bid({from: accounts[0], value: 10000000000000000000});

```

In this testcase ann error will be thrown as the owner of Team1 can not bid as the team is still incomplete.




#### Test 4

On the terminal, type
```bash
truffle develop
```

In the truffle console,
```javascript
deploy
let instance = await FantasySports.deployed();
instance.startGame(2, 1, 50);
instance.addPlayerToGame("Player1");
instance.addPlayerToGame("Player2");
instance.addPlayerToGame("Player3");
instance.addPlayerToGame("Player4");
instance.playersAddedToGame();
instance.addFantasyTeam("Team1", {from: accounts[0]});
instance.addFantasyTeam("Team2", {from: accounts[0]});
```


Again in this testcase an error will be thrown as one owner ofcan not own 2 teams.


<hr/>

### Team 1
- Manish (2018101073)
- Akshat Goyal (2018101075)
- Tanish Lad (2018114005)

