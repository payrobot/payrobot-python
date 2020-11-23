# payrobot.PaymentApi

All URIs are relative to *https://api.payrobot.io*

Method | HTTP request | Description
------------- | ------------- | -------------
[**create_payment**](PaymentApi.md#create_payment) | **POST** /{currency}/payments | Generate a new one-use address to receive a payment
[**get_payment**](PaymentApi.md#get_payment) | **GET** /{currency}/payments/{paymentId} | Get detailed information about a payment


# **create_payment**
> PaymentRequest create_payment(currency, type, destination, amount, param_callback, reference=reference)

Generate a new one-use address to receive a payment

Generates a new one-use address to receive a payment. It callbacks your web/app server as soon as it's paid and confirmed.


**Payment can be `forwarded` to another address or it can be `stored` in
a payrobot.io wallet**


---

## Important

  * Unpaid requests are deleted after **3 hours** of theirs creation
  * Confirmed payments information is deleted after **3 days** of being confirmed

---

## Minimum Amounts


  * `Bitcoin`: 0.0001 BTC
  * `Litecoin`: 0.001 LTC
  * `Bitcoin Cash`: 0.001 BCH

---

## Callbacks

A **payment notificacion** will be sent to your callback url in the
following scenarios:

  1. *Payment is received partially*
  2. *Payment is being confirmed by network*
  3. *Payment is confirmed at least with 1 confirmation*


The callback sent to your callback url is a **POST** request with the
following parameters:


*Example:*

    currency:         "BTC"
    paymentId:        "698fd3f6-5482-4798-8a46-6732af440616"
    address:          "3KoUDMfrov91G4SXaCKGvTWDjGia9Jod5b"
    type:             0
    partialAmount:    "0.00"
                      //Partial amount received when payment is incomplete
    remainingAmount:  "0.00"
                      //Remaining amount to pay when payment is incomplete
    amount:           "0.1"
    feePct:           0.90
    feeAmount:        "0.0009"
    finalAmount:      "0.0991"
    destination:      "698fd3f6-5482-4798-8a46-6732af440616"
    reference:        "12345"
    status:           2

### Example

```python
from __future__ import print_function
import time
import payrobot
from payrobot.rest import ApiException
from pprint import pprint
# Defining the host is optional and defaults to https://api.payrobot.io
# See configuration.py for a list of all supported configuration parameters.
configuration = payrobot.Configuration(
    host = "https://api.payrobot.io"
)


# Enter a context with an instance of the API client
with payrobot.ApiClient() as api_client:
    # Create an instance of the API class
    api_instance = payrobot.PaymentApi(api_client)
    currency = 'btc' # str | Object Currency:   * `btc`: Bitcoin   * `ltc`: Litecoin   * `bch`: Bitcoin Cash 
type = 0 # int | * `0: Receive and forward` payment is forwarded to a desired coin address once it's confirmed  * `1: Receive and store` payment is stored in a payrobot.io wallet 
destination = 'bc1qzlza4ke65fa2sqacjfu5vtwy8ar6x8xttgk999' # str | * For `Receive and forward` payment is the `ADDRESS` where the payment is going to be forwarded as soon as it's confirmed. **ADDRESS HAS TO BE OF THE SAME TYPE OF CURRENCY**  * For `Receive and store` payment is the payrobot.io `WALLET ID` where the payment is going to be stored as soon as it's confirmed. **WALLET HAS TO BE OF THE SAME TYPE OF CURRENCY** 
amount = 0.0129 # float | Amount of the payment
param_callback = 'https://your-callback-url.com' # str | Your URL where payrobot.io will send the status of the payment (Webhook)
reference = 'Bill123' # str | Optional custom reference to identify the payment (optional)

    try:
        # Generate a new one-use address to receive a payment
        api_response = api_instance.create_payment(currency, type, destination, amount, param_callback, reference=reference)
        pprint(api_response)
    except ApiException as e:
        print("Exception when calling PaymentApi->create_payment: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **currency** | **str**| Object Currency:   * &#x60;btc&#x60;: Bitcoin   * &#x60;ltc&#x60;: Litecoin   * &#x60;bch&#x60;: Bitcoin Cash  | 
 **type** | **int**| * &#x60;0: Receive and forward&#x60; payment is forwarded to a desired coin address once it&#39;s confirmed  * &#x60;1: Receive and store&#x60; payment is stored in a payrobot.io wallet  | 
 **destination** | **str**| * For &#x60;Receive and forward&#x60; payment is the &#x60;ADDRESS&#x60; where the payment is going to be forwarded as soon as it&#39;s confirmed. **ADDRESS HAS TO BE OF THE SAME TYPE OF CURRENCY**  * For &#x60;Receive and store&#x60; payment is the payrobot.io &#x60;WALLET ID&#x60; where the payment is going to be stored as soon as it&#39;s confirmed. **WALLET HAS TO BE OF THE SAME TYPE OF CURRENCY**  | 
 **amount** | **float**| Amount of the payment | 
 **param_callback** | **str**| Your URL where payrobot.io will send the status of the payment (Webhook) | 
 **reference** | **str**| Optional custom reference to identify the payment | [optional] 

### Return type

[**PaymentRequest**](PaymentRequest.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** | Successful operation |  -  |
**500** | Error |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_payment**
> PaymentRequest get_payment(currency, payment_id)

Get detailed information about a payment

Gets detailed information about a payment

### Example

```python
from __future__ import print_function
import time
import payrobot
from payrobot.rest import ApiException
from pprint import pprint
# Defining the host is optional and defaults to https://api.payrobot.io
# See configuration.py for a list of all supported configuration parameters.
configuration = payrobot.Configuration(
    host = "https://api.payrobot.io"
)


# Enter a context with an instance of the API client
with payrobot.ApiClient() as api_client:
    # Create an instance of the API class
    api_instance = payrobot.PaymentApi(api_client)
    currency = 'btc' # str | Object Currency:   * `btc`: Bitcoin   * `ltc`: Litecoin   * `bch`: Bitcoin Cash 
payment_id = '698fd3f6-5482-4798-8a46-6732af440616' # str | Payment ID to query

    try:
        # Get detailed information about a payment
        api_response = api_instance.get_payment(currency, payment_id)
        pprint(api_response)
    except ApiException as e:
        print("Exception when calling PaymentApi->get_payment: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **currency** | **str**| Object Currency:   * &#x60;btc&#x60;: Bitcoin   * &#x60;ltc&#x60;: Litecoin   * &#x60;bch&#x60;: Bitcoin Cash  | 
 **payment_id** | **str**| Payment ID to query | 

### Return type

[**PaymentRequest**](PaymentRequest.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** | Succesful operation |  -  |
**500** | Error |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

