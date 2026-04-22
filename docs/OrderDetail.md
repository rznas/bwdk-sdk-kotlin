
# OrderDetail

## Properties
| Name | Type | Description | Notes |
| ------------ | ------------- | ------------- | ------------- |
| **id** | **kotlin.Int** |  |  [readonly] |
| **createdAt** | [**java.time.OffsetDateTime**](java.time.OffsetDateTime.md) |  |  [readonly] |
| **orderUuid** | [**java.util.UUID**](java.util.UUID.md) |  |  [readonly] |
| **reservationExpiredAt** | **kotlin.Int** | Unix timestamp تا زمانی که سفارش برای پرداخت رزرو شده است |  [readonly] |
| **merchantOrderId** | **kotlin.String** | شناسه منحصر به فرد سفارش در سیستم فروشنده |  [readonly] |
| **status** | [**OrderStatusEnum**](OrderStatusEnum.md) |  |  [readonly] |
| **statusDisplay** | **kotlin.String** |  |  [readonly] |
| **mainAmount** | **kotlin.Int** | مجموع قیمت اولیه تمام کالاهای سفارش بدون تخفیف (به تومان) |  [readonly] |
| **finalAmount** | **kotlin.Int** | قیمت نهایی قابل پرداخت توسط مشتری: مبلغ_اصلی - مبلغ_تخفیف + مبلغ_مالیات (به تومان) |  [readonly] |
| **totalPaidAmount** | **kotlin.Int** | مبلغ کل پرداخت شده توسط کاربر: مبلغ_نهایی + هزینه_ارسال (به تومان) |  [readonly] |
| **discountAmount** | **kotlin.Int** | مبلغ کل تخفیف اعمال شده بر سفارش (به تومان) |  [readonly] |
| **taxAmount** | **kotlin.Int** | مبلغ کل مالیات برای سفارش (به تومان) |  [readonly] |
| **shippingAmount** | **kotlin.Int** | هزینه ارسال برای سفارش (به تومان) |  [readonly] |
| **loyaltyAmount** | **kotlin.Int** | مقدار تخفیف از برنامه باشگاه مشتریان/پاداش (به تومان) |  [readonly] |
| **callbackUrl** | [**java.net.URI**](java.net.URI.md) | آدرسی برای دریافت اطلاع رسانی وضعیت پرداخت پس از تکمیل سفارش |  [readonly] |
| **merchant** | [**Merchant**](Merchant.md) |  |  |
| **items** | [**kotlin.collections.List&lt;OrderItemCreate&gt;**](OrderItemCreate.md) |  |  |
| **sourceAddress** | [**kotlin.Any**](.md) |  |  [readonly] |
| **destinationAddress** | [**kotlin.Any**](.md) |  |  [readonly] |
| **selectedShippingMethod** | [**ShippingMethod**](ShippingMethod.md) |  |  [readonly] |
| **shippingSelectedAt** | [**java.time.OffsetDateTime**](java.time.OffsetDateTime.md) |  |  [readonly] |
| **addressSelectedAt** | [**java.time.OffsetDateTime**](java.time.OffsetDateTime.md) |  |  [readonly] |
| **packingAmount** | **kotlin.Int** | هزینه روش بسته‌بندی انتخاب‌شده (به تومان) |  [readonly] |
| **packingSelectedAt** | [**java.time.OffsetDateTime**](java.time.OffsetDateTime.md) |  |  [readonly] |
| **selectedPacking** | [**Packing**](Packing.md) |  |  [readonly] |
| **canSelectPacking** | **kotlin.Boolean** |  |  [readonly] |
| **canSelectShipping** | **kotlin.Boolean** |  |  [readonly] |
| **canSelectAddress** | **kotlin.Boolean** |  |  [readonly] |
| **canProceedToPayment** | **kotlin.Boolean** |  |  [readonly] |
| **isPaid** | **kotlin.Boolean** |  |  [readonly] |
| **user** | [**OrderUser**](OrderUser.md) |  |  [readonly] |
| **payment** | [**PaymentOrder**](PaymentOrder.md) |  |  [readonly] |
| **preparationTime** | **kotlin.Int** | Preparation time for the order (in days) |  [readonly] |
| **weight** | **kotlin.Double** | Total weight of the order (in grams) |  [readonly] |
| **selectedShippingData** | [**kotlin.collections.Map&lt;kotlin.String, kotlin.Any&gt;**](kotlin.Any.md) |  |  [readonly] |
| **referenceCode** | **kotlin.String** | کد مرجع یکتا برای پیگیری سفارش مشتری (قالب: BD-XXXXXXXX) |  [readonly] |
| **promotionDiscountAmount** | **kotlin.Double** |  |  [readonly] |
| **promotionData** | [**kotlin.collections.Map&lt;kotlin.String, kotlin.Any&gt;**](kotlin.Any.md) |  |  [readonly] |
| **digipayMarkupAmount** | **kotlin.Int** | Markup amount for the order (in Tomans) |  [readonly] |
| **markupCommissionPercentage** | **kotlin.Int** | Markup commission percentage for the order (in percent) |  [readonly] |
| **previousStatus** | [**OrderStatusEnum**](OrderStatusEnum.md) |  |  [readonly] |
| **previousStatusDisplay** | **kotlin.String** |  |  [readonly] |



