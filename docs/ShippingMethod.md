
# ShippingMethod

## Properties
| Name | Type | Description | Notes |
| ------------ | ------------- | ------------- | ------------- |
| **id** | **kotlin.Int** |  |  [readonly] |
| **name** | **kotlin.String** | نام روش ارسال |  |
| **getShippingTypeDisplay** | **kotlin.String** |  |  [readonly] |
| **shippingTypeDisplay** | **kotlin.String** |  |  [readonly] |
| **deliveryTimeDisplay** | **kotlin.String** |  |  [readonly] |
| **deliveryTimeRangeDisplay** | [**DeliveryTimeRangeDisplay**](DeliveryTimeRangeDisplay.md) |  |  [readonly] |
| **inventoryAddress** | [**BusinessAddress**](BusinessAddress.md) |  |  [readonly] |
| **description** | **kotlin.String** | توضیحات روش ارسال و جزئیات تحویل آن |  [optional] |
| **shippingType** | [**ShippingTypeEnum**](ShippingTypeEnum.md) | نوع روش ارسال: عادی یا دیجی اکسپرس  * &#x60;1&#x60; - سایر * &#x60;2&#x60; - دیجی اکسپرس |  [optional] |
| **cost** | **kotlin.Int** | هزینه ارسال برای منطقه اولیه (مثلاً تهران) به تومان |  [optional] |
| **secondaryCost** | **kotlin.Int** | هزینه ارسال برای مناطق دیگر به تومان |  [optional] |
| **minimumTimeSending** | **kotlin.Int** | حداقل تعداد روزها از تاریخ سفارش تا تحویل |  [optional] |
| **maximumTimeSending** | **kotlin.Int** | حداکثر تعداد روزها از تاریخ سفارش تا تحویل |  [optional] |
| **isPayAtDestination** | **kotlin.Boolean** | Whether the shipping method is pay at destination |  [optional] |



