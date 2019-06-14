<p align="center">
  <img alt="MageSuite" width="211" src="https://avatars1.githubusercontent.com/u/42670934?s=350&v=4">
</p>

_A Magento 2 extension ecosystem providing UX/performance improvements and many new features._

This is a core metapackage which you should install in order to get MageSuite into your
Magento 2 setup.

## Demo

_A small peek into to available features, this is by no means exaustive._ 

Short video presentation of the __Content Constructor__ feature:

<p align="center">
	<a href="https://vimeo.com/229095695">
  		<img width="350" src="https://i.vimeocdn.com/video/625378407.webp?mw=960&mh=540">
  	</a>
</p>

A demo installation showing the theme can be found [here](https://demo.creativeshop.io).

## Requirements

All of the packages require Magento 2.3.0+.

The whole ecosystem depends on [elasticsuite](http://elasticsuite.io/) and you need 
[elasticsearch](https://www.elastic.co/products/elasticsearch) in order to use it.

All of the frontend features and improvements are implemented in 
[theme-creativeshop](https://github.com/creativestyle/theme-creativeshop). 
You won't be able to take advantage of them if you use __Luma__ or other custom theme.

__WARNING!__ We do not support "easy"/"zip" magento installations. Creativeshop supports
only the [Integrator / composer](https://devdocs.magento.com/guides/v2.2/install-gde/prereq/integrator_install.html)
route.

## Installation

__TIP__ *It's advised you either have __[Elasticsuite](https://github.com/Smile-SA/elasticsuite/wiki/GettingStarted)__
(version 2.7.x) already installed and running. If you don't then this package will install it and you must have 
__elasticsearch__ up and running on `localhost:9200` prior to executing the `setup:upgrade` or it will fail.*

* (optional) [Install Magento](https://devdocs.magento.com/guides/v2.2/install-gde/prereq/integrator_install.html) if you don't have it yet 
* Execute `composer require creativestyle/magesuite ^2.0.0`
* Execute `bin/magento setup:upgrade`
* Build the theme (next chapter)
* Flush Magento cache
* Switch the theme to __Theme Creativeshop__ in admin

## Building theme-creativeshop

MageSuite theme does not rely on Magento for building the assets, instead it uses *gulp*.

Before you start, make sure you have [nodejs](https://nodejs.org/en/) and 
[yarn](https://yarnpkg.com/lang/en/) installed.

__After__ the theme's composer package is installed to your Magento project, execute:

```bash
cd vendor/creativestyle/theme-creativeshop
yarn
yarn build
```

__TIP__ If `yarn` command fails with `guppy-pre-push: Command failed` you need to run `git init` in the theme's 
directory as a workaround and retry `yarn`. A permanent solution is on the way.

It will install the build artifacts into `app/design` subfolder.

After the theme is built, clear your Magento cache and you should be able to select it in admin.

Brought to life by<br/>
<a href="https://creativestyle.de">
	<img src="http://www.creativestyle.pl/wp-content/uploads/2014/04/CS-logo-red-creativestyle-gmbh-sp-z-o-o-interactive-agency-krakow-munchen-logo.png" width="150"/>
</a>