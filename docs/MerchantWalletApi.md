# MerchantWalletApi

All URIs are relative to *https://bwdk-backend.digify.shop*

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**walletsApiV1WalletBalanceRetrieve**](MerchantWalletApi.md#walletsApiV1WalletBalanceRetrieve) | **GET** /wallets/api/v1/wallet-balance/ | Get Wallet Balance |


<a id="walletsApiV1WalletBalanceRetrieve"></a>
# **walletsApiV1WalletBalanceRetrieve**
> WalletBalance walletsApiV1WalletBalanceRetrieve()

Get Wallet Balance

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  موجودی کیف پول فروشنده  ## توضیحات  این endpoint موجودی کیف پول فروشنده را برمی‌گرداند. کیف پول برای پرداخت هزینه ارسال دیجی‌اکسپرس استفاده می‌شود. هنگام ثبت مرسوله دیجی‌اکسپرس، هزینه ارسال به‌صورت خودکار از کیف پول کسر می‌شود.  نیاز به **API_KEY** فروشنده دارد.  &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = MerchantWalletApi()
try {
    val result : WalletBalance = apiInstance.walletsApiV1WalletBalanceRetrieve()
    println(result)
} catch (e: ClientException) {
    println("4xx response calling MerchantWalletApi#walletsApiV1WalletBalanceRetrieve")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling MerchantWalletApi#walletsApiV1WalletBalanceRetrieve")
    e.printStackTrace()
}
```

### Parameters
This endpoint does not need any parameter.

### Return type

[**WalletBalance**](WalletBalance.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

