# payrobot.WalletApi

All URIs are relative to *https://api.payrobot.io*

Method | HTTP request | Description
------------- | ------------- | -------------
[**create_wallet**](WalletApi.md#create_wallet) | **POST** /{currency}/wallets | Create new wallet
[**create_wallet_send_request**](WalletApi.md#create_wallet_send_request) | **POST** /{currency}/wallets/{walletId}/send-requests | Send funds from a wallet
[**get_wallet**](WalletApi.md#get_wallet) | **GET** /{currency}/wallets/{walletId} | Get Wallet information
[**get_wallet_history**](WalletApi.md#get_wallet_history) | **GET** /{currency}/wallets/{walletId}/history | Get last transactions of wallet
[**get_wallet_send_request**](WalletApi.md#get_wallet_send_request) | **GET** /{currency}/wallets/{walletId}/send-requests/{requestId} | Obtain information of a send request


# **create_wallet**
> WalletCreationInfo create_wallet(currency)

Create new wallet

Creates a new wallet where you can receive, store and send funds for your web or app.  --- ## Important This method returns your `Wallet Passphrase`, it will be required when you send funds from your wallet. **Please keep it safe and private** 

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
    api_instance = payrobot.WalletApi(api_client)
    currency = 'btc' # str | Object Currency:   * `btc`: Bitcoin   * `ltc`: Litecoin   * `bch`: Bitcoin Cash 

    try:
        # Create new wallet
        api_response = api_instance.create_wallet(currency)
        pprint(api_response)
    except ApiException as e:
        print("Exception when calling WalletApi->create_wallet: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **currency** | **str**| Object Currency:   * &#x60;btc&#x60;: Bitcoin   * &#x60;ltc&#x60;: Litecoin   * &#x60;bch&#x60;: Bitcoin Cash  | 

### Return type

[**WalletCreationInfo**](WalletCreationInfo.md)

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

# **create_wallet_send_request**
> WalletSendRequest create_wallet_send_request(currency, wallet_id, destination, seed, token, param_callback=param_callback)

Send funds from a wallet

Sends funds from a wallet to one or multiple addresses.  --- ## Required Authorization Token This transaction requires an authorization `token` which is the result of the `sha-256` hash of the following string:        walletId~destination~seed~walletPassphrase    **For example**  Considering the following example values for the token:   - `walletId` 9df3f909-088d-4724-b34f-9a587c5ccc15   - `destination`     [{\"address\":\"bc1q5defveu0acrf87m3huwxjq6pqaszdjf3d4ej9y\",\"amount\":0.01},{\"address\":\"bc1qs59a7e23zpjm0znteytrxvj839dlp205e50zch\",\"amount\":0.056}]     - `seed` 758748394   - `walletPassphrase` **Note: this was provided when you created the wallet** OHh6IIININmfmjGGsxlBBft2ch61VncaPscsp295h2ULx9xPY07Jom3d5cBifgoW    The resulting string, previous to hash is::        9df3f909-088d-4724-b34f-9a587c5ccc15~[{\"address\":\"bc1q5defveu0acrf87m3huwxjq6pqaszdjf3d4ej9y\",\"amount\":0.01},{\"address\":\"bc1qs59a7e23zpjm0znteytrxvj839dlp205e50zch\",\"amount\":0.056}]~758748394~OHh6IIININmfmjGGsxlBBft2ch61VncaPscsp295h2ULx9xPY07Jom3d5cBifgoW    Finally after applying `sha-256` hash, we obtain the required `token`:        804ca9457b0fe3e4d243fe9e39e760ff1f287491ae8e79d015f92f7c6c96d7b1       --- ## Important    * Send requests are commonly queued, optionally you can specify a callback to get your web / app notified as soon as the request has been fully broadcasted to the Network.    * Transaction is limited to `25` destination addresses per request      * Tx Hash is provided only through the callback      * Confirmed send requests information is `DELETED` after `3 days` of being confirmed    --- ## Minimum Send Amounts     * `Bitcoin`: 0.0001 BTC   * `Litecoin`: 0.001 LTC   * `Bitcoin Cash`: 0.001 BCH    --- ## Callback Send requests are commonly queued, optionally you can specify a callback to get your web / app notified as soon as the request has been fully broadcasted to the Network.  The callback sent to your callback url is a **POST** request with the following parameters:       *Example:*      currency:     \"BTC\"     walletId:     \"698fd3f6-5482-4798-8a46-6732af440616\"     requestId:    \"123fd3f6-9078-5790-4f40-6932bf440120\"     timestamp:    1577179288     lastupdate:   1577179388     amount:       \"0.01\"     callback:     \"https://callback-url.com\"     destination:  '[{\"address\": \"bc1qf6ss0qtdn5q42...\"                   \"amount\": \"0.01\"}]'     txid:         \"2cdac43e92e65cb428e3ed992bcf61347...\"     status:       0 

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
    api_instance = payrobot.WalletApi(api_client)
    currency = 'btc' # str | Object Currency:   * `btc`: Bitcoin   * `ltc`: Litecoin   * `bch`: Bitcoin Cash 
wallet_id = '9df3f909-088d-4724-b34f-9a587c5ccc15' # str | Wallet where funds to send are stored
destination = '[{\"address\":\"bc1q5defveu0acrf87m3huwxjq6pqaszdjf3d4ej9y\",\"amount\":0.01},{\"address\":\"bc1qs59a7e23zpjm0znteytrxvj839dlp205e50zch\",\"amount\":0.056}] ' # str | JSON formatted array with all the destination addres(es) and the amount(s) to send\\ `[{\"address\":\"desired-destination-address\",\"amount\":X.XXXXXXXX}, ...]` 
seed = '12345' # str | Unique random string generated by your web/app. **IT MUST BE UNIQUE PER TRANSACTION PER WALLET**
token = 'c3c081de9510e8405839f36a875aa9fef43032caa3015305b27d6b7e0bcfc182' # str | SHA-256 hash of the concatenated string (substituting with the proper data):\\ `walletId~destination~seed~walletPassphrase` 
param_callback = 'https://your-app-url.com/example' # str | Optional callback to notify your web / app as soon as the send request has been fully broadcasted to the Network (optional)

    try:
        # Send funds from a wallet
        api_response = api_instance.create_wallet_send_request(currency, wallet_id, destination, seed, token, param_callback=param_callback)
        pprint(api_response)
    except ApiException as e:
        print("Exception when calling WalletApi->create_wallet_send_request: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **currency** | **str**| Object Currency:   * &#x60;btc&#x60;: Bitcoin   * &#x60;ltc&#x60;: Litecoin   * &#x60;bch&#x60;: Bitcoin Cash  | 
 **wallet_id** | **str**| Wallet where funds to send are stored | 
 **destination** | **str**| JSON formatted array with all the destination addres(es) and the amount(s) to send\\ &#x60;[{\&quot;address\&quot;:\&quot;desired-destination-address\&quot;,\&quot;amount\&quot;:X.XXXXXXXX}, ...]&#x60;  | 
 **seed** | **str**| Unique random string generated by your web/app. **IT MUST BE UNIQUE PER TRANSACTION PER WALLET** | 
 **token** | **str**| SHA-256 hash of the concatenated string (substituting with the proper data):\\ &#x60;walletId~destination~seed~walletPassphrase&#x60;  | 
 **param_callback** | **str**| Optional callback to notify your web / app as soon as the send request has been fully broadcasted to the Network | [optional] 

### Return type

[**WalletSendRequest**](WalletSendRequest.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** | Successful operation |  -  |
**500** | error |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_wallet**
> Wallet get_wallet(currency, wallet_id)

Get Wallet information

Gets detailed information from a Wallet

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
    api_instance = payrobot.WalletApi(api_client)
    currency = 'btc' # str | Object Currency:   * `btc`: Bitcoin   * `ltc`: Litecoin   * `bch`: Bitcoin Cash 
wallet_id = '775937b9-b7fc-47cf-be7c-934d602bd6af' # str | ID of the desired Wallet

    try:
        # Get Wallet information
        api_response = api_instance.get_wallet(currency, wallet_id)
        pprint(api_response)
    except ApiException as e:
        print("Exception when calling WalletApi->get_wallet: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **currency** | **str**| Object Currency:   * &#x60;btc&#x60;: Bitcoin   * &#x60;ltc&#x60;: Litecoin   * &#x60;bch&#x60;: Bitcoin Cash  | 
 **wallet_id** | **str**| ID of the desired Wallet | 

### Return type

[**Wallet**](Wallet.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** | Successful operation |  -  |
**500** | error |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_wallet_history**
> WalletHistory get_wallet_history(currency, wallet_id)

Get last transactions of wallet

Gets last 100 transactions of the wallet

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
    api_instance = payrobot.WalletApi(api_client)
    currency = 'btc' # str | Object Currency:   * `btc`: Bitcoin   * `ltc`: Litecoin   * `bch`: Bitcoin Cash 
wallet_id = 'dd304d65-b606-4462-854b-51cdf061b00f' # str | ID of the desired Wallet

    try:
        # Get last transactions of wallet
        api_response = api_instance.get_wallet_history(currency, wallet_id)
        pprint(api_response)
    except ApiException as e:
        print("Exception when calling WalletApi->get_wallet_history: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **currency** | **str**| Object Currency:   * &#x60;btc&#x60;: Bitcoin   * &#x60;ltc&#x60;: Litecoin   * &#x60;bch&#x60;: Bitcoin Cash  | 
 **wallet_id** | **str**| ID of the desired Wallet | 

### Return type

[**WalletHistory**](WalletHistory.md)

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

# **get_wallet_send_request**
> WalletSendRequest get_wallet_send_request(currency, wallet_id, request_id)

Obtain information of a send request

Obtains detailed information about a send request

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
    api_instance = payrobot.WalletApi(api_client)
    currency = 'btc' # str | Object Currency:   * `btc`: Bitcoin   * `ltc`: Litecoin   * `bch`: Bitcoin Cash 
wallet_id = '9df3f909-088d-4724-b34f-9a587c5ccc15' # str | Wallet where funds to send are stored
request_id = '54f78565-56e2-4ece-b925-cab6ed67eb63' # str | Send Request ID

    try:
        # Obtain information of a send request
        api_response = api_instance.get_wallet_send_request(currency, wallet_id, request_id)
        pprint(api_response)
    except ApiException as e:
        print("Exception when calling WalletApi->get_wallet_send_request: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **currency** | **str**| Object Currency:   * &#x60;btc&#x60;: Bitcoin   * &#x60;ltc&#x60;: Litecoin   * &#x60;bch&#x60;: Bitcoin Cash  | 
 **wallet_id** | **str**| Wallet where funds to send are stored | 
 **request_id** | **str**| Send Request ID | 

### Return type

[**WalletSendRequest**](WalletSendRequest.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** | Successful operation |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

