MageSuite 11.0.0 bumps up te following modules:
* *theme-creativeshop* to version ^17.0.0
* *magesuite-product-tile* to version ^2.0.0
* *magesuite-content-constructor-admin* to version ^4.0.0
* *magesuite-content-constructor-frontend* to version ^5.0.0
* *magesuite-product-positive-indicators* to version ^3.0.0
* *magesuite-daily-deal* to version ^2.0.0
* *magesuite-navigation* to version ^2.0.0
* **magesuite-navigation-mega-dropdown* to version ^2.0.0
* **magesuite-quick-reorder* to version ^2.0.0

> \* These modules are optional, not included in core metapackage

It rewrites some frontend components (f.e. image-teaser, product carousel, tile) in order to remove heavy third party libraries and improve frontend performance. 
It also introduces new features and improvements.

## **Theme Creativeshop breaking changes**

The following **breaking changes** were introduced in *theme-creativeshop* v17

### Next-gen Carousels, Grids, Teasers and Tiles
https://github.com/magesuite/theme-creativeshop/commit/ed89941f4e56ddb4e8938241b0b42ae3f6c910d3
The reasons for rewriting some CMS components were to improve performance, reduce amount of code, especially third-party scripts and start to use widely supported new browser features.

## New higher level slider component
The goal was to remove Swiper library in favour of native scrolling with some custom js enhancement (f.e. pagination, navigation, autorotation, slides grouping). New higher level component was introduced:

Main slider component files added: 
```
'components/_slider/slider.ts'
'components/_slider/interface.ts'
'components/_slider/index.ts'
'components/_slider/mixin.scss'
'components/_slider/hooks.scss'
```

Slider subcomponents folders added: 
```
'components/_slide/autorotation
'components/_slide/navigation
'components/_slide/pagination
```
### Next-gen teasers
This release introduces a refactor for slider-based components, like image-teasers and products-carousels, as well as the new structure and architecture for product tile. It gets rid of a Swiper library, replacing JS-based slider with modern CSS solutions and simplyfing product-tile. Next-gen image teasers introduc native lazy laoding instead of script lazy-laoding, native aspect-ratio instead of padding hack. Html elements were reduced and semantic of code was improved in order to make teasers accessible for screen readers and keyboard .

Breaking changes:
* Rewritten CSS, reduced number of variables.
* Removed some hotspots due to `structural HTML changes`.
* Structural changes: `better semantics`, some code was moved to other places
* Padding hack was replaced by inline style (`aspect-ratio`)
* Changed approach of `collecting JS options` and passing them
* `4-in-row image teasers` on tablets is now 2-in-row.
* `Dynamic fonts scaling` was removed.
* `Endless loop` sliding is no longer supported
* Swiper based `breakpoints` are removed. Breakpoints are now covered in CSS and should be modified there as well
* Swiper based `SpaceBetween` option is removed, use CSS's gap instead
* Swiper based `centeredSlides` (JS option). Covered in CSS (scroll-snap)
* Swiper based `callbacks` are no longer in use. Extend magesuite slider class in order tp introduce new custom functionalities.

Removed: 
```
'web/js/vendor/ismobile'
'wev/js/vendor/bootstrap-dropdown'
'web/js/vendor/bootstrap-select'
'components/device-detection'
```

> **Potential TODOs:**
> \- Check new teasers configuration in `etc/view.xml` 
> \- Check new variables and rewritten `image-teaser.scss` file
> \- Remove any code dependant on Swiper library

### Next-gen product carousel

Carousel ar now based on magesuite `_slider` component.

> **Potential TODOs:**
> \- Check new products carousel configuration in `etc/view.xml`. 
> \- Check new variables and rewritten `products-carousel.scss` file 

### Next-gen grid
Script for setting proper position of teaser in grid has been removed. Instead of it, inline CSS generated in the templayte has been introduced introduced.

> **Potential TODOs:**
> \- Check new variables and rewritten products-carousel.scss file 

### Brand carousel
As all carousels brand carousel is now based on magesuite `_slider` component. Config in etc/view.xml follows the same patterns as can be found in other carousels

### Icon component
As all carousels icon component is now based on magesuite `_slider` component. Config in etc/view.xml follows the same patterns as can be found in other carousels

### Products carousel in offcanvas minicart
As all carousels products carousel in minicart offcanvas is now based on magesuite `_slider` component. Its columns setting can be defined in `etc/view.xml`: `Magento_Checkout/minicart_offcanvas/products_carousel/js/columnsConfig`

### Next-gen product tile
In order to combine product tile with new carousel and grid refactor of product tiles was needed. Due to CSS properties introduced in new carousel technology there cannot be overflowing elements across all states of its children elements. Changes that are happening on product tile during mouse hovers must happen within the bounding box of the element. There are 2 built-in hover scenarios that can be introduced.

Previously, because of list view requirement (quite different layout than on grid view) some tile elements very duplicated in the magesuite-product-tile/view/frontend/layout/product_tile.xml. As now tile content is based on CSS grid layout duplicated content is not needed anymore. Every block with name="product.tile.XXX.list" name was removed.

**Breaking changes:**
* HTML Structure has been rewritten
* List view style tile is optional component now. All its styles are moved to `components/product-tile-list`.
* The tile is divided into 2 main parts: thumbnail and content. All children elements of content are placed directly inside it and distributed by CSS `grid-template-areas`
* All sass variables with pattern `$product-tile-grid_XXXX` were changed into `$product-tile_XXXX`
* Product tile keeps its own aspect ratio - padding hack was removed

> **Potential TODOs:**
> \- Check html structure of product tile and align
> \- Check new variables and rewritten product-tile.scss and product-tile-list.scss files
> \- Import optional product-tile-list component for list view

### Video teasers
https://github.com/magesuite/theme-creativeshop/commit/6ba732108cf2e0bd1b5c2aed54cf42ac23adab3a

With the current release the MageSuite slider based CC components allow displaying both image assets as well as video assets. The video assets can be displayed using autoplay. The video will play once the image teaser is visible on the page and pause when the customer scrolls the page and image teaser is no longer visible. The sound is muted and the player GUI is hidden.

The component allows using video assets via:
- uploading a .mp4 file to Magento 2 media explorer 
- providing a video URL while the video is hosted on YouTube
- providing a video URL while the video is hosted on Vimeo 
- providing a video URL while the video is hosted on Facebook

Video autoplay has built-in support for Consent Management (Usercentrics and Amasty). The consent for one of YouTube Video, Vimeo or Facebook Videos is required in order to load that specific third-party player. Consents can be added or changed by the developer. Videos uploaded to Magento 2 media explorer don't need consent and will always autoplay.

> check consent configuration in `etc/view.xml`

If no Consent Management tool is used or the user didn't accept the consent for a specific video player, the video won't play and the image will be displayed as a fallback. This default behavior can be changed by the developer (meaning all videos will play even if the user didn't accept any consent).

New higher level video component files added: 
'components/_video/players',
'components/_video/utils',
'components/_video/interfaces.ts',

### Content Constructor Admin - Custom CC Components
That's a feature that was requested many times by OpenSource community.

Breaking change has been introduced in `creativestyle/magesuite-content-constructor-admin` module, since assets needs to be build dynamically now.
Refer to https://github.com/magesuite/content-constructor-admin/blob/4.x/README.md for details.