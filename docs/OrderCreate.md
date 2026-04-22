
# OrderCreate

## Properties
| Name | Type | Description | Notes |
| ------------ | ------------- | ------------- | ------------- |
| **merchantOrderId** | **kotlin.String** | شناسه منحصر به فرد این سفارش در سیستم فروشنده |  |
| **merchantUniqueId** | **kotlin.String** | شناسه منحصر به فرد برای تأیید اصالت سفارش |  |
| **callbackUrl** | [**java.net.URI**](java.net.URI.md) | آدرس وب‌هوک برای دریافت اطلاع رسانی وضعیت پرداخت |  |
| **destinationAddress** | [**kotlin.Any**](.md) |  |  [readonly] |
| **items** | [**kotlin.collections.List&lt;OrderItemCreate&gt;**](OrderItemCreate.md) |  |  |
| **user** | **kotlin.Int** |  |  [readonly] |
| **referenceCode** | **kotlin.String** | کد مرجع منحصر به فرد برای پیگیری سفارش مشتری (فرمت: BD-XXXXXXXX) |  [readonly] |
| **mainAmount** | **kotlin.Int** | مجموع قیمت‌های اولیه تمام کالاها بدون تخفیف (به تومان) |  [optional] |
| **finalAmount** | **kotlin.Int** | مبلغ نهایی: مبلغ_اصلی - مبلغ_تخفیف + مبلغ_مالیات (به تومان) |  [optional] |
| **totalPaidAmount** | **kotlin.Int** | مبلغ کل پرداخت شده توسط کاربر: مبلغ_نهایی + هزینه_ارسال (به تومان) |  [optional] |
| **discountAmount** | **kotlin.Int** | مبلغ کل تخفیف برای تمام سفارش (به تومان) |  [optional] |
| **taxAmount** | **kotlin.Int** | مبلغ کل مالیات برای تمام سفارش (به تومان) |  [optional] |
| **shippingAmount** | **kotlin.Int** | هزینه ارسال برای سفارش (به تومان) |  [optional] |
| **loyaltyAmount** | **kotlin.Int** | مبلغ تخفیف باشگاه مشتریان/پاداش (به تومان) |  [optional] |
| **merchant** | **kotlin.Int** | مقدار توسط سیستم جایگذاری می شود |  [optional] |
| **sourceAddress** | [**kotlin.Any**](.md) | مقدار توسط سیستم جایگذاری می شود |  [optional] |
| **reservationExpiredAt** | **kotlin.Int** | مهلت پرداخت (به عنوان Unix timestamp) قبل از اتمام سفارش |  [optional] |
| **preparationTime** | **kotlin.Int** | زمان آمادهسازی سفارش (به روز) |  [optional] |
| **weight** | **kotlin.Double** | وزن کل سفارش (بر حسب گرم) |  [optional] |



