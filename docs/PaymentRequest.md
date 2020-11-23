# PaymentRequest

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**currency** | [**CryptoCurrency**](CryptoCurrency.md) |  | [optional] 
**payment_id** | **str** | Unique identifier of the payment in selected currency | [optional] 
**address** | **str** | One-use address for receive your client payment | [optional] 
**pin** | **str** | PIN, it will be required if you need support with this payment.\\ *Note: It&#39;s provided only the first time you create the payment request* | [optional] 
**type** | **int** | * &#x60;0: Receive and forward&#x60; payment is forwarded to a desired coin address once it&#39;s confirmed  * &#x60;1: Receive and store&#x60; payment is stored in a payrobot.io wallet  | [optional] 
**amount** | **str** | The payment amount your client has to send to the coin address | [optional] 
**callback** | **str** | URL where payrobot.io will send the status of the payment (Webhook) | [optional] 
**fee_pct** | **float** | Fee percentage that will be discounted | [optional] [default to 0.9]
**fee_amount** | **str** | Fee amount that will be discounted | [optional] 
**final_amount** | **str** | Final amount of the transaction (Fee discount is already applied)   * For &#x60;Receive and forward&#x60; payment is the total amount to &#x60;forward&#x60; as soon as the payment is confirmed         * For &#x60;Receive and forward&#x60; payment is the total amount to &#x60;store&#x60; in the wallet as soon as the payment is confirmed | [optional] 
**destination** | **str** | * For &#x60;Receive and forward&#x60; payment is the coin &#x60;ADDRESS&#x60; where the payment is going to be forwarded as soon as it&#39;s confirmed  * For &#x60;Receive and store&#x60; payment is the &#x60;WALLET ID&#x60; where the payment is going to be stored as soon as it&#39;s confirmed  | [optional] 
**reference** | **str** | Custom reference for payment identifying | [optional] 
**timestamp** | **int** | Request creation date expressed in UNIX timestamp | [optional] 
**lastupdate** | **int** | Last update expressed in UNIX timestamp | [optional] 
**status** | **int** | Status of the payment:    * &#x60;0: Idle&#x60; payment has not been paid    * &#x60;1: Incomplete&#x60; payment is being paid partially    * &#x60;2: Confirming&#x60; payment has been received completely but it&#39;s not confirmed by network yet    * &#x60;3: Confirmed&#x60; payment has been paid completely and it has at least &#x60;1&#x60; confirmation by network  | [optional] 
**error** | **bool** | &#x60;true&#x60; is there was a problem. &#x60;false&#x60; if not  | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


