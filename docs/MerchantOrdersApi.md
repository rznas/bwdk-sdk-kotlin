# MerchantOrdersApi

All URIs are relative to *https://bwdk-backend.digify.shop*

| Method | HTTP request | Description |
| ------------- | ------------- | ------------- |
| [**orderApiV1CreateOrderCreate**](MerchantOrdersApi.md#orderApiV1CreateOrderCreate) | **POST** /order/api/v1/create-order/ | ساخت سفارش |
| [**orderApiV1ManagerList**](MerchantOrdersApi.md#orderApiV1ManagerList) | **GET** /order/api/v1/manager/ | لیست سفارشات |
| [**orderApiV1ManagerPaidList**](MerchantOrdersApi.md#orderApiV1ManagerPaidList) | **GET** /order/api/v1/manager/paid/ | سفارش پرداخت‌شده و تایید‌نشده |
| [**orderApiV1ManagerRefundCreate**](MerchantOrdersApi.md#orderApiV1ManagerRefundCreate) | **POST** /order/api/v1/manager/{order_uuid}/refund/ | بازگشت سفارش |
| [**orderApiV1ManagerRetrieve**](MerchantOrdersApi.md#orderApiV1ManagerRetrieve) | **GET** /order/api/v1/manager/{order_uuid}/ | دریافت سفارش |
| [**orderApiV1ManagerUpdateStatusUpdate**](MerchantOrdersApi.md#orderApiV1ManagerUpdateStatusUpdate) | **PUT** /order/api/v1/manager/{order_uuid}/update-status/ | Update Order Status |
| [**orderApiV1ManagerVerifyCreate**](MerchantOrdersApi.md#orderApiV1ManagerVerifyCreate) | **POST** /order/api/v1/manager/{order_uuid}/verify/ | تایید سفارش |


<a id="orderApiV1CreateOrderCreate"></a>
# **orderApiV1CreateOrderCreate**
> OrderCreateResponse orderApiV1CreateOrderCreate(orderCreate)

ساخت سفارش

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  ساخت سفارش جدید در سیستم BWDK  ## توضیحات  این endpoint برای ایجاد یک سفارش جدید در سیستم خرید با دیجی‌کالا استفاده می‌شود. در این درخواست باید اطلاعات سفارش، اقلام سبد خرید، و آدرس callback شامل شود.  برای شروع ارتباط با سرویس‌های **خرید با دیجی‌کالا** شما باید دارای **API_KEY** باشید که این مورد از سمت تیم دیجی‌فای در اختیار شما قرار خواهد گرفت.  ### روند کاری  **مرحله ۱: درخواست ساخت سفارش**  کاربر پس از انتخاب کالاهای خود در سبد خرید، بر روی دکمه **خرید با دیجی‌کالا** کلیک می‌کند و بک‌اند مرچنت درخواستی برای ساخت سفارش BWDK دریافت می‌کند. در این مرحله اولین درخواست خود را به بک‌اند BWDK ارسال می‌نمایید:  BWDK یک سفارش جدید برای مرچنت با وضعیت **INITIAL** ایجاد می‌کند و **order_uuid** را جنریت می‌کند. آدرس **order_start_url** نقطه شروع مسیر تکمیل سفارش است (انتخاب آدرس، شیپینگ، پکینگ، پرداخت و غیره).  **مرحله ۲: بررسی نهایی سفارش پیش از تأیید**  پس از اینکه مشتری فرآیند پرداخت را تکمیل کرد و به **callback_url** هدایت شد، بک‌اند مرچنت باید پیش از فراخوانی verify، یک‌بار سفارش را دریافت کرده و مبالغ نهایی (شامل هزینه کالاها، شیپینگ، تخفیف‌ها و جمع کل) را با اطلاعات سمت مرچنت تطبیق دهد تا از صحت تراکنش اطمینان حاصل شود.  **مرحله ۳: تأیید سفارش**  پس از تطبیق موفق مبالغ، درخواست verify ارسال می‌شود تا سفارش نهایی و آماده ارسال گردد. &lt;br&gt; &lt;/div&gt;  &#x60;&#x60;&#x60;mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API     participant C as مشتری     participant PG as درگاه پرداخت      M-&gt;&gt;API: POST /api/v1/orders/create     Note over M,API: شناسه سفارش, کالاها, مبلغ, callback_url     API--&gt;&gt;M: {لینک شروع سفارش, شناسه سفارش}      M-&gt;&gt;C: تغییر مسیر به لینک شروع      C-&gt;&gt;API: تکمیل درخواست خرید توسط مشتری     API-&gt;&gt;PG: شروع فرآیند پرداخت     PG--&gt;&gt;C: نتیجه پرداخت     PG-&gt;&gt;API: تأیید پرداخت     API--&gt;&gt;C: تغییر مسیر به callback_url      M-&gt;&gt;API: GET /api/v1/orders/manager/{uuid}     Note over M,API: بررسی نهایی مبالغ سفارش     API--&gt;&gt;M: اطلاعات سفارش (مبالغ، اقلام، وضعیت)      M-&gt;&gt;API: POST /api/v1/orders/manager/{uuid}/verify     Note over M,API: {شناسه منحصربفرد فروشنده}     API--&gt;&gt;M: سفارش تأیید شد و آماده ارسال است &#x60;&#x60;&#x60;  &lt;/div&gt; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = MerchantOrdersApi()
val orderCreate : OrderCreate =  // OrderCreate | 
try {
    val result : OrderCreateResponse = apiInstance.orderApiV1CreateOrderCreate(orderCreate)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling MerchantOrdersApi#orderApiV1CreateOrderCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling MerchantOrdersApi#orderApiV1CreateOrderCreate")
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

val apiInstance = MerchantOrdersApi()
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
val status : kotlin.Int = 56 // kotlin.Int | * `1` - اولیه * `2` - شروع شده * `3` - در انتظار * `4` - در انتظار درگاه * `5` - منقضی شده * `6` - لغو شده * `7` - پرداخت‌شده توسط کاربر * `8` - پرداخت موفیت آمیز نبود * `9` - تأیید شده توسط فروشگاه * `10` - تأیید توسط فروشگاه ناموفق بود * `11` - ناموفق از سوی فروشگاه * `12` - لغوشده توسط فروشگاه * `13` - درخواست بازگشت وجه به مشتری به دلیل درخواست مشتری * `14` - درخواست بازگشت وجه به فروشگاه پس از عدم تأیید توسط فروشگاه * `15` - درخواست بازگشت وجه به مشتری پس از ناموفق بودن توسط فروشگاه * `16` - بازپرداخت به فروشگاه پس از لغو توسط فروشگاه * `17` - بازپرداخت تکمیل شد * `18` - زمان انقضا گذشته است * `19` - تحویل شده * `20` - جمع اوری شده و در حال ارسال
val statuses : kotlin.String = statuses_example // kotlin.String | 
val todayPickup : kotlin.Boolean = true // kotlin.Boolean | 
try {
    val result : PaginatedOrderDetailList = apiInstance.orderApiV1ManagerList(cities, createdAt, cursor, orderIds, ordering, paymentTypes, provinces, referenceCode, search, shippingTypes, status, statuses, todayPickup)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling MerchantOrdersApi#orderApiV1ManagerList")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling MerchantOrdersApi#orderApiV1ManagerList")
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
| **status** | **kotlin.Int**| * &#x60;1&#x60; - اولیه * &#x60;2&#x60; - شروع شده * &#x60;3&#x60; - در انتظار * &#x60;4&#x60; - در انتظار درگاه * &#x60;5&#x60; - منقضی شده * &#x60;6&#x60; - لغو شده * &#x60;7&#x60; - پرداخت‌شده توسط کاربر * &#x60;8&#x60; - پرداخت موفیت آمیز نبود * &#x60;9&#x60; - تأیید شده توسط فروشگاه * &#x60;10&#x60; - تأیید توسط فروشگاه ناموفق بود * &#x60;11&#x60; - ناموفق از سوی فروشگاه * &#x60;12&#x60; - لغوشده توسط فروشگاه * &#x60;13&#x60; - درخواست بازگشت وجه به مشتری به دلیل درخواست مشتری * &#x60;14&#x60; - درخواست بازگشت وجه به فروشگاه پس از عدم تأیید توسط فروشگاه * &#x60;15&#x60; - درخواست بازگشت وجه به مشتری پس از ناموفق بودن توسط فروشگاه * &#x60;16&#x60; - بازپرداخت به فروشگاه پس از لغو توسط فروشگاه * &#x60;17&#x60; - بازپرداخت تکمیل شد * &#x60;18&#x60; - زمان انقضا گذشته است * &#x60;19&#x60; - تحویل شده * &#x60;20&#x60; - جمع اوری شده و در حال ارسال | [optional] [enum: 1, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 2, 20, 3, 4, 5, 6, 7, 8, 9] |
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

val apiInstance = MerchantOrdersApi()
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
val status : kotlin.Int = 56 // kotlin.Int | * `1` - اولیه * `2` - شروع شده * `3` - در انتظار * `4` - در انتظار درگاه * `5` - منقضی شده * `6` - لغو شده * `7` - پرداخت‌شده توسط کاربر * `8` - پرداخت موفیت آمیز نبود * `9` - تأیید شده توسط فروشگاه * `10` - تأیید توسط فروشگاه ناموفق بود * `11` - ناموفق از سوی فروشگاه * `12` - لغوشده توسط فروشگاه * `13` - درخواست بازگشت وجه به مشتری به دلیل درخواست مشتری * `14` - درخواست بازگشت وجه به فروشگاه پس از عدم تأیید توسط فروشگاه * `15` - درخواست بازگشت وجه به مشتری پس از ناموفق بودن توسط فروشگاه * `16` - بازپرداخت به فروشگاه پس از لغو توسط فروشگاه * `17` - بازپرداخت تکمیل شد * `18` - زمان انقضا گذشته است * `19` - تحویل شده * `20` - جمع اوری شده و در حال ارسال
val statuses : kotlin.String = statuses_example // kotlin.String | 
val todayPickup : kotlin.Boolean = true // kotlin.Boolean | 
try {
    val result : PaginatedMerchantPaidOrderListList = apiInstance.orderApiV1ManagerPaidList(cities, createdAt, cursor, orderIds, ordering, paymentTypes, provinces, referenceCode, search, shippingTypes, status, statuses, todayPickup)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling MerchantOrdersApi#orderApiV1ManagerPaidList")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling MerchantOrdersApi#orderApiV1ManagerPaidList")
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
| **status** | **kotlin.Int**| * &#x60;1&#x60; - اولیه * &#x60;2&#x60; - شروع شده * &#x60;3&#x60; - در انتظار * &#x60;4&#x60; - در انتظار درگاه * &#x60;5&#x60; - منقضی شده * &#x60;6&#x60; - لغو شده * &#x60;7&#x60; - پرداخت‌شده توسط کاربر * &#x60;8&#x60; - پرداخت موفیت آمیز نبود * &#x60;9&#x60; - تأیید شده توسط فروشگاه * &#x60;10&#x60; - تأیید توسط فروشگاه ناموفق بود * &#x60;11&#x60; - ناموفق از سوی فروشگاه * &#x60;12&#x60; - لغوشده توسط فروشگاه * &#x60;13&#x60; - درخواست بازگشت وجه به مشتری به دلیل درخواست مشتری * &#x60;14&#x60; - درخواست بازگشت وجه به فروشگاه پس از عدم تأیید توسط فروشگاه * &#x60;15&#x60; - درخواست بازگشت وجه به مشتری پس از ناموفق بودن توسط فروشگاه * &#x60;16&#x60; - بازپرداخت به فروشگاه پس از لغو توسط فروشگاه * &#x60;17&#x60; - بازپرداخت تکمیل شد * &#x60;18&#x60; - زمان انقضا گذشته است * &#x60;19&#x60; - تحویل شده * &#x60;20&#x60; - جمع اوری شده و در حال ارسال | [optional] [enum: 1, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 2, 20, 3, 4, 5, 6, 7, 8, 9] |
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

val apiInstance = MerchantOrdersApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val refundOrder : RefundOrder =  // RefundOrder | 
try {
    val result : MerchantOrderRefundResponse = apiInstance.orderApiV1ManagerRefundCreate(orderUuid, refundOrder)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling MerchantOrdersApi#orderApiV1ManagerRefundCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling MerchantOrdersApi#orderApiV1ManagerRefundCreate")
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

val apiInstance = MerchantOrdersApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
try {
    val result : OrderDetail = apiInstance.orderApiV1ManagerRetrieve(orderUuid)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling MerchantOrdersApi#orderApiV1ManagerRetrieve")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling MerchantOrdersApi#orderApiV1ManagerRetrieve")
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

<a id="orderApiV1ManagerUpdateStatusUpdate"></a>
# **orderApiV1ManagerUpdateStatusUpdate**
> OrderDetail orderApiV1ManagerUpdateStatusUpdate(orderUuid, updateOrderStatus)

Update Order Status

&lt;div dir&#x3D;\&quot;rtl\&quot; style&#x3D;\&quot;text-align: right;\&quot;&gt;  بروزرسانی وضعیت سفارش  ## توضیحات  این endpoint به فروشنده امکان می‌دهد وضعیت یک سفارش را به‌صورت مستقیم تغییر دهد. این endpoint برای مواردی مانند علامت‌گذاری سفارش به‌عنوان «ارسال شده» یا «تحویل داده شده» توسط فروشنده استفاده می‌شود.  نیاز به **API_KEY** فروشنده دارد.  ## وضعیت‌های مجاز  * **DELIVERED**: تحویل شد * **DISPATCHED**: ارسال شد * سایر وضعیت‌های تعریف‌شده در سیستم  &lt;/div&gt;  &#x60;&#x60;&#x60;mermaid sequenceDiagram     participant M as فروشنده     participant API as BWDK API      M-&gt;&gt;API: PUT /order/api/v1/manager/{order_uuid}/update-status/     Note over M,API: Header: X-API-KEY&lt;br/&gt;{status: \&quot;DELIVERED\&quot;}      alt وضعیت معتبر است         API--&gt;&gt;M: 200 موفق         Note over API,M: اطلاعات کامل سفارش با وضعیت جدید     else وضعیت نامعتبر است         API--&gt;&gt;M: 400 خطا         Note over API,M: {error: \&quot;invalid status\&quot;}     end &#x60;&#x60;&#x60; 

### Example
```kotlin
// Import classes:
//import bwdk_sdk.infrastructure.*
//import bwdk_sdk.models.*

val apiInstance = MerchantOrdersApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val updateOrderStatus : UpdateOrderStatus =  // UpdateOrderStatus | 
try {
    val result : OrderDetail = apiInstance.orderApiV1ManagerUpdateStatusUpdate(orderUuid, updateOrderStatus)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling MerchantOrdersApi#orderApiV1ManagerUpdateStatusUpdate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling MerchantOrdersApi#orderApiV1ManagerUpdateStatusUpdate")
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

val apiInstance = MerchantOrdersApi()
val orderUuid : java.util.UUID = 38400000-8cf0-11bd-b23e-10b96e4ef00d // java.util.UUID | 
val verifyOrder : VerifyOrder =  // VerifyOrder | 
try {
    val result : OrderDetail = apiInstance.orderApiV1ManagerVerifyCreate(orderUuid, verifyOrder)
    println(result)
} catch (e: ClientException) {
    println("4xx response calling MerchantOrdersApi#orderApiV1ManagerVerifyCreate")
    e.printStackTrace()
} catch (e: ServerException) {
    println("5xx response calling MerchantOrdersApi#orderApiV1ManagerVerifyCreate")
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

