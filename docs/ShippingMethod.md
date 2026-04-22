
# ShippingMethod

## Properties
| Name | Type | Description | Notes |
| ------------ | ------------- | ------------- | ------------- |
| **id** | **kotlin.Int** |  |  [readonly] |
| **name** | **kotlin.String** | نام روش/گزینه بسته‌بندی |  |
| **getShippingTypeDisplay** | **kotlin.String** |  |  [readonly] |
| **shippingTypeDisplay** | **kotlin.String** |  |  [readonly] |
| **deliveryTimeDisplay** | **kotlin.String** |  |  [readonly] |
| **deliveryTimeRangeDisplay** | [**DeliveryTimeRangeDisplay**](DeliveryTimeRangeDisplay.md) |  |  [readonly] |
| **inventoryAddress** | [**BusinessAddress**](BusinessAddress.md) |  |  [readonly] |
| **description** | **kotlin.String** | شناسه روش ارسال برای استفاده در سفارش |  [optional] |
| **shippingType** | [**ShippingTypeEnum**](ShippingTypeEnum.md) | شناسه وضعیت ارسال از دیجی اکسپرس  * &#x60;1&#x60; - سایر * &#x60;2&#x60; - دیجی اکسپرس |  [optional] |
| **cost** | **kotlin.Int** | هزینه ارسال برای منطقه اصلی (مثلاً تهران) به تومان |  [optional] |
| **secondaryCost** | **kotlin.Int** | هزینه ارسال برای مناطق دیگر به تومان |  [optional] |
| **minimumTimeSending** | **kotlin.Int** | حداقل تعداد روز از تاریخ سفارش تا تحویل |  [optional] |
| **maximumTimeSending** | **kotlin.Int** | Maximum number of days from order date to delivery |  [optional] |
| **isPayAtDestination** | **kotlin.Boolean** | آیا روش ارسال پرداخت در مقصد است |  [optional] |



