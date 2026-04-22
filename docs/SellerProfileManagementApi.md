# SellerProfileManagementApi

All URIs are relative to *https://bwdk-backend.digify.shop*

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**merchantApiV1AuthStatusRetrieve**](SellerProfileManagementApi.md#merchantApiV1AuthStatusRetrieve) | **GET** /merchant/api/v1/auth/status/ | وضعیت لاگین بودن |


<a id="merchantApiV1AuthStatusRetrieve"></a>
# **merchantApiV1AuthStatusRetrieve**
> AuthStatusResponse merchantApiV1AuthStatusRetrieve()

وضعیت لاگین بودن

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  بررسی وضعیت احراز هویت فروشنده  ## توضیحات  این endpoint برای بررسی اعتبار **API_KEY** فروشنده استفاده می‌شود. اگر کلید معتبر باشد، پاسخ &#x60;is_authenticated: true&#x60; برمی‌گردد. از این endpoint برای تأیید صحت کلید API قبل از شروع عملیات استفاده کنید.  نیاز به **API_KEY** فروشنده دارد (فقط Header لازم است، بدنه درخواست ندارد).  &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = SellerProfileManagementApi()
try {
    val result : AuthStatusResponse = apiInstance.merchantApiV1AuthStatusRetrieve()
    println(result)
} catch (e: ClientException) {
    println("4xx response calling SellerProfileManagementApi#merchantApiV1AuthStatusRetrieve")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling SellerProfileManagementApi#merchantApiV1AuthStatusRetrieve")
    e.printStackTrace()
}
```

### Parameters
This endpoint does not need any parameter.

### Return type

[**AuthStatusResponse**](AuthStatusResponse.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

