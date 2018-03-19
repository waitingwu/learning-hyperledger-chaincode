# Chaincode API

每隻chaincode都要實作Chaincode interface。

一段chaincode所建立的帳本狀態是與其他chaincode相互隔離的，但若處於相同網路中，只要取得許可就可以調用其他chaincode來訪問自己的帳本

> Init\(初始化\): 在chaincode接收到instantiate或upgrade交易時被調用
>
> Invoke\(調用\): 在invoke交易時被調用以執行交易

 The shim package provides APIs that let your chaincode interact with the underlying blockchain network to access state variables, transaction context, caller certificates and attributes, and to invoke other chaincodes, among other operations.

