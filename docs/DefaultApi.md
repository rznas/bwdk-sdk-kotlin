# DefaultApi

All URIs are relative to *https://bwdk-backend.digify.shop*

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**merchantApiV1AuthStatusRetrieve**](DefaultApi.md#merchantApiV1AuthStatusRetrieve) | **GET** /merchant/api/v1/auth/status/ | وضعیت لاگین بودن |
| [**orderApiV1CreateOrderCreate**](DefaultApi.md#orderApiV1CreateOrderCreate) | **POST** /order/api/v1/create-order/ | ساخت سفارش |
| [**orderApiV1ManagerCancelShipmentCreate**](DefaultApi.md#orderApiV1ManagerCancelShipmentCreate) | **POST** /order/api/v1/manager/{order_uuid}/cancel-shipment/ | لغو ارسال سفارش |
| [**orderApiV1ManagerChangeShippingMethodUpdate**](DefaultApi.md#orderApiV1ManagerChangeShippingMethodUpdate) | **PUT** /order/api/v1/manager/{order_uuid}/change-shipping-method/ | تغییر روش ارسال |
| [**orderApiV1ManagerList**](DefaultApi.md#orderApiV1ManagerList) | **GET** /order/api/v1/manager/ | لیست سفارشات |
| [**orderApiV1ManagerPaidList**](DefaultApi.md#orderApiV1ManagerPaidList) | **GET** /order/api/v1/manager/paid/ | سفارش پرداخت‌شده و تایید‌نشده |
| [**orderApiV1ManagerRefundCreate**](DefaultApi.md#orderApiV1ManagerRefundCreate) | **POST** /order/api/v1/manager/{order_uuid}/refund/ | بازگشت سفارش |
| [**orderApiV1ManagerRetrieve**](DefaultApi.md#orderApiV1ManagerRetrieve) | **GET** /order/api/v1/manager/{order_uuid}/ | دریافت سفارش |
| [**orderApiV1ManagerReviveShipmentCreate**](DefaultApi.md#orderApiV1ManagerReviveShipmentCreate) | **POST** /order/api/v1/manager/{order_uuid}/revive-shipment/ | احیای ارسال سفارش |
| [**orderApiV1ManagerUpdateStatusUpdate**](DefaultApi.md#orderApiV1ManagerUpdateStatusUpdate) | **PUT** /order/api/v1/manager/{order_uuid}/update-status/ | به‌روزرسانی وضعیت سفارش |
| [**orderApiV1ManagerVerifyCreate**](DefaultApi.md#orderApiV1ManagerVerifyCreate) | **POST** /order/api/v1/manager/{order_uuid}/verify/ | تایید سفارش |
| [**walletsApiV1WalletBalanceRetrieve**](DefaultApi.md#walletsApiV1WalletBalanceRetrieve) | **GET** /wallets/api/v1/wallet-balance/ | دریافت موجودی کیف پول |


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

val apiInstance = DefaultApi()
try {
    val result : AuthStatusResponse = apiInstance.merchantApiV1AuthStatusRetrieve()
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#merchantApiV1AuthStatusRetrieve")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#merchantApiV1AuthStatusRetrieve")
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

<a id="orderApiV1CreateOrderCreate"></a>
# **orderApiV1CreateOrderCreate**
> OrderCreateResponse orderApiV1CreateOrderCreate(orderCreate)

ساخت سفارش

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  ساخت سفارش جدید در سیستم BWDK  ## توضیحات  این endpoint برای ایجاد یک سفارش جدید در سیستم خرید با دیجی‌کالا استفاده می‌شود. در این درخواست باید اطلاعات سفارش، اقلام سبد خرید، و آدرس callback شامل شود.  برای شروع ارتباط با سرویس‌های **خرید با دیجی‌کالا** شما باید دارای **API_KEY** باشید که این مورد از سمت تیم دیجی‌فای در اختیار شما قرار خواهد گرفت.  ### روند کاری  **مرحله ۱: درخواست ساخت سفارش**  کاربر پس از انتخاب کالاهای خود در سبد خرید، بر روی دکمه **خرید با دیجی‌کالا** کلیک می‌کند و بک‌اند مرچنت درخواستی برای ساخت سفارش BWDK دریافت می‌کند. در این مرحله اولین درخواست خود را به بک‌اند BWDK ارسال می‌نمایید:  BWDK یک سفارش جدید برای مرچنت با وضعیت **INITIAL** ایجاد می‌کند و **order_uuid** را جنریت می‌کند. آدرس **order_start_url** نقطه شروع مسیر تکمیل سفارش است (انتخاب آدرس، شیپینگ، پکینگ، پرداخت و غیره). &lt;br&gt; &lt;/div&gt;  &#x60;&#x60;&#x60;mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant C as مشتری     participant PG as درگاه پرداخت      M-&gt;&gt;API: POST /api/v1/orders/create     Note over M,API: شناسه سفارش, کالاها, مبلغ, callback_url     API--&gt;&gt;M: {لینک شروع سفارش, شناسه سفارش}      M-&gt;&gt;C: تغییر مسیر به لینک شروع      C-&gt;&gt;API: تکمیل درخواست خرید توسط مشتری     API-&gt;&gt;PG: شروع فرآیند پرداخت     PG--&gt;&gt;C: نتیجه پرداخت     PG-&gt;&gt;API: تأیید پرداخت     API--&gt;&gt;C: تغییر مسیر به callback_url      M-&gt;&gt;API: POST /api/v1/orders/manager/{uuid}/verify     Note over M,API: {شناسه منحصربفرد فروشنده}     API--&gt;&gt;M: سفارش تأیید شد و آماده ارسال است &#x60;&#x60;&#x60;  &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val orderCreate : OrderCreate =  // OrderCreate | 
try {
    val result : OrderCreateResponse = apiInstance.orderApiV1CreateOrderCreate(orderCreate)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1CreateOrderCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1CreateOrderCreate")
    e.printStackTrace()
}
```

### Parameters
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **orderCreate** | [**OrderCreate**](OrderCreate.md)|  | |

### Return type

[**OrderCreateResponse**](OrderCreateResponse.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

<a id="orderApiV1ManagerCancelShipmentCreate"></a>
# **orderApiV1ManagerCancelShipmentCreate**
> MerchantOrderCancelShipmentResponse orderApiV1ManagerCancelShipmentCreate(orderUuid)

لغو ارسال سفارش

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  لغو مرسوله دیجی‌اکسپرس  ## توضیحات  این endpoint برای لغو یک مرسوله ثبت‌شده در سرویس دیجی‌اکسپرس استفاده می‌شود. پس از لغو موفق، مرسوله از صف ارسال خارج می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## شرایط لغو  * سفارش باید دارای روش ارسال **DigiExpress** باشد * مرسوله باید در وضعیت **در انتظار تحویل به پیک** (Request for Pickup) باشد  &lt;/div&gt;  &#x60;&#x60;&#x60;mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant DX as دیجی‌اکسپرس      M-&gt;&gt;API: POST /order/api/v1/manager/{order_uuid}/cancel-shipment/     Note over M,API: Header: X-API-KEY (بدون بدنه)      alt روش ارسال DigiExpress نیست         API--&gt;&gt;M: 400 خطا         Note over API,M: {error: \&quot;Selected shipping method is not DigiExpress\&quot;}     else مرسوله قابل لغو نیست         API--&gt;&gt;M: 400 خطا         Note over API,M: {error: \&quot;...\&quot;}     else لغو موفق         API-&gt;&gt;DX: لغو مرسوله         DX--&gt;&gt;API: تأیید لغو         API--&gt;&gt;M: 200 موفق         Note over API,M: {message, order_uuid, status, status_display}     end &#x60;&#x60;&#x60; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
try {
    val result : MerchantOrderCancelShipmentResponse = apiInstance.orderApiV1ManagerCancelShipmentCreate(orderUuid)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1ManagerCancelShipmentCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1ManagerCancelShipmentCreate")
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

تغییر روش ارسال

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  تغییر روش ارسال سفارش  ## توضیحات  این endpoint به فروشنده اجازه می‌دهد روش ارسال یک سفارش را تغییر دهد. این عملیات معمولاً زمانی استفاده می‌شود که فروشنده بخواهد از DigiExpress به روش ارسال پیش‌فرض (یا بالعکس) تغییر دهد.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای ورودی  * **updated_shipping**: شناسه روش ارسال جدید * **preparation_time** (اختیاری): زمان آماده‌سازی (روز) برای DigiExpress  &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val orderDetail : OrderDetail =  // OrderDetail | 
try {
    val result : OrderDetail = apiInstance.orderApiV1ManagerChangeShippingMethodUpdate(orderUuid, orderDetail)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1ManagerChangeShippingMethodUpdate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1ManagerChangeShippingMethodUpdate")
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

<a id="orderApiV1ManagerList"></a>
# **orderApiV1ManagerList**
> PaginatedOrderDetailList orderApiV1ManagerList(cities, createdAt, cursor, orderIds, ordering, paymentTypes, provinces, referenceCode, search, shippingTypes, status, statuses, todayPickup)

لیست سفارشات

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  لیست سفارشات فروشنده  ## توضیحات  این endpoint لیست تمام سفارشات مرتبط با فروشنده را با امکان فیلتر، جستجو و مرتب‌سازی برمی‌گرداند. نتایج به صورت صفحه‌بندی‌شده (Cursor Pagination) ارسال می‌شوند و به ترتیب جدیدترین سفارش اول مرتب می‌شوند.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای فیلتر  * **status**: وضعیت سفارش (INITIAL, PENDING, PAID_BY_USER, VERIFIED_BY_MERCHANT, ...) * **created_at__gte / created_at__lte**: فیلتر بر اساس تاریخ ایجاد * **search**: جستجو در شماره تلفن مشتری، نام، کد مرجع، شناسه سفارش مرچنت * **ordering**: مرتب‌سازی بر اساس created_at, final_amount, status, merchant_order_id  &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val cities : kotlin.String = cities_example // kotlin.String | 
val createdAt : java.time.LocalDate = 2013-10-20 // java.time.LocalDate | 
val cursor : kotlin.String = cursor_example // kotlin.String | مقدار نشانگر صفحه‌بندی.
val orderIds : kotlin.String = orderIds_example // kotlin.String | 
val ordering : kotlin.String = ordering_example // kotlin.String | کدام فیلد باید هنگام مرتب‌سازی نتایج استفاده شود.
val paymentTypes : kotlin.String = paymentTypes_example // kotlin.String | 
val provinces : kotlin.String = provinces_example // kotlin.String | 
val referenceCode : kotlin.String = referenceCode_example // kotlin.String | 
val search : kotlin.String = search_example // kotlin.String | یک عبارت جستجو.
val shippingTypes : kotlin.String = shippingTypes_example // kotlin.String | 
val status : kotlin.Int = 56 // kotlin.Int | * `1` - اولیه * `2` - شروع در * `3` - در انتظار * `4` - در انتظار درگاه * `5` - منقضی شده * `6` - لغو شده * `7` - ممنوع شده توسط ما * `8` - ناموفق در پرداخت * `9` - تأیید شده توسط فروشنده * `10` - ناموفق در تأیید توسط فروشنده * `11` - فروشگاه * `12` - لغو شده توسط فروشنده * `13` - درخواست بازگرداندن وجه به مشتری به دلیل درخواست مشتری * `14` - درخواست بازگرداندن وجه به فروشنده پس از ناموفقی در تأیید توسط فروشنده * `15` - درخواست بازگرداندن وجه به مشتری پس از ناموفقی توسط فروشنده * `16` - بازگردانده شده به فروشنده پس از لغو توسط فروشنده * `17` - بازگرداندن وجه تکمیل شد * `18` - زمان مجاز برای منقضی کردن گذشته است * `19` - تحویل نشده * `20` - مرسوله
val statuses : kotlin.String = statuses_example // kotlin.String | 
val todayPickup : kotlin.Boolean = true // kotlin.Boolean | 
try {
    val result : PaginatedOrderDetailList = apiInstance.orderApiV1ManagerList(cities, createdAt, cursor, orderIds, ordering, paymentTypes, provinces, referenceCode, search, shippingTypes, status, statuses, todayPickup)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1ManagerList")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1ManagerList")
    e.printStackTrace()
}
```

### Parameters
| **cities** | **kotlin.String**|  | [optional] |
| **createdAt** | **java.time.LocalDate**|  | [optional] |
| **cursor** | **kotlin.String**| مقدار نشانگر صفحه‌بندی. | [optional] |
| **orderIds** | **kotlin.String**|  | [optional] |
| **ordering** | **kotlin.String**| کدام فیلد باید هنگام مرتب‌سازی نتایج استفاده شود. | [optional] |
| **paymentTypes** | **kotlin.String**|  | [optional] |
| **provinces** | **kotlin.String**|  | [optional] |
| **referenceCode** | **kotlin.String**|  | [optional] |
| **search** | **kotlin.String**| یک عبارت جستجو. | [optional] |
| **shippingTypes** | **kotlin.String**|  | [optional] |
| **status** | **kotlin.Int**| * &#x60;1&#x60; - اولیه * &#x60;2&#x60; - شروع در * &#x60;3&#x60; - در انتظار * &#x60;4&#x60; - در انتظار درگاه * &#x60;5&#x60; - منقضی شده * &#x60;6&#x60; - لغو شده * &#x60;7&#x60; - ممنوع شده توسط ما * &#x60;8&#x60; - ناموفق در پرداخت * &#x60;9&#x60; - تأیید شده توسط فروشنده * &#x60;10&#x60; - ناموفق در تأیید توسط فروشنده * &#x60;11&#x60; - فروشگاه * &#x60;12&#x60; - لغو شده توسط فروشنده * &#x60;13&#x60; - درخواست بازگرداندن وجه به مشتری به دلیل درخواست مشتری * &#x60;14&#x60; - درخواست بازگرداندن وجه به فروشنده پس از ناموفقی در تأیید توسط فروشنده * &#x60;15&#x60; - درخواست بازگرداندن وجه به مشتری پس از ناموفقی توسط فروشنده * &#x60;16&#x60; - بازگردانده شده به فروشنده پس از لغو توسط فروشنده * &#x60;17&#x60; - بازگرداندن وجه تکمیل شد * &#x60;18&#x60; - زمان مجاز برای منقضی کردن گذشته است * &#x60;19&#x60; - تحویل نشده * &#x60;20&#x60; - مرسوله | [optional] [enum: 1, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 2, 20, 3, 4, 5, 6, 7, 8, 9] |
| **statuses** | **kotlin.String**|  | [optional] |
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **todayPickup** | **kotlin.Boolean**|  | [optional] |

### Return type

[**PaginatedOrderDetailList**](PaginatedOrderDetailList.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

<a id="orderApiV1ManagerPaidList"></a>
# **orderApiV1ManagerPaidList**
> PaginatedMerchantPaidOrderListList orderApiV1ManagerPaidList(cities, createdAt, cursor, orderIds, ordering, paymentTypes, provinces, referenceCode, search, shippingTypes, status, statuses, todayPickup)

سفارش پرداخت‌شده و تایید‌نشده

لیست تمامی سفارشاتی که توسط کاربر پرداخت شده اند ولی توسط فروشنده تایید نشده اند. 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val cities : kotlin.String = cities_example // kotlin.String | 
val createdAt : java.time.LocalDate = 2013-10-20 // java.time.LocalDate | 
val cursor : kotlin.String = cursor_example // kotlin.String | مقدار نشانگر صفحه‌بندی.
val orderIds : kotlin.String = orderIds_example // kotlin.String | 
val ordering : kotlin.String = ordering_example // kotlin.String | کدام فیلد باید هنگام مرتب‌سازی نتایج استفاده شود.
val paymentTypes : kotlin.String = paymentTypes_example // kotlin.String | 
val provinces : kotlin.String = provinces_example // kotlin.String | 
val referenceCode : kotlin.String = referenceCode_example // kotlin.String | 
val search : kotlin.String = search_example // kotlin.String | یک عبارت جستجو.
val shippingTypes : kotlin.String = shippingTypes_example // kotlin.String | 
val status : kotlin.Int = 56 // kotlin.Int | * `1` - اولیه * `2` - شروع در * `3` - در انتظار * `4` - در انتظار درگاه * `5` - منقضی شده * `6` - لغو شده * `7` - ممنوع شده توسط ما * `8` - ناموفق در پرداخت * `9` - تأیید شده توسط فروشنده * `10` - ناموفق در تأیید توسط فروشنده * `11` - فروشگاه * `12` - لغو شده توسط فروشنده * `13` - درخواست بازگرداندن وجه به مشتری به دلیل درخواست مشتری * `14` - درخواست بازگرداندن وجه به فروشنده پس از ناموفقی در تأیید توسط فروشنده * `15` - درخواست بازگرداندن وجه به مشتری پس از ناموفقی توسط فروشنده * `16` - بازگردانده شده به فروشنده پس از لغو توسط فروشنده * `17` - بازگرداندن وجه تکمیل شد * `18` - زمان مجاز برای منقضی کردن گذشته است * `19` - تحویل نشده * `20` - مرسوله
val statuses : kotlin.String = statuses_example // kotlin.String | 
val todayPickup : kotlin.Boolean = true // kotlin.Boolean | 
try {
    val result : PaginatedMerchantPaidOrderListList = apiInstance.orderApiV1ManagerPaidList(cities, createdAt, cursor, orderIds, ordering, paymentTypes, provinces, referenceCode, search, shippingTypes, status, statuses, todayPickup)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1ManagerPaidList")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1ManagerPaidList")
    e.printStackTrace()
}
```

### Parameters
| **cities** | **kotlin.String**|  | [optional] |
| **createdAt** | **java.time.LocalDate**|  | [optional] |
| **cursor** | **kotlin.String**| مقدار نشانگر صفحه‌بندی. | [optional] |
| **orderIds** | **kotlin.String**|  | [optional] |
| **ordering** | **kotlin.String**| کدام فیلد باید هنگام مرتب‌سازی نتایج استفاده شود. | [optional] |
| **paymentTypes** | **kotlin.String**|  | [optional] |
| **provinces** | **kotlin.String**|  | [optional] |
| **referenceCode** | **kotlin.String**|  | [optional] |
| **search** | **kotlin.String**| یک عبارت جستجو. | [optional] |
| **shippingTypes** | **kotlin.String**|  | [optional] |
| **status** | **kotlin.Int**| * &#x60;1&#x60; - اولیه * &#x60;2&#x60; - شروع در * &#x60;3&#x60; - در انتظار * &#x60;4&#x60; - در انتظار درگاه * &#x60;5&#x60; - منقضی شده * &#x60;6&#x60; - لغو شده * &#x60;7&#x60; - ممنوع شده توسط ما * &#x60;8&#x60; - ناموفق در پرداخت * &#x60;9&#x60; - تأیید شده توسط فروشنده * &#x60;10&#x60; - ناموفق در تأیید توسط فروشنده * &#x60;11&#x60; - فروشگاه * &#x60;12&#x60; - لغو شده توسط فروشنده * &#x60;13&#x60; - درخواست بازگرداندن وجه به مشتری به دلیل درخواست مشتری * &#x60;14&#x60; - درخواست بازگرداندن وجه به فروشنده پس از ناموفقی در تأیید توسط فروشنده * &#x60;15&#x60; - درخواست بازگرداندن وجه به مشتری پس از ناموفقی توسط فروشنده * &#x60;16&#x60; - بازگردانده شده به فروشنده پس از لغو توسط فروشنده * &#x60;17&#x60; - بازگرداندن وجه تکمیل شد * &#x60;18&#x60; - زمان مجاز برای منقضی کردن گذشته است * &#x60;19&#x60; - تحویل نشده * &#x60;20&#x60; - مرسوله | [optional] [enum: 1, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 2, 20, 3, 4, 5, 6, 7, 8, 9] |
| **statuses** | **kotlin.String**|  | [optional] |
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **todayPickup** | **kotlin.Boolean**|  | [optional] |

### Return type

[**PaginatedMerchantPaidOrderListList**](PaginatedMerchantPaidOrderListList.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

<a id="orderApiV1ManagerRefundCreate"></a>
# **orderApiV1ManagerRefundCreate**
> MerchantOrderRefundResponse orderApiV1ManagerRefundCreate(orderUuid, refundOrder)

بازگشت سفارش

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt; بازگشت و لغو سفارش  ## توضیحات  این endpoint برای بازگشت یا لغو سفارشی استفاده می‌شود که قبلاً پرداخت شده یا تایید شده است. در این مرحله مبلغ سفارش به کاربر بازگشت داده می‌شود و وضعیت سفارش به **REFUNDED** تغییر می‌یابد.   ## شرایط بازگشت  سفارش باید در یکی از وضعیت‌های زیر باشد تا بازگشت امکان‌پذیر باشد: * **PAID_BY_USER**: سفارش پرداخت شده است اما هنوز تایید نشده * **VERIFIED_BY_MERCHANT**: سفارش تایید شده است  سفارش نباید قبلاً بازگشت داده شده باشد.  **پاسخ خطا** - اگر سفارش در وضعیت مناسب نباشد یا قبلاً بازگشت داده شده باشد &lt;/div&gt;  &#x60;&#x60;&#x60;mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API      M-&gt;&gt;API: POST /api/v1/orders/manager/{uuid}/refund     Note over M,API: {reason: \&quot;درخواست مشتری\&quot;}      alt سفارش قابل بازگشت نیست         API--&gt;&gt;M: 500 خطا         Note over API,M: {error: \&quot;شروع بازگشت ناموفق بود.&lt;br/&gt;لطفاً دوباره تلاش کنید.\&quot;}     else سفارش معتبر است         API--&gt;&gt;M: 200 موفق         Note over API,M: {message: \&quot;درخواست بازگشت با&lt;br/&gt;موفقیت شروع شد\&quot;,&lt;br/&gt;order_uuid, status: 13,&lt;br/&gt;status_display,&lt;br/&gt;refund_reason}          M-&gt;&gt;API: GET /api/v1/orders/manager/{uuid}         Note over M,API: بررسی وضعیت سفارش&lt;br/&gt;(endpoint جداگانه /refund/status وجود ندارد)          alt status: 17 (بازگشت تکمیل شد)             API--&gt;&gt;M: 200 موفق             Note over API,M: {order_uuid, status: 17,&lt;br/&gt;status_display: \&quot;بازگشت تکمیل شد\&quot;,&lt;br/&gt;metadata.refund_tracking_code,&lt;br/&gt;metadata.refund_completed_at}          else status: 13 (در حال پردازش)             API--&gt;&gt;M: 200 موفق             Note over API,M: {order_uuid, status: 13,&lt;br/&gt;status_display: \&quot;درخواست بازگشت به مشتری&lt;br/&gt;به دلیل درخواست&lt;br/&gt;مشتری\&quot;,&lt;br/&gt;metadata.refund_reason}          else status: قبلی (بازگشت ناموفق)             API--&gt;&gt;M: 200 موفق             Note over API,M: {order_uuid, status: (قبلی),&lt;br/&gt;metadata.refund_error,&lt;br/&gt;metadata.refund_failed_at}         end     end &#x60;&#x60;&#x60; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val refundOrder : RefundOrder =  // RefundOrder | 
try {
    val result : MerchantOrderRefundResponse = apiInstance.orderApiV1ManagerRefundCreate(orderUuid, refundOrder)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1ManagerRefundCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1ManagerRefundCreate")
    e.printStackTrace()
}
```

### Parameters
| **orderUuid** | **java.util.UUID**|  | |
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **refundOrder** | [**RefundOrder**](RefundOrder.md)|  | [optional] |

### Return type

[**MerchantOrderRefundResponse**](MerchantOrderRefundResponse.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

<a id="orderApiV1ManagerRetrieve"></a>
# **orderApiV1ManagerRetrieve**
> OrderDetail orderApiV1ManagerRetrieve(orderUuid)

دریافت سفارش

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  # مدیریت سفارشات  ## توضیحات  این endpoint برای مدیریت و مشاهده سفارشات فروشنده استفاده می‌شود.  &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
try {
    val result : OrderDetail = apiInstance.orderApiV1ManagerRetrieve(orderUuid)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1ManagerRetrieve")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1ManagerRetrieve")
    e.printStackTrace()
}
```

### Parameters
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **orderUuid** | **java.util.UUID**|  | |

### Return type

[**OrderDetail**](OrderDetail.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

<a id="orderApiV1ManagerReviveShipmentCreate"></a>
# **orderApiV1ManagerReviveShipmentCreate**
> MerchantOrderReviveShipmentResponse orderApiV1ManagerReviveShipmentCreate(orderUuid, reviveShipment)

احیای ارسال سفارش

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  احیای مرسوله دیجی‌اکسپرس  ## توضیحات  این endpoint برای احیای (reactivate) یک مرسوله دیجی‌اکسپرس که قبلاً لغو شده یا در وضعیت غیرفعال است استفاده می‌شود. با ارسال &#x60;preparation_time&#x60; (زمان آماده‌سازی بر حسب روز)، زمان جدید آماده بودن بار تنظیم می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## پارامترهای ورودی  * **preparation_time** (اختیاری، پیش‌فرض: ۲): تعداد روز تا آماده‌شدن بار برای تحویل به پیک  ## شرایط  * سفارش باید دارای روش ارسال **DigiExpress** باشد * مرسوله باید در وضعیت قابل احیا باشد  &lt;/div&gt;  &#x60;&#x60;&#x60;mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant DX as دیجی‌اکسپرس      M-&gt;&gt;API: POST /order/api/v1/manager/{order_uuid}/revive-shipment/     Note over M,API: Header: X-API-KEY&lt;br/&gt;{preparation_time: 2}      alt روش ارسال DigiExpress نیست         API--&gt;&gt;M: 400 خطا         Note over API,M: {error: \&quot;Selected shipping method is not DigiExpress\&quot;}     else احیا موفق         API-&gt;&gt;DX: احیای مرسوله با زمان جدید         DX--&gt;&gt;API: تأیید احیا         API--&gt;&gt;M: 200 موفق         Note over API,M: {message, order_uuid, status, status_display}     end &#x60;&#x60;&#x60; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val reviveShipment : ReviveShipment =  // ReviveShipment | 
try {
    val result : MerchantOrderReviveShipmentResponse = apiInstance.orderApiV1ManagerReviveShipmentCreate(orderUuid, reviveShipment)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1ManagerReviveShipmentCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1ManagerReviveShipmentCreate")
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

<a id="orderApiV1ManagerUpdateStatusUpdate"></a>
# **orderApiV1ManagerUpdateStatusUpdate**
> OrderDetail orderApiV1ManagerUpdateStatusUpdate(orderUuid, updateOrderStatus)

به‌روزرسانی وضعیت سفارش

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  بروزرسانی وضعیت سفارش  ## توضیحات  این endpoint به فروشنده امکان می‌دهد وضعیت یک سفارش را به‌صورت مستقیم تغییر دهد. این endpoint برای مواردی مانند علامت‌گذاری سفارش به‌عنوان «ارسال شده» یا «تحویل داده شده» توسط فروشنده استفاده می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## وضعیت‌های مجاز  * **DELIVERED**: تحویل شد * **DISPATCHED**: ارسال شد * سایر وضعیت‌های تعریف‌شده در سیستم  &lt;/div&gt;  &#x60;&#x60;&#x60;mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API      M-&gt;&gt;API: PUT /order/api/v1/manager/{order_uuid}/update-status/     Note over M,API: Header: X-API-KEY&lt;br/&gt;{status: \&quot;DELIVERED\&quot;}      alt وضعیت معتبر است         API--&gt;&gt;M: 200 موفق         Note over API,M: اطلاعات کامل سفارش با وضعیت جدید     else وضعیت نامعتبر است         API--&gt;&gt;M: 400 خطا         Note over API,M: {error: \&quot;invalid status\&quot;}     end &#x60;&#x60;&#x60; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val updateOrderStatus : UpdateOrderStatus =  // UpdateOrderStatus | 
try {
    val result : OrderDetail = apiInstance.orderApiV1ManagerUpdateStatusUpdate(orderUuid, updateOrderStatus)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1ManagerUpdateStatusUpdate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1ManagerUpdateStatusUpdate")
    e.printStackTrace()
}
```

### Parameters
| **orderUuid** | **java.util.UUID**|  | |
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **updateOrderStatus** | [**UpdateOrderStatus**](UpdateOrderStatus.md)|  | |

### Return type

[**OrderDetail**](OrderDetail.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

<a id="orderApiV1ManagerVerifyCreate"></a>
# **orderApiV1ManagerVerifyCreate**
> OrderDetail orderApiV1ManagerVerifyCreate(orderUuid, verifyOrder)

تایید سفارش

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  تایید سفارش پس از پرداخت  ## توضیحات  پس از اتمام فرایند پرداخت توسط کاربر، مرچنت باید سفارش را تایید کند. این endpoint برای تایید و نهایی کردن سفارش پس از پرداخت موفق توسط مشتری استفاده می‌شود. در این مرحله مرچنت سفارش را تایید می‌کند و وضعیت سفارش به **VERIFIED_BY_MERCHANT** تغییر می‌یابد.  ## روند کاری  **مرحله ۲: بازگشت کاربر و دریافت نتیجه**  پس از تکمیل فرایند پرداخت (موفق یا ناموفق)، کاربر به آدرس callback_url که هنگام ساخت سفارش ارسال کرده بودید بازگردانده می‌شود. در این درخواست وضعیت سفارش به صورت query parameters ارسال می‌شود:   **Query Parameters:** * **success**: متغیر منطقی نشان‌دهنده موفق یا ناموفق بودن سفارش * **status**: وضعیت سفارش (PAID، FAILED، وغیره) * **phone_number**: شماره تلفن مشتری * **order_uuid**: شناسه یکتای سفارش * **merchant_order_id**: شناسه سفارش در سیستم مرچنت  **مرحله ۳: تایید سفارش در بک‌اند**  سپس شما باید این endpoint را فراخوانی کنید تا سفارش را تایید کنید و اطمینان حاصل کنید که سفارش موفقیت‌آمیز ثبت شده است: &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val verifyOrder : VerifyOrder =  // VerifyOrder | 
try {
    val result : OrderDetail = apiInstance.orderApiV1ManagerVerifyCreate(orderUuid, verifyOrder)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#orderApiV1ManagerVerifyCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#orderApiV1ManagerVerifyCreate")
    e.printStackTrace()
}
```

### Parameters
| **orderUuid** | **java.util.UUID**|  | |
| Name | Type | Description  | Notes |
| ------------- | ------------- | ------------- | ------------- |
| **verifyOrder** | [**VerifyOrder**](VerifyOrder.md)|  | |

### Return type

[**OrderDetail**](OrderDetail.md)

### Authorization


Configure MerchantAPIKeyAuth:
    ApiClient.apiKey["Authorization"] = ""
    ApiClient.apiKeyPrefix["Authorization"] = ""

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

<a id="walletsApiV1WalletBalanceRetrieve"></a>
# **walletsApiV1WalletBalanceRetrieve**
> WalletBalance walletsApiV1WalletBalanceRetrieve()

دریافت موجودی کیف پول

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  موجودی کیف پول فروشنده  ## توضیحات  این endpoint موجودی کیف پول فروشنده را برمی‌گرداند. کیف پول برای پرداخت هزینه ارسال دیجی‌اکسپرس استفاده می‌شود. هنگام ثبت مرسوله دیجی‌اکسپرس، هزینه ارسال به‌صورت خودکار از کیف پول کسر می‌شود.  نیاز به **API_KEY** فروشنده دارد.  &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = DefaultApi()
try {
    val result : WalletBalance = apiInstance.walletsApiV1WalletBalanceRetrieve()
    println(result)
} catch (e: ClientException) {
    println("4xx response calling DefaultApi#walletsApiV1WalletBalanceRetrieve")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling DefaultApi#walletsApiV1WalletBalanceRetrieve")
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

