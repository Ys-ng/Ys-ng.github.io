---
layout: post
title: Geth 설치 및 실행
subtitle: blockchain ethereum
categories: BlockChain
tags: [ethereum, blockchain]
---



##설치
https://myanjini.tistory.com/entry/Geth-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C-%ED%9B%84-%EC%84%A4%EC%B9%98?category=771573


C:\testnet\genesis.json 

```json
{
  "config": {
    "chainId": 15,
    "homesteadBlock": 0,
    "eip155Block": 0,
    "eip158Block": 0, 
    "eip150Block": 0,
    "eip150Hash": "0x0000000000000000000000000000000000000000000000000000000000000000"
  },
  "nonce": "0x0000000000000042",		
  "timestamp": "0x00",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "extraData": "0x00",
  "gasLimit": "0x80000000",
  "difficulty": "0x4000",
  "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "coinbase": "0x3333333333333333333333333333333333333333",
  "alloc": {}
}
```

#### geth 초기화
geth 초기화 = genesis.json 파일을 이용해서 genesis 블록을 생성
```cmd
C:\testnet> geth --datadir c:\testnet init c:\testnet\genesis.json
```

#### geth 실행
```cmd
C:\testnet> geth --datadir c:\testnet console --networkid 4649 --nodiscover --maxpeers 0
```

#### IPC 접속
명령 프롬프트를 하나 더 실행해서 IPC 접속을 시도
```cmd
C:\Users\admin> geth attach ipc:\\.\pipe\geth.ipc
Welcome to the Geth JavaScript console!
```
#### 데이터 디렉터리 구성 확인
```cmd
C:\Users\admin> cd c:\testnet
c:\testnet> tree c:\testnet /f /a
```
폴더 PATH의 목록입니다.
볼륨 일련 번호가 00000092 8C63:168C입니다.

#### EOA (외부 소유 계정) 생성 
```cmd
> personal.newAccount("pass0")
INFO [07-01|14:11:20.653] Your new key was generated               address=0xbc1148161cfEd3731F971e0Ed2121481A7E6B2CD 	⇐ EOA
WARN [07-01|14:11:20.660] Please backup your key file!             path=c:\testnet\keystore\UTC--2021-07-01T05-11-19.299469000Z--bc1148161cfed3731f971e0ed2121481a7e6b2cd
WARN [07-01|14:11:20.669] Please remember your password!
"0xbc1148161cfed3731f971e0ed2121481a7e6b2cd"


> eth.accounts
["0xbc1148161cfed3731f971e0ed2121481a7e6b2cd"]	⇐ 배열


> personal.newAccount("pass1")
INFO [07-01|14:15:27.781] Your new key was generated               address=0xa81A2CFCd53f0f032053BB6d41A5A0b06b9Ac17e
WARN [07-01|14:15:27.788] Please backup your key file!             path=c:\testnet\keystore\UTC--2021-07-01T05-15-26.306478300Z--a81a2cfcd53f0f032053bb6d41a5a0b06b9ac17e
WARN [07-01|14:15:27.796] Please remember your password!
"0xa81a2cfcd53f0f032053bb6d41a5a0b06b9ac17e"


> eth.accounts
["0xbc1148161cfed3731f971e0ed2121481a7e6b2cd", "0xa81a2cfcd53f0f032053bb6d41a5a0b06b9ac17e"]


> eth.accounts[0]
"0xbc1148161cfed3731f971e0ed2121481a7e6b2cd"

> eth.accounts[1]
"0xa81a2cfcd53f0f032053bb6d41a5a0b06b9ac17e"

```

#### Geth 명령으로 계정 생성 및 확인

