---
layout: post
title: Installing eosio
subtitle: eosio 설치
tags: [eosio, markdown]
---

### eosio 설치

home direcotry 내에 eosio를 설치해야 하는 경우 아래와 같이... ...

```bash
~$ wget https://github.com/EOSIO/eos/releases/download/v2.0.9/eosio_2.0.9-1-ubuntu-18.04_amd64.deb
~$ dpkg-deb -x ./eosio_2.0.9-1-ubuntu-18.04_amd64.deb /home/worker/eosio/
```

### eosio cdt 설치

```bash
~$ wget https://github.com/eosio/eosio.cdt/releases/download/v1.7.0/eosio.cdt_1.7.0-1-ubuntu-18.04_amd64.deb
~$ dpkg-deb -x ./eosio.cdt_1.7.0-1-ubuntu-18.04_amd64.deb /home/worker/eosio.cdt
```

### path 설정
 
설치후 path 설정하기 위해 아래와 export 문을 .bashrc에 추가.

```bash
export PATH=${PATH}:/home/worker/eosio/usr/bin:/home/worker/eosio.cdt/usr/bin
```
