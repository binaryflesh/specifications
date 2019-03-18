
# Ontology SDK Baseline

1. Develop a wallet file according to the wallet specification, and store the encrypted account private key of the asset account and identity in the wallet file. There is also a need for mnemonics and keystore functionality.

2. Interacting with the blockchain, including querying and sending transactions.

3. Transaction serialization, constructing the call smart contract bytecode.

4. Complete these native smart contracts: ont, ong, ontid, auth, governance

| Wallet             | Asset                    | RPC             | VM                            |
|:------------------:|:------------------------:|:---------------:|:-----------------------------:|
| Create Account     | Transfer (ONT, ONG) 	    | See #1-http-rpc | Build call contract parameter |
| Delete Account     | Query Balance (ONT, ONG) |                 |                               |
| Export Keystore    | Query Unbound ONG        |                 |                               |
| Import Keystore    | Withdraw ONG             |                 |                               |
| Import Mnemonic    |                          |                 |                               |
| Import Private Key |                          |                 |                               |
| Import WIF         |                          |                 |                               |
 
* [Function list](#function-list)
	* [1. http rpc](#1-http-rpc)
	* [2. wallet](#2-wallet)
	* [3. asset](#3-asset)
	* [4. identity](#3-identity)

## 1. http rpc

>rpc: 
https://github.com/ontio/ontology/blob/master/docs/specifications/rpc_api.md


java code example:

https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/sdk/manager/ConnectMgr.java

need complete:

1.get transaction

2.get smartcontract

3.get smartcontract event

4.get block

5.get block height

6.send transaction

7.get balance

## 2. wallet

>wallet https://github.com/ontio/ontology-ts-sdk/blob/master/docs/en/Wallet_File_Specification.md 

### account: 

need complete:

1.add update get delete

2.Account importAccount(String encryptedPrikey, String password, String address,byte[] salt)

3.Account createAccount(String password)

4.Account createAccountFromPriKey(String password, String prikey)

5.Import from the mnemonic words: MnemonicCode.getPrikeyFromMnemonicCodesStr

6.import from keystore: WalletQR.getPriKeyFromQrCode

7.export keystore:   WalletQR.exportAccountQRCode

java code example:

https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/crypto/MnemonicCode.java

https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/common/WalletQR.java

https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/sdk/manager/WalletMgr.java

### identity: 

>account https://github.com/ontio-community/specifications/blob/master/sdk_dev_standard/en/account.md

need complete:

1.add update get delete

2.Generation Public and Private Key Pair with ECDSA

3.Generate a public key based on the specified private key with ECDSA

4.import export WIF

5.Private key encryption and decryption with GCM, dont need CTR

6.ECDSA signature

7.ECDSA verify signature

java code example:

https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/account/Account.java

## 3. asset

>native asset include ont and ong.

https://github.com/ontio/ontology-java-sdk/blob/master/docs/en/asset.md

java code example:

https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/smartcontract/nativevm/Ong.java

https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/smartcontract/nativevm/Ont.java

You need implement build vm parameter when you make invoke contract transaction,like transfer:

https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/core/scripts/ScriptBuilder.java

buildNativeParams: 
  
  https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/smartcontract/Vm.java

need complete:


1. String sendTransfer(Account sendAcct, String recvAddr, long amount, Account payerAcct, long gaslimit, long gasprice)

2. long queryBalanceOf(String address)

3. String unboundOng(String address)

4. String withdrawOng(Account sendAcct, String toAddr, long amount, Account payerAcct, long gaslimit, long gasprice)

>nep-5 smartcontract digit asset:

don't need do this

## 4. identity

> identity rigistry and get ddo
 https://github.com/ontio/ontology-java-sdk/blob/master/docs/en/identity_claim.md

java code example:

https://github.com/ontio/ontology-java-sdk/blob/master/src/main/java/com/github/ontio/smartcontract/nativevm/OntId.java

need complete:

String sendRegister(Identity ident, String password, Account payerAcct, long gaslimit, long gasprice) 

String sendGetDDO(String ontid)
