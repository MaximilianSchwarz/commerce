# Running Release Notes for Craft Commerce 3.0

### Added
- Added the ability to create and edit orders from the Control Panel.
- Added GraphQL support for products.
- Added the ability to send emails from the Edit Order page.
- Line items can now be exported from the Order index page.
- Added “Edit Orders” and “Delete Orders” user permissions.
- Line items now have a status that can be changed on the Edit Order page.
- Line items now have a Private Note field for store managers.
- Inactive carts are now purged during garbage collection.
- Orders now have recalculation modes to determine what should be recalculated on the order.
- Added the `origin` order query param.
- `commerce/payments/pay` JSON responses now include an `orderErrors` array if there were any errors on the order.
- Added warnings to settings that are being overridden in the config file.
- Added the ability on promotions to choose the relationship type for related categories.
- Added the ability to add a product to an existing Sale from the Product Edit page.
- Added the ability to set a plain text template for Commerce emails.
- Added the `showCustomerInfoTab` setting to allow control over showing the customer info tab on the User Edit page.
- Added the ability to create discounts using the order total and percentages. 
- Added the ability to sort by shipping and billing first, last and full name on the Orders index page.
- Added the ability to set the title label for Products and Variants per product type.
- Added the ability to enable/disabled countries.
- Added the ability to enable/disabled states.
- Added consolidation of guest orders after an order is completed.
- Added the ability to manager Customers and Customer Addresses.
- Added the ability to show the customer on the Order index table.
- Added the `orderTableDateOrderedFormat` setting to allow format control of date ordered on the order index table.
- Added `craft\commerce\controllers\CountriesController::actionUpdateStatus()`
- Added `craft\commerce\controllers\DiscountsController::actionClearDiscountUses()`
- Added `craft\commerce\controllers\DiscountsController::actionUpdateStatus()`
- Added `craft\commerce\controllers\DiscountsController::DISCOUNT_COUNTER_TYPE_TOTAL`
- Added `craft\commerce\controllers\DiscountsController::DISCOUNT_COUNTER_TYPE_CUSTOMER`
- Added `craft\commerce\controllers\DiscountsController::DISCOUNT_COUNTER_TYPE_EMAIL`
- Added `craft\commerce\controllers\LineItemStatuses`.
- Added `craft\commerce\controllers\OrdersController::_getTransactionsWIthLevelsTableArray()`
- Added `craft\commerce\controllers\OrdersController::actionNewOrder()`.
- Added `craft\commerce\controllers\SalesController::actionUpdateStatus()`
- Added `craft\commerce\controllers\StatesController::actionUpdateStatus()`
- Added `craft\commerce\elements\Order::$origin`.
- Added `craft\commerce\elements\Order::$recalculationMode`.
- Added `craft\commerce\elements\Order::getAdjustmentsByType()`.
- Added `craft\commerce\elements\Order::getCustomerLinkHtml()`.
- Added `craft\commerce\models\Country::$enabled`.
- Added `craft\commerce\models\Customer::getCpEditUrl()`.
- Added `craft\commerce\models\Discount::$totalDiscountUseLimit`.
- Added `craft\commerce\models\Discount::$totalDiscountUses`.
- Added `craft\commerce\models\LineItem::$lineItemStatusId`.
- Added `craft\commerce\models\LineItem::$privateNote`.
- Added `craft\commerce\models\ProductType::$titleLabel`.
- Added `craft\commerce\models\ProductType::$variantTitleLabel`.
- Added `craft\commerce\models\State::$enabled`.
- Added `craft\commerce\queue\ConsolidateGuestOrders`.
- Added `craft\commerce\records\Country::$enabled`.
- Added `craft\commerce\records\LineItemStatus`.
- Added `craft\commerce\records\Purchasable::$description`.
- Added `craft\commerce\records\State::$enabled`.
- Added `craft\commerce\services\Countries::getAllEnabledCountries`.
- Added `craft\commerce\services\Countries::getAllEnabledCountriesAsList`.
- Added `craft\commerce\services\Discounts::clearCustomerUsageHistoryById()`.
- Added `craft\commerce\services\Discounts::clearEmailUsageHistoryById()`.
- Added `craft\commerce\services\Discounts::clearDiscountUsesById()`.
- Added `craft\commerce\services\Discounts::getEmailUsageStatsById()`.
- Added `craft\commerce\services\Discounts::getCustomerUsageStatsById()`.
- Added `craft\commerce\services\Emails::getAllEnabledEmails()`.
- Added `craft\commerce\services\LineItemStatuses::EVENT_DEFAULT_LINE_ITEM_STATUS`.
- Added `craft\commerce\services\LineItemStatuses`.
- Added `craft\commerce\services\States::getAllEnabledStates`.
- Added `craft\commerce\services\States::getAllEnabledStatesAsList`.
- Added `craft\commerce\services\States::getAllEnabledStatesAsListGroupedByCountryId`.
- Added `craft\commerce\services\States::getAllStatesAsListGroupedByCountryId`.