```cmd
C:\testnet> geth --datadir c:\testnet account new
INFO [07-01|14:22:06.160] Maximum peer count                       ETH=50 LES=0 total=50
Your new account is locked with a password. Please give a password. Do not forget this password.
Password: pass2
Repeat password: pass2

Your new key was generated
.
.
.
C:\testnet> geth --datadir c:\testnet account list
INFO [07-01|14:23:38.435] Maximum peer count                       ETH=50 LES=0 total=50
INFO [07-01|14:23:38.511] Set global gas cap                       cap=50,000,000
Account #0: {bc1148161cfed3731f971e0ed2121481a7e6b2cd} keystore://c:\testnet\keystore\UTC--2021-07-01T05-11-19.299469000Z--bc1148161cfed3731f971e0ed2121481a7e6b2cd
Account #1: {a81a2cfcd53f0f032053bb6d41a5a0b06b9ac17e} keystore://c:\testnet\keystore\UTC--2021-07-01T05-15-26.306478300Z--a81a2cfcd53f0f032053bb6d41a5a0b06b9ac17e
Account #2: {c1006f907db701c832b516f1b14931f14edac3d0} keystore://c:\testnet\keystore\UTC--2021-07-01T05-22-29.289023500Z--c1006f907db701c832b516f1b14931f14edac3d0

```

## 채굴(mining)

```cmd
C:\testnet> geth --datadir c:\testnet console --networkid 4649 --nodiscover --maxpeers 0
```


### 코인베이스 계정 조회 및 변경
```cmd
> eth.accounts
["0xbc1148161cfed3731f971e0ed2121481a7e6b2cd", "0xa81a2cfcd53f0f032053bb6d41a5a0b06b9ac17e", "0xc1006f907db701c832b516f1b14931f14edac3d0"]

> eth.coinbase
"0xbc1148161cfed3731f971e0ed2121481a7e6b2cd"

> miner.setEtherbase("0xc1006f907db701c832b516f1b14931f14edac3d0")
true

> eth.coinbase
"0xc1006f907db701c832b516f1b14931f14edac3d0"

> miner.setEtherbase(eth.accounts[0])
true

> eth.coinbase
"0xbc1148161cfed3731f971e0ed2121481a7e6b2cd"
```

### 잔고확인
```cmd
> eth.getBalance("0xbc1148161cfed3731f971e0ed2121481a7e6b2cd")
0
> eth.getBalance(eth.coinbase)
0
> eth.getBalance(eth.accounts[0])
0
```

### 블록 길이를 확인
```cmd
> eth.blockNumber
0 			⇐ 마이닝 전이므로 
> miner.start(1)             ⇐ 마이닝 시작
INFO [07-01|14:43:12.399] Updated mining threads                   threads=1
INFO [07-01|14:43:12.404] Transaction pool price threshold updated price=1,000,000,000
nIuNlFlO
[0> 7-01|14:43:12.408] Commit new mining work                   number=1 sealhash=96170e..31fc64 uncles=0 txs=0 gas=0 fees=0 elapsed=0s
INFO [07-01|14:43:13.442] Generating DAG in progress               epoch=0 percentage=0 elapsed=528.587ms
INFO [07-01|14:43:13.989] Generating DAG in progress               epoch=0 percentage=1 elapsed=1.076s
INFO [07-01|14:43:14.528] Generating DAG in progress               epoch=0 percentage=2 elapsed=1.614s
INFO [07-01|14:43:15.077] Generating DAG in progress               epoch=0 percentage=3 elapsed=2.164s

> miner.stop()              ⇐ 마이닝 멈추기

> eth.blockNumber
14

> eth.getBalance(eth.coinbase)
70000000000000000000			⇐ wei 단위

> web3.fromWei(eth.getBalance(eth.coinbase), "ether")
70					⇐ ether 단위


```
채굴보상 = 블록길이 * 5이더
70 = 14 * 5



### 이더 송금
* 첫번째 계정에서 두번째 계정으로 10 이더를 송금

첫번째 계정과 두번째 계정의 잔액을 확인
```cmd
> web3.fromWei(eth.getBalance(eth.accounts[0]), "ether")
70
```
```cmd
> web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")
0
```

#### 송금
```cmd
> eth.sendTransaction({ from: eth.accounts[0], to: eth.accounts[1], value: web3.toWei(10, "ether") })
> personal.unlockAccount(eth.accounts[0])
> eth.sendTransaction({ from: eth.accounts[0], to: eth.accounts[1], value: web3.toWei(10, "ether") })
WARN [07-01|15:21:12.632] Caller gas above allowance, capping      requested=2,116,240,524 cap=50,000,000
INFO [07-01|15:21:12.639] Setting new local account                address=0xbc1148161cfEd3731F971e0Ed2121481A7E6B2CD
INFO [07-01|15:21:12.644] Submitted transaction                    hash=0x52971667f7ab5f44548493b39ccb39ef70808be40350694de4dfc2bc718b5580 from=0xbc1148161cfEd3731F971e0Ed2121481A7E6B2CD nonce=0 recipient=0xa81A2CFCd53f0f032053BB6d41A5A0b06b9Ac17e value=10,000,000,000,000,000,000
"0x52971667f7ab5f44548493b39ccb39ef70808be40350694de4dfc2bc718b5580"	⇐ 트랜젝션 아이디
>

```

