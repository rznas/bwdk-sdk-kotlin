# OrderShippingApi

All URIs are relative to *https://bwdk-backend.digify.shop*

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**orderApiV1ManagerCancelShipmentCreate**](OrderShippingApi.md#orderApiV1ManagerCancelShipmentCreate) | **POST** /order/api/v1/manager/{order_uuid}/cancel-shipment/ | Cancel Shipment |
| [**orderApiV1ManagerChangeShippingMethodUpdate**](OrderShippingApi.md#orderApiV1ManagerChangeShippingMethodUpdate) | **PUT** /order/api/v1/manager/{order_uuid}/change-shipping-method/ | Change Shipping Method |
| [**orderApiV1ManagerReviveShipmentCreate**](OrderShippingApi.md#orderApiV1ManagerReviveShipmentCreate) | **POST** /order/api/v1/manager/{order_uuid}/revive-shipment/ | Revive Shipment |


<a id="orderApiV1ManagerCancelShipmentCreate"></a>
# **orderApiV1ManagerCancelShipmentCreate**
> MerchantOrderCancelShipmentResponse orderApiV1ManagerCancelShipmentCreate(orderUuid)

Cancel Shipment

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  لغو مرسوله دیجی‌اکسپرس  ## توضیحات  این endpoint برای لغو یک مرسوله ثبت‌شده در سرویس دیجی‌اکسپرس استفاده می‌شود. پس از لغو موفق، مرسوله از صف ارسال خارج می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## شرایط لغو  * سفارش باید دارای روش ارسال **DigiExpress** باشد * مرسوله باید در وضعیت **در انتظار تحویل به پیک** (Request for Pickup) باشد  &lt;/div&gt;  &#x60;&#x60;&#x60;mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant DX as دیجی‌اکسپرس      M-&gt;&gt;API: POST /order/api/v1/manager/{order_uuid}/cancel-shipment/     Note over M,API: Header: X-API-KEY (بدون بدنه)      alt روش ارسال DigiExpress نیست         API--&gt;&gt;M: 400 خطا         Note over API,M: {error: \&quot;Selected shipping method is not DigiExpress\&quot;}     else مرسوله قابل لغو نیست         API--&gt;&gt;M: 400 خطا         Note over API,M: {error: \&quot;...\&quot;}     else لغو موفق         API-&gt;&gt;DX: لغو مرسوله         DX--&gt;&gt;API: تأیید لغو         API--&gt;&gt;M: 200 موفق         Note over API,M: {message, order_uuid, status, status_display}     end &#x60;&#x60;&#x60; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = OrderShippingApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
try {
    val result : MerchantOrderCancelShipmentResponse = apiInstance.orderApiV1ManagerCancelShipmentCreate(orderUuid)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling OrderShippingApi#orderApiV1ManagerCancelShipmentCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling OrderShippingApi#orderApiV1ManagerCancelShipmentCreate")
    e.printStackTrace()
}
```

### Parameters
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **orderUuid** | **java.util.UUID**|  | |

### Return type

[**MerchantOrderCancelShipmentResponse**](MerchantOrderCancelShipmentResponse.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

<a id="orderApiV1ManagerChangeShippingMethodUpdate"></a>
# **orderApiV1ManagerChangeShippingMethodUpdate**
> OrderDetail orderApiV1ManagerChangeShippingMethodUpdate(orderUuid, orderDetail)

Change Shipping Method

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  تغییر روش ارسال سفارش  ## توضیحات  این endpoint به فروشنده اجازه می‌دهد روش ارسال یک سفارش را تغییر دهد. این عملیات معمولاً زمانی استفاده می‌شود که فروشنده بخواهد از DigiExpress به روش ارسال پیش‌فرض (یا بالعکس) تغییر دهد.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای ورودی  * **updated_shipping**: شناسه روش ارسال جدید * **preparation_time** (اختیاری): زمان آماده‌سازی (روز) برای DigiExpress  &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = OrderShippingApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val orderDetail : OrderDetail =  // OrderDetail | 
try {
    val result : OrderDetail = apiInstance.orderApiV1ManagerChangeShippingMethodUpdate(orderUuid, orderDetail)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling OrderShippingApi#orderApiV1ManagerChangeShippingMethodUpdate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling OrderShippingApi#orderApiV1ManagerChangeShippingMethodUpdate")
    e.printStackTrace()
}
```

### Parameters
| **orderUuid** | **java.util.UUID**|  | |
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **orderDetail** | [**OrderDetail**](OrderDetail.md)|  | |

### Return type

[**OrderDetail**](OrderDetail.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

<a id="orderApiV1ManagerReviveShipmentCreate"></a>
# **orderApiV1ManagerReviveShipmentCreate**
> MerchantOrderReviveShipmentResponse orderApiV1ManagerReviveShipmentCreate(orderUuid, reviveShipment)

Revive Shipment

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  احیای مرسوله دیجی‌اکسپرس  ## توضیحات  این endpoint برای احیای (reactivate) یک مرسوله دیجی‌اکسپرس که قبلاً لغو شده یا در وضعیت غیرفعال است استفاده می‌شود. با ارسال &#x60;preparation_time&#x60; (زمان آماده‌سازی بر حسب روز)، زمان جدید آماده بودن بار تنظیم می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای ورودی  * **preparation_time** (اختیاری، پیش‌فرض: ۲): تعداد روز تا آماده‌شدن بار برای تحویل به پیک  ## شرایط  * سفارش باید دارای روش ارسال **DigiExpress** باشد * مرسوله باید در وضعیت قابل احیا باشد  &lt;/div&gt;  &#x60;&#x60;&#x60;mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant DX as دیجی‌اکسپرس      M-&gt;&gt;API: POST /order/api/v1/manager/{order_uuid}/revive-shipment/     Note over M,API: Header: X-API-KEY&lt;br/&gt;{preparation_time: 2}      alt روش ارسال DigiExpress نیست         API--&gt;&gt;M: 400 خطا         Note over API,M: {error: \&quot;Selected shipping method is not DigiExpress\&quot;}     else احیا موفق         API-&gt;&gt;DX: احیای مرسوله با زمان جدید         DX--&gt;&gt;API: تأیید احیا         API--&gt;&gt;M: 200 موفق         Note over API,M: {message, order_uuid, status, status_display}     end &#x60;&#x60;&#x60; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = OrderShippingApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val reviveShipment : ReviveShipment =  // ReviveShipment | 
try {
    val result : MerchantOrderReviveShipmentResponse = apiInstance.orderApiV1ManagerReviveShipmentCreate(orderUuid, reviveShipment)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling OrderShippingApi#orderApiV1ManagerReviveShipmentCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling OrderShippingApi#orderApiV1ManagerReviveShipmentCreate")
    e.printStackTrace()
}
```

### Parameters
| **orderUuid** | **java.util.UUID**|  | |
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **reviveShipment** | [**ReviveShipment**](ReviveShipment.md)|  | [optional] |

### Return type

[**MerchantOrderReviveShipmentResponse**](MerchantOrderReviveShipmentResponse.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

