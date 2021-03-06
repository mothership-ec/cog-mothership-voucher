# Changelog

## 2.3.0

- E-voucher notification sent on order creation instead of voucher creation
- Added `Exception` namespace
- Added `Exception\VoucherDisplayException` for relaying information back to the user when there is an error
- Added `Exception\EVoucherSendException` for displaying errors to users when an e-voucher could not be sent
- Added `EventListener\EVoucherListener::sendEVoucherOnOrderComplete()` method to send e-vouchers when the `Order\Events::CREATE_COMPLETE` event is fired, assuming that there is a voucher on the order and e-vouchers are enabled
- Deprecated `EventListener\EVoucherListener::sendEVoucher()` method in favour of `EventListener\EVoucherListener::sendEVoucherOnOrderComplete()`
- Add user object to voucher authorship on voucher generation generated from an order and not instance of `Message\User\AnonymousUser` or null
- Resolve issue where `Validator::getError()` would fail when checking currency if there is no order
- Added `ms.voucher.evoucher.error.email` translation string for flash message when an e-voucher cannot be sent, takes a `%code%` parameter for the voucher code
- Update `Cog` dependency to 4.13
- Added `.travis.yml` file

## 2.2.2

- Resolve issue where unwanted characters would appear in voucher codes
- Increased Cog dependency to 4.11

## 2.2.1

- URL encode voucher ID when redirecting from search
- URL encode voucher ID when redirecting to newly created voucher page

## 2.2.0

- Refactored `Loader` to only run one query when loading vouchers
- Added second `$returnAsArray` parameter to `Loader::getByID()` to ensure that vouchers are always returned as an array if set to true. Defaults to false,
- Added private `_setQueryBuilder()` method to `Loader` for instanciating query builder with query set up to load vouchers
- Switched `Loader::_load()` method to private, as it was erroneously declared as public. **NOTE:** This is not considered a BC break as this was a bug, however, if you relied on this method your application will break. Use `Loader::getByID()` instead.
- `voucher.e_voucher.mailer` service is no longer a singleton
- Renamed `Mailer\AbstractMailer::Send()` to `Mailer\AbstractMailer::send()`
- Refactored check for epos vouchers in `EventListener\EVoucherListener`
- Amended docblock for `IdGenerator::__construct()`
- Removed `ms.epos.sale.modal` routes, moved to EPOS module
- Removed addition of `Voucher\EventListener\ReceiptCreateListener` to events, moved to EPOS module
- `voucher.form.epos.search` service triggers a deprecated error, replaced with `epos.form.voucher.search` in EPOS module
- `voucher.form.epos.apply` service triggers a deprecated error, replaced with `epos.form.voucher.apply` in EPOS module
- `voucher.form.epos.remove` service triggers a deprecated error, replaced with `epos.form.voucher.remove` in EPOS module
- Removed extension of `epos.tender.methods` service, the voucher tender method is now added within the EPOS module
- Removed extension of `receipt.templates` service, the voucher receipt template is now added within the EPOS module
- Deprecated `EventListener\ReceiptCreateListener`, use `Message\Mothership\Epos\EventListener\VoucherReceiptListener` in EPOS module instead
- Deprecated `Form\Epos\VoucherApply`, use `Message\Mothership\Epos\Form\Voucher\VoucherApply` in EPOS module instead
- Deprecated `Form\Epos\VoucherRemove`, use `Message\Mothership\Epos\Form\Voucher\VoucherRemove` in EPOS module instead
- Deprecated `Form\Epos\VoucherSearch`, use `Message\Mothership\Epos\Form\Voucher\VoucherSearch` in EPOS module instead
- Deprecated `Receipt\VoucherGenerated`, use `Message\Mothership\Epos\Receipt\Template\VoucherGenerated` in EPOS module instead
- Deprecated `Receipt\VoucherUsage`, use `Message\Mothership\Epos\Receipt\Template\VoucherUsage` in EPOS module instead
- Deprecated `TenderMethod\Voucher`, use `Message\Mothership\Epos\TenderMethod\Voucher` in EPOS module instead
- `resources/assets/js/epos.js` file logs a deprecated error message, use `voucher.js` file in EPOS module instead

## 2.1.2

- Fix issue where vouchers with slashes and dots in the voucher code would break the URLs in the admin panel (note: vouchers theoretically *shouldn't* have these characters, see <a href="https://github.com/mothership-ec/cog/issues/449">this issue</a>)

## 2.1.1

- Fix issue where EPOS orders would break on voucher validation by passing validator the epos order

## 2.1.0

- Electronic vouchers
- Voucher generation checks voucher product type as well as product IDs set in the config

## 2.0.0

- Initial open sourced release
