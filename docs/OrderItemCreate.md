
# OrderItemCreate

## Properties
| Name | Type | Description | Notes |
| ------------ | ------------- | ------------- | ------------- |
| **name** | **kotlin.String** | نام کامل محصول شامل تمام مشخصات |  |
| **count** | **kotlin.Int** | تعداد واحدهای این کالا در سفارش |  |
| **options** | [**kotlin.collections.List&lt;Option&gt;**](Option.md) |  |  |
| **primaryAmount** | **kotlin.Int** | قیمت اولیه برای هر واحد بدون تخفیف (به تومان) |  [optional] |
| **amount** | **kotlin.Int** | قیمت نهایی برای تمام واحدها بعد از تخفیف (به تومان) |  [optional] |
| **discountAmount** | **kotlin.Int** | مبلغ کل تخفیف برای این کالا (به تومان) |  [optional] |
| **taxAmount** | **kotlin.Int** | مبلغ کل مالیات برای این کالا (به تومان) |  [optional] |
| **imageLink** | [**java.net.URI**](java.net.URI.md) | آدرس تصویر محصول |  [optional] |
| **preparationTime** | **kotlin.Int** | زمان آمادهسازی کالا (به روز) |  [optional] |
| **weight** | **kotlin.Double** | وزن کالا (بر حسب گرم) |  [optional] |



