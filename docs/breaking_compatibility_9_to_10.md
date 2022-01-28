MageSuite 10.0.0 bumps up te following modules:
* *theme-creativeshop* to version ^16.0.0
* *magesuite-content-constructor-admin* to version ^3.0.0 (main change: removed dependency to magesuite-content-constructor module)
* *magesuite-content-constructor-frontend* to version ^4.0.0 (main change: removed dependency to magesuite-content-constructor module)
* *creativestyle/magesuite-frontend* to version ^3.0.0 (main change: removed dependency to magesuite-content-constructor module)
* *magesuite-content-constructor* - removed
* *magesuite-sentry-io* - removed (as deprecated, but package still available OS) 
It introduces compatibility with Magento 2.4.3+ and many other improvements.

###
## **Theme Creativeshop breaking changes**

The following **breaking changes** were introduced in *theme-creativeshop* v16


## - Updated templates (phtml/html) to Magento 2.4.3:

https://github.com/magesuite/theme-creativeshop/commit/5121ab9b7860588a7aaa51cd61b7e94628133f24

Overridden magento templates were update to 2.4.3. Please take a look also on phtml/html templates that are overridden in the project. In order to keep high security level please compare templates with current creativeshop or magento templates and add missing escaping methods.

## - Removed boostrap html select and all the related modules to improve performance:

https://github.com/magesuite/theme-creativeshop/commit/440aaac85abf0391de2cdead0e2c590e1f395a7e

Removed: 
'web/js/vendor/ismobile',
'wev/js/vendor/bootstrap-dropdown',
'web/js/vendor/bootstrap-select',
'components/device-detection'

Boostrap html select implementation was done 4 years ago. The goal was to make visually appealing select on desktops. Nowadays we can see that the implementation affects performance and is against the modern approach - using native browsers functionalities every time it is possible. We can save 55 KiB of minified js and also 250 lines of CSS. 
The only place that can need nicely styled select is magesuite product variants module. To use old select for this module please add import 'components/html-select'; to your pdp.ts entry.
Along with select device-detection script was removed. It added is-touch, is-desktop, is-mobile, is-tablet classes. However, they are very rarely used. Please try some media queries, f.e. @media (hover: hover)

Potential TODOs: 
- Check if categorypage toolbar is displayed properly. 
- If your project uses product-variants include styles as described. 
- If you use magepack, plesae regenerate it or remove bootstrapSelect and bootstrapDropdown from magepack.config.js 

## - Checkout changes:

We removed onepage.phtml overridden file as well as duplicated summary in checkout. Shipping summary has been pulled out from modal. 

https://github.com/magesuite/theme-creativeshop/commit/d1abac1f7a7bf9574bb34cad816841a2c7816cf2
https://github.com/magesuite/theme-creativeshop/commit/d9a61c01a338e460fa9314f7636bf90bb3dc96b7

TODO: Check visual look of checkout, especially on payment step on mobile.

## - Replaced pagination with "load more" button for reviews on PDP

https://github.com/magesuite/theme-creativeshop/commit/6e5acc42be5bd3a997c6e588da1ebae9469c2f32

We changed the implementation according to be up to date with modern UX approach. 

Note: 
If it is desired to have pagination scenario this shall be added to `requirejs-config.js`:
`'Magento_Review/js/process-reviews': { 'Magento_Review/js/process-reviews-ext': false }`
and 
`$reviews_load-more-scenario-enabled: true` changed to `false`  in components/reviews/reviews.scss

## - Add to cart Disabled status:

https://github.com/magesuite/theme-creativeshop/commit/331c70ab1451a014bc27af4c729a075822e71867

We extended add to cart functionallity to make it work even if the button was clicked before scripts initialized.

## - Change of breakpoint utility: 

Breakpoint utility we use acroos the theme has been refactored again. 
Remember - you do not have to use window resize event listeners anymore, to detect specific breakpoint.
Get rid of all window.resize event handlers that are not needed and replace with breakpoint change events (as stated in code comment:)

https://github.com/magesuite/theme-creativeshop/commit/13c54f564db926e5dc0ca985661554b42130927a#diff-2bdaa26e228c1b6a7df3f4175af41b0ac72444f1760a5b4bafa6b3a67f3aa954L32
