---
layout: post
title: Set up development env (1)
subtitle: preparing local development environment to build and deploy eosio smart contracts
tags: [eosio, markdown]
---

### keosd 실행시 문제해결

* 회사내 service 이용시 keosd 실행시 libusb library를 찾지 못하는 경우에 brew로 libusb 설치한다.
* 설치한 후 library path를 .bashrc에 추가한다.

```bash
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/home/linuxbrew/.linuxbrew/lib
```

### wallet 생성

wallet은 cleos (~ command line eos 일듯)로 생성한다.

```bash
~$ cleos wallet create --to-console
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5JqNDg7RN5R6yVD9KF1PKrRZBiazRjShy2LqU8H3aYcPmoytHM2"
```

PW5JqNDg7RN5R6yVD9KF1PKrRZBiazRjShy2LqU8H3aYcPmoytHM2 는 wallet password로 사용된다.

wallet 관련 작업은 모두 cleos를 사용하는 듯.

### wallet open/list/lock/unlock

wallet은 기본적으로 close 상태이므로 open해서 사용한다.

```bash
~$ cleos wallet open
~$ cleos wallet list
Wallets:
[
  "default"
]
~$ cleos wallet unlock #password를 입력해야 함.
password: Unlocked: default
~$ cleos wallet list # default 옆에 * 가 붙었다. wallet이 unlock되었다는 것을 표시함.
Wallets:
[
  "default *"
]
```

### import keys into a wallet

wallet을 open한 상태에서 진행해야 함. open된 지갑에 keys를 import한다.
keys는 일반적으로 public key와 private key의 쌍이다.

private key 하나를 생성한다.

```bash
~$ cleos wallet create_key
Created new private key with a public key of: "EOS5nFzT62pCx2aPfC3u752oMaRmXt64zWXR3jUron1TP5DjMV6mG"
```

### import the development key into wallet
 
모든 새로운 EOSIO chain에는 eosio account가 존재함.
eosio는 EOSIO chain의 거버넌스와 합의를 수행하는 system contracts를 loading하여 chain을 설정하는데 사용되는 계정.

```bash
~$ cleos get account eosio
created: 2018-06-01T12:00:00.000
privileged: true
permissions: 
     owner     1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
        active     1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
memory: 
     quota:       unlimited  used:      2.66 KiB  

net bandwidth: 
     used:               unlimited
     available:          unlimited
     limit:              unlimited

cpu bandwidth:
     used:               unlimited
     available:          unlimited
     limit:              unlimited
```
eosio account의 owner/active public key에 해당하는 private key는 아래와 같다.

```bash
5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```

이미 생성된 private key이므로 생성하지는 않는다.
private key를 wallet에 import한다.

```bash
~$ cleos wallet import # 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3 key를 copy / paste로 입력하자.
private key:
```

### keys 확인

```bash
~$ cleos wallet keys
[
  "EOS5nFzT62pCx2aPfC3u752oMaRmXt64zWXR3jUron1TP5DjMV6mG",
  "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV"
]
```

* EOS5nFzT62pCx2aPfC3u752oMaRmXt64zWXR3jUron1TP5DjMV6mG : cleos wallet create_key로 생성된 public key
* EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV : cleos wallet import로 생성된 public key

> cleos wallet private_keys 명령어로 public / private key 쌍을 모두 볼 수 있다.

```bash
~$ cleos wallet private_keys
password: [[
    "EOS5nFzT62pCx2aPfC3u752oMaRmXt64zWXR3jUron1TP5DjMV6mG",
    "5JFUfP9F5YoK4i8PBDonduVH9isRENNBtTSrfEfGpAprGmGJYto"
  ],[
    "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
    "5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"
  ]
]
```