## Changed
- The Edit Order page is now a Vue app. This is likely to break any plugins that use JavaScript to modify the DOM on that page.
- Order status change emails are triggered by a job on the queue for faster checkout.
- If no `donationAmount` line item option parameter is submitted when adding a donation to the cart, the donation amount will default to zero.
- Controller actions now call `craft\commerce\elements\Order::toArray()` when generating the cart array for JSON responses.
- `commerce/payments/pay` JSON responses now list payment form errors under `paymentFormErrors` rather than `paymentForm`.
- Customer records that are anonymous and orphaned are now deleted during garbage collection.
- Changed the default category relationship type on promotions from `sourceElement` to `element` .
- `purgeInactiveCartsDuration` default value is number of seconds as an integer and is now being passed through `craft\cms\helpers\ConfigHelper::durationInSeconds()`.
- `activeCartDuration` default value is number of seconds as an integer and is now being passed through `craft\cms\helpers\ConfigHelper::durationInSeconds()`.
- `craft\commerce\controllers\CustomerAddressesController::actionSave()` no long forces primary shipping and billing addresses if they do not exist.
- Moved `craft\commerce\services\States::getAllStatesAsList` logic to `craft\commerce\services\States::getAllStatesAsListGroupedByCountryId` to be consistent with other service methods. 
- `allowEmptyCartOnCheckout` default value is false.
- `totalDiscountUses` now counts all usage instances of a discount.
- Discount uses for `perUserLimit` and `perEmailLimit` are now counted on every discount use instead of only when a coupon code is used.
- Addresses no longer require a first and last name.
- Clearing discount usage counters is now done on a per counter basis.

## Deprecated
- Deprecated `craft\commerce\elements\Order::getShouldRecalculateAdjustments()` and `setShouldRecalculateAdjustments()`. `craft\commerce\elements\Order::$recalculationMode` should be used instead.
- Deprecated `craft\commerce\serviced\Customers::consolidateOrdersToUser()`. `craft\commerce\queue\ConsolidateGuestOrders` job should be used instead.
- Deprecated `craft\commerce\services\Orders::cartArray()`. `craft\commerce\elements\Order::toArray()` should be used instead.

## Removed
- Removed the Customer Info field type.
- Removed the `craft.commerce.availableShippingMethods` Twig property.
- Removed the `craft.commerce.cart` Twig property.
- Removed the `craft.commerce.countriesList` Twig property.
- Removed the `craft.commerce.customer` Twig property.
- Removed the `craft.commerce.discountByCode` Twig property.
- Removed the `craft.commerce.primaryPaymentCurrency` Twig property.
- Removed the `craft.commerce.statesArray` Twig property.
- Removed the `commerce/cart/remove-all-line-items` action.
- Removed the `commerce/cart/remove-line-item` action.
- Removed the `commerce/cart/update-line-item` action.
- Removed `craft\commerce\base\Purchasable::getPurchasableId()`.
- Removed `craft\commerce\controllers\DiscountsController::actionClearCouponUsageHistory()`.
- Removed `craft\commerce\controllers\DownloadController::actionExportOrder()`.
- Removed `craft\commerce\elements\db\OrderQuery::updatedAfter()`.
- Removed `craft\commerce\elements\db\OrderQuery::updatedBefore()`.
- Removed `craft\commerce\elements\db\SubscriptionQuery::subscribedAfter()`.
- Removed `craft\commerce\elements\db\SubscriptionQuery::subscribedBefore()`.
- Removed `craft\commerce\elements\Order::getOrderLocale()`.
- Removed `craft\commerce\elements\Order::getTotalDiscount()`.
- Removed `craft\commerce\elements\Order::getTotalShippingCost()`.
- Removed `craft\commerce\elements\Order::getTotalTax()`.
- Removed `craft\commerce\elements\Order::getTotalTaxIncluded()`.
- Removed `craft\commerce\elements\Order::updateOrderPaidTotal()`.
- Removed `craft\commerce\elements\Product::getSnapshot()`.
- Removed `craft\commerce\elements\Product::getUnlimitedStock()`.
- Removed `craft\commerce\elements\Variant::getSalesApplied()`.
- Removed `craft\commerce\models\Address::getFullName()`.
- Removed `craft\commerce\models\Discount::$totalUses`.
- Removed `craft\commerce\models\Discount::$totalUseLimit`.
- Removed `craft\commerce\models\Discount::getFreeShipping()`.
- Removed `craft\commerce\models\Discount::setFreeShipping()`.
- Removed `craft\commerce\models\LineItem::fillFromPurchasable()`.
- Removed `craft\commerce\models\Order::getDiscount()`.
- Removed `craft\commerce\models\Order::getShippingCost()`.
- Removed `craft\commerce\models\Order::getTax()`.
- Removed `craft\commerce\models\Order::getTaxIncluded()`.
- Removed `craft\commerce\models\ShippingMethod::$amount`.
- Removed `craft\commerce\services\Countries::getAllCountriesListData()`.
- Removed `craft\commerce\services\Discounts::clearCouponUsageHistoryById()`.
- Removed `craft\commerce\services\Gateways::getAllFrontEndGateways()`.
- Removed `craft\commerce\services\ShippingMethods::getOrderedAvailableShippingMethods()`.
- Removed `craft\commerce\services\Reports::getOrdersExportFile()`.
- Removed `craft\commerce\models\Address::EVENT_REGISTER_ADDRESS_VALIDATION_RULES` event use `craft\base\Model::EVENT_DEFINE_RULES` instead.
- Removed `craft\commerce\services\Reports::EVENT_BEFORE_GENERATE_EXPORT` event. Use `craft\base\Element::EVENT_REGISTER_EXPORTERS` to create your own exports.