#### 계정잠금 해제 방법
```cmd
> personal.unlockAccount(eth.accounts[0])
> personal.unlockAccount(eth.accounts[0], "pass0")
> personal.unlockAccount(eth.accounts[0], "pass0", 0)
```

#### 계류 중인 트랜잭션을 확인
```cmd
> eth.pendingTransactions
[{
    blockHash: null,
    blockNumber: null,
    from: "0xbc1148161cfed3731f971e0ed2121481a7e6b2cd",
    gas: 21000,
    gasPrice: 1000000000,
    hash: "0x52971667f7ab5f44548493b39ccb39ef70808be40350694de4dfc2bc718b5580",
    input: "0x",
    nonce: 0,
    r: "0x3448f9ef95cf37e19797e48e3d8642607255f2580efd699ebc69b31b1e2a93b",
    s: "0x2b6a1fde8776e412acb3ab01d49fe0d74a324ab5131f7b5b3f0ea76b5ecb6d6",
    to: "0xa81a2cfcd53f0f032053bb6d41a5a0b06b9ac17e",
    transactionIndex: null,
    type: "0x0",
    v: "0x41",
    value: 10000000000000000000
}]
>

```


#### 채굴을 통해서 트랜잭션을 처리
```
> miner.start(1)
> eth.pendingTransactions
```

#### 첫번째 두번째 계정의 잔액을 조회
```
> web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")
10			⇐ 송금을 통해서 전달된 이더를 확인
> web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")
10			⇐ 송금을 통해서 전달된 이더를 확인
```

### 블록 길이 조회
```
> eth.blockNumber
21

```


#### 첫번째 계정의 잔액
전체 블록 길이 * 5 이더 - 송금한 10 이더 
= 21 * 5 - 10 = 95






#### 트랜잭션의 상태를 확인
```
> eth.getTransaction(트랜잭션아이디)

> eth.getTransaction("0x52971667f7ab5f44548493b39ccb39ef70808be40350694de4dfc2bc718b5580")
{
  blockHash: "0x77d84c5c765fc28dbd075f00c626231321b82f71a09e2a5b95040af829a15de1",
  blockNumber: 15,
  from: "0xbc1148161cfed3731f971e0ed2121481a7e6b2cd",
  gas: 21000,
  gasPrice: 1000000000,
...
> eth.getBlock(15)
> eth.getTransaction(eth.getBlock(15).transactions[0])

```

#### 리스트 확인
```
> eth.getTransactionReceipt(eth.getBlock(15).transactions[0])
{
  blockHash: "0x77d84c5c765fc28dbd075f00c626231321b82f71a09e2a5b95040af829a15de1",
  blockNumber: 15,
  contractAddress: null,
  cumulativeGasUsed: 21000,
  effectiveGasPrice: 1000000000,
  from: "0xbc1148161cfed3731f971e0ed2121481a7e6b2cd",
  gasUsed: 21000,
  logs: [],
  logsBloom: "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  root: "0x87a69e27cbad0752577e41980715d63dd06564cbb83f431cef4d3ab3a0df83b2",
  to: "0xa81a2cfcd53f0f032053bb6d41a5a0b06b9ac17e",
  transactionHash: "0x52971667f7ab5f44548493b39ccb39ef70808be40350694de4dfc2bc718b5580",
  transactionIndex: 0,
  type: "0x0"
}
```

#### 두번째 계정에서 세번째 계정으로 5이더를 송금
**각 계정의 잔액을 확인**

1. 두번째 계정에서 세번째 계정으로 5이더를 송금


2. 채굴을 통해서 블록 생성한 후 채굴 중지


3. 세번째 계정에 잔액을 확인

4. 두번째 계정에 잔액을 확인

5. 첫번째 계정에 잔액을 확인









