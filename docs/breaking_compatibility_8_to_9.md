MageSuite 9.0.0 bumps up *theme-creativeshop* to v15.0.0 introducing compatibility with Magento 2.4.2+ and many other improvements


## Theme Creativeshop breaking changes
The following **breaking changes** were introduced in *theme-creativeshop* since version v12.0.0

## v15.0.0
[refactor(page-scroll)!: P2G-1610 To the top jumpmark missing](https://github.com/magesuite/theme-creativeshop/commit/1c938c448cb36ae999315b900977fc7aa4d357a4)

We refactored page-scroll component to make it more performant and cleaner. 
Also, we moved page-scroll template to magesuite-theme-helers module instead of the theme to get rid of new custom templates. 
If page-scroll was used in the child theme, it should be checked. 


## v14.0.0
[refactor!: [KRG-1864] Remove address-autofill and google-address-detector components](https://github.com/magesuite/theme-creativeshop/commit/c2e2b2ce8d09a477d61fe12d0f68885afabbba5d)

Due to issues with autofill tools, we decided to get rid of this custom address autofill implementation.
Following components have been removed from theme-creativeshop:

google-address-detector
address-autofill

As address autofill was the last feature that used the following file
`src/Magento_Checkout/web/js/checkout-customizations.js`
we removed it entirely, as well as it's initialization, so if there was any extension of this in child theme,
it won't work anymore. [Related commit]


## v13.0.0
[feat(header): [MGS-4289] Switch from fixed to real sticky header positioning](https://github.com/magesuite/theme-creativeshop/commit/ba579d68acd91ab785cb7809a0a4774f7f4ca6d6)

In order to allow more flexibility we switched from fixed positioning to css sticky.
This MR changes the positioning of a header, therefore child projects have to be reviewed and adjusted
especially if project contains some elements on top of the header on mobile/tablets.

When you update you should: 
- Check scrolling header on mobile/tablet
- Check offcanvass elements opening, before/after scrolling.
- Check scrolling behaviour if project uses salebar widget or any widget on top of the header.

Check below variables, they might be useful to properly position the page-content and the header:
- $header_sticky-top-position-mobile
- $header_sticky-top-position-tablet
- $sticky-header-page-wrapper-offset-mobile
- $sticky-header-page-wrapper-offset-tablet

[fix(breakpoint-util): Move util to separate entry and include on every page](https://github.com/magesuite/theme-creativeshop/commit/5abcd5b1f4aba4b882c04528008edc359a803269)
We refactored breakpoint utility and included it separately on every page. 
It should be used directly from `window.breakpoint`. All the imports of this util should be removed. 

## v12.0.0

[feat!: Container component cleanup](https://github.com/magesuite/theme-creativeshop/commit/3e48d228eb28de0bc12bf30efe4053c962bc6f28)
We've cleaned up most of the container styles, moving declarations to the components that are related to them, instead of one global container component. 

[feat! Comment out optional entries //to not include components that are not really needed](https://github.com/magesuite/theme-creativeshop/commit/f175bd9a6ea64b2d3e49c3d63499a30d326f1cfa)
We've removed some components from entries, to not include them by default, as not every feature is used/installed or needed. `Check entries/*`

[fix!: [LED-2444] Fix product tile gallery images size](https://github.com/magesuite/theme-creativeshop/commit/b9be48ed6274d025772984e8d4798adb7c0a7c4c)
We've optimized product tile gallery feature seo-wise. tile-gallery component is no longer imported in entries by default. 

[feat! (optional-ie-support): [MGS-4208] Move all styles for .ie11 html class to a separate file](https://github.com/magesuite/theme-creativeshop/commit/6ef52830be311f021a02cce390c0792e2bc6291b)

[feat!: Remove unused blank theme styles](https://github.com/magesuite/theme-creativeshop/commit/ff60910fc67852ddaa3c86fe749d8382f1fb0da7)
We got rid of default blank theme styles by overwriting

[fix!: [GNP-707] Fix removing agreements in order to keep native Magento before-place-order component](https://github.com/magesuite/theme-creativeshop/commit/582f0004fd250a14277026af59b61dfe75b6e1b3)
We got rid of our implementation of checkout agreements in favor of Magento one

[feat!: [LP-979] Add elastic offcanvas filters](https://github.com/magesuite/theme-creativeshop/commit/d97b743c143d6b75ac0b9f9eb648f4c0d0e54aaa)
We introduced a possibility of placing category/search results page filters in offcanvas

