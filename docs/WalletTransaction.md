# WalletTransaction

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**amount** | **str** | Amount of the transaction:   * &#x60;Negative number (&lt; 0)&#x60; is a withdrawal   * &#x60;Positive number (&gt; 0)&#x60; is a deposit  | [optional] 
**addresses** | [**list[AddressDetail]**](AddressDetail.md) | Address(es) involved:   * &#x60;payments&#x60; address(es) where payment was received   * &#x60;withdrawals&#x60; address(es) where funds were sent  | [optional] 
**timestamp** | **int** | Timestamp of the transaction expressed in &#x60;Unix Timestamp&#x60; | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


