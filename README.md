# Hyva Cart State Lookup

## Introduction

This module uses google maps places (autocomplete) API to find the State for a given ZIP.

The result is cached within the browser localStorage, thus limiting the usage of the API for repeat lookups.

** NOTE: This was built for (and locked down to) USA zip lookups, which was my need. The cache is already built for country based caches, however the lookup data parsing, and form fields population will need adjustment for other countries. MR's welcomed. 



https://user-images.githubusercontent.com/4994260/187010277-39f541e3-8f6b-4a9d-ae1e-dffb734ab616.mp4



## Requirements

* Hyva Theme for Magento >= 1.1.17 (Uses the SSR cart code)

## Install

* composer config repositories.github.repo.repman.io composer https://github.repo.repman.io
* composer require proxiblue/module-state-lookup
* ./bin/magento setup:upgrade
* ./bin/magento setup:di:compile

## Configuration

NOTE: I use this module with [ShipperHQ Address Autocomplete](https://github.com/shipperhq/module-address-autocomplete) already installed, which already has a config value for the required google API key. Since I did not want multiple configs for the API key, this module shares the API key config value of that module.

**There is no dependency on the shipperHQ module, this module will effect the same config setup in admin, if the shipperHQ module is not installed**

* Once installed, go to Stores > Configuration > Sales > Shipping Settings
* Enter the Google API Key

## Usage

Once install and activated, enter a Zip into the required field on cart Shipping lookup, and the State will be auto-filled

## Theme changes

This module overrides the core Hyva theme file: ```php-cart/shipping.phtml``` so, if you have customizations in that file, you will need to merge that with this modules version of the template

Main things to note:

* move Zip input above Region input
* add ```x-bind:data-code="region.code"``` to region_id select element
* add ```@keyup.debounce="zipLookup($event.target.value)"``` to zip element
* ```zipLookup``` and ```setStateByCode``` functions in javascript
