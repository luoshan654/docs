---
title: Qitmeer-wallet RPC
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

# Qitmeer-wallet RPC Reference

Downlocad Qitmeer Wallet from [github.com/Qitmeer/qitmeer-wallet](https://github.com/Qitmeer/qitmeer-wallet)

```sh
# run rpc or ul model  will support rpc interface

./qitmeer-wallet qc web
```

Useage: 

RPC interface URL http://127.0.0.1:38130/api

```sh

curl -k -u "user:password" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_createAccount","params":["account"],"id":1}' http://127.0.0.1:38130/api | jq
```


# API List 

## 1. wallet_unlock {password} {second}
### info: 解锁钱包
### args：
- password 钱包密码
- second 解锁时间,单位秒
### example:
```json
{"jsonrpc":"1.0","method":"wallet_unlock","params":["password",30],"id":1}
```

## 2. wallet_lock
### info：锁定钱包
### example:
```json
{"jsonrpc":"1.0","method":"wallet_lock","params":[],"id":1}
```

## 3. wallet_getAccountsAndBalance
### info: 获取所有的账号和余额
### example:
```json
{"jsonrpc":"1.0","method":"wallet_getAccountsAndBalance","params":[],"id":1}
```
result:
```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "account": {
            "TotalAmount": 0,
            "SpendAmount": 0,
            "UnspendAmount": 0,
            "ConfirmAmount": 0
        },
        "default": {
            "TotalAmount": 280000000000,
            "SpendAmount": 0,
            "UnspendAmount": 280000000000,
            "ConfirmAmount": 0
        },
        "imported": {
            "TotalAmount": 11172999678800,
            "SpendAmount": 325000000000,
            "UnspendAmount": 8754999678800,
            "ConfirmAmount": 2418000000000
        }
    }
}

```

## 4. wallet_createAccount {accountName} 
### info: 添加账户
### args：
- accountName 新账户名
### example:
```json
{"jsonrpc":"1.0","method":"wallet_createAccount","params":["accountName"],"id":1}
```

## 5. wallet_getAddressesByAccount {accountName}
### info: 获取账户所有的地址
### args：
- accountName 账户名
### example:
```json
{"jsonrpc":"1.0","method":"wallet_getAddressesByAccount","params":["default"],"id":1}
```
result:
```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": [
        "TmSbEJs3nDmy68Af7M4Rsuj4pyAwcAret5a",
        "Tmbzp2af9Ereh2hRejcVH9mCQgYdY2GHCAa",
        "TmZu8zU1i6xbZMpLQZLMAJsyWHanZXUZtiV"
    ]
}
```
## 6. wallet_createAddress {accountName}
### info: 创建地址
### args：
- accountName 账户名
### example:
```json
{"jsonrpc":"1.0","method":"wallet_createAddress","params":["default"],"id":1}
```
result:
```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "TmhMzHPCH6F2k3WYQkyvjhwAXoZt7q8TFv9"
}
```

## 7. wallet_sendToAddressByAccount {fromAccount} {toAddr} {amount} {comment} {commentTo}
### info: 发送交易
### args：
- fromAccount from account
- toAddr send to address
- amount send amount coin
- comment
- commentTo 
### example:
```json
{"id":1574828051839,"method":"wallet_sendToAddressByAccount","params":["default","TmZu8zU1i6xbZMpLQZLMAJsyWHanZXUZtiV",800,"",""]}
```
result:
```json
{
    "jsonrpc": "2.0",
    "id": 1574828051839,
    "result": "b1ff3645c374992313e66d504fdf4fd3f2006f9414b97a7e1f6382328cc74fb1"
}
```

## 8. wallet_getTxListByAddr {addr} {type} {page} {pageSize}
### info: 获取地址相关交易列表
### args：
- addr 
- type  0: in tx; 1: out tx; 2: all tx 
- page 
- pageSize
### example:
```json
{"id":1574750774018,"method":"wallet_getTxListByAddr","params":["TmhJcjphz3Y3jRysKT56JaH8m9pzAzsFMu7",2,-1,100]}
```
result:
```json
{
    "jsonrpc": "2.0",
    "id": 1574750774018,
    "result": {
        "Total": 1,
        "Page": 1,
        "PageSize": 1000000000,
        "transactions": [
            {
                "hex": "",
                "txid": "47879fb9dea684e4ce6f24f30812d3832d11fee34400754c6d8b34cd7d7eba8f",
                "txhash": "937de7e15ec48e9cd58d79c594e7395015d5c663924ab5af929a9ef5e5f2e446",
                "size": 377,
                "version": 1,
                "locktime": 0,
                "expire": 0,
                "vin": [
                   ...
                ],
                "vout": [
                   ...
                ],
                "blockhash": "026c6c85a1ae0183fe2e8bfda3450b9990acf9b8c4af3e995f9e361c7bb3d4cd",
                "confirmations": 0
            }
        ]
    }
}
```

## 9. wallet_importWifPrivKey {accountName} {privKey} {rescan}
### info: 导入wif格式私钥
### args：
- accountName 导入账户,目前只支持imported
- privKey 私钥
- rescan  bool,是否重新扫描交易记录
### example:
```json
{"id":1574750774018,"method":"wallet_importWifPrivKey","params":["imported","xxxxx",false]}
```

## 10. wallet_dumpPrivKey {addr}
### info: 导出地址wif格式私钥
### args：
- addr 地址
### example:
```json
{"id":1574829854509,"method":"wallet_dumpPrivKey","params":["Tmh3je9zbnHAvPfwwHhQsFSJmKkeRTtKqmV"]}
```

## 11. ui_openWallet {pass}
### info: 打开钱包 
### args：
- pass 钱包密码
### example:
```json
{"jsonrpc":"1.0","method":"ui_openWallet","params":["pass"],"id":1}
```

## 12. wallet_syncStats
### info: 查看当前钱包同步高度 
### args：
### example:
```json
{"jsonrpc":"1.0","method":"wallet_syncStats","params":[],"id":1}
```
result:
```json
{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"Height": 20460
	}
}
```

## 13. wallet_getUtxo {addr}
### info: 获取指定地址可用utxo
### args：
- addr 地址
### example:
```json
{"jsonrpc":"1.0","method":"wallet_getUtxo","params":["TmgD1mu8zMMV9aWmJrXqQYnWRhR9SBfDZG6"],"id":1}
```
result:
```json
{
	"jsonrpc": "2.0",
	"id": 1,
	"result": [{
		"Txid": "54c47af3a17201c64a8f3b27164d4e09e8e38e05501b16bfd4f001caeddfa86a",
		"Index": 1,
		"Amount": 699925600
	}]
}
```

## 14. wallet_importPrivKey {accountName} {privKey} {rescan}
### info: 导入私钥
### args：
- accountName 导入账户,目前只支持imported
- privKey 私钥
- rescan  bool,是否重新扫描交易记录
### example:
```json
{"jsonrpc":"1.0","method":"wallet_importPrivKey","params":["imported","xxxxxx",true],"id":1}
```


## 15. wallet_getBalanceByAddr {addr}
### info: 获取地址余额 
### args：
- addr 地址
### example:
```json
{"jsonrpc":"1.0","method":"wallet_getBalanceByAddr","params":["TmfDniZnvsjdH98GsH4aetL3XQKFUTWPp4e",1],"id":16}
```
result:
```json
{
	"jsonrpc": "2.0",
	"id": 16,
	"result": {
		"TotalAmount": 400000000,
		"SpendAmount": 0,
		"UnspendAmount": 400000000,
		"ConfirmAmount": 0
	}
}
```

## 15. wallet_sendToAddressBatch {addr:amount}
### info: 单地址批量交易
### args：
- addr 地址
- amount 金额
### example:
```json
{
	"id": 1578639635748,
	"method": "wallet_sendToAddressBatch",
	"params": [{
		"TmeUg4pxc14y64J5BQj4M7jKEryeYfJ4APh": 0.1,
		"TmU3Xwo1rnh4hTKBwifDYAccDrF3kxXaEFe": 0.2,
		"TmjbGfbcMN1nVVHdcvzmPA4ksKqGq4eEkXu": 0.3,
		"TmmWRCMcRZ1ZGdQEw2BwZ3ibsobATw4KTrw": 0.4
	}]
}
```
result:
```json
{
    "jsonrpc": "2.0",
    "id": 1578639635748,
    "result": "d7a7d24d47bb66ad3d3185764808af730c9a9dbb5970686cf6e5a1d5f249923c"
}
```


