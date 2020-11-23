# WalletSendRequest

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**currency** | [**CryptoCurrency**](CryptoCurrency.md) |  | [optional] 
**wallet_id** | **str** | Unique ID of the new created Wallet | [optional] 
**request_id** | **str** | ID of this transaction, it can be used letter in the callback or to query it | [optional] 
**timestamp** | **int** | Request creation date expressed in UNIX timestamp | [optional] 
**lastupdate** | **int** | Last update expressed in UNIX timestamp | [optional] 
**amount** | **str** | Total amount sent from wallet | [optional] 
**callback** | **str** | Optional callback to notify your web / app as soon as the send request has been fully broadcasted to the network | [optional] 
**destination** | [**list[AddressDetail]**](AddressDetail.md) | Array with all the destination coin addres(es) and the amount(s) to send  | [optional] 
**txid** | **str** | Tx Hash. *Only available in requests with confirmed status*  | [optional] 
**status** | **int** | Status of this send request:   * &#x60;0: Queued&#x60; Request has been queued for broadcasting. It usually takes few seconds under normal conditions   * &#x60;1: Broadcasted&#x60; Request has been fully broadcasted to Bitcoin Network   | [optional] [default to 0]
**error** | **bool** | &#x60;true&#x60; is there was a problem. &#x60;false&#x60; if not  | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


