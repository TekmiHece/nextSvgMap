# svgmap-next

svgmap-next is a JavaScript library that lets you easily create an interactable world map comparing customizable data for each country. It's a Webpack-compatible adaptation of the original [svgMap](https://github.com/StephanWagner/svgMap) by Stephen Wagner.

## Install

```bash
yarn add svgmap-next
```

## Webpack Usage

```html
<div id="map"></div>
```

```javascript
import svgmap from 'svgmap-next'

const map = new svgmap({
  element: document.getElementById('map'),
  data: {
    data: {
      gdp: {
        name: 'GDP per capita',
        format: '{0} USD',
        thousandSeparator: ',',
        thresholdMax: 50000,
        thresholdMin: 1000
      },
      change: {
        name: 'Change to year before',
        format: '{0} %'
      }
    },
    applyData: 'gdp',
    values: {
      AF: {gdp: 587, change: 4.73},
      AL: {gdp: 4583, change: 11.09},
      DZ: {gdp: 4293, change: 10.01}
    }
  }
})

// later on, before leaving the page, eg. `turbolinks:before-cache`

map.unload()
```

## Options

You can pass the following options into svgMap:

* `element` (`DOMElement`) The element where the world map will render (Required)

* `minZoom`, `maxZoom` (`float`) Minimal and maximal zoom level. Default: `1` for `minZoom`, `25` for `maxZoom`

* `initialZoom` (`float`) Initial zoom level. Default: `1.06`

* `zoomScaleSensitivity` (`float`) Sensitivity when zooming. Default: `0.2`

* `mouseWheelZoomEnabled` (`boolean`) Enables or disables zooming with the scroll wheel. Default: `true`

* `colorMax`, `colorMin`, `colorNoData` (`string`) The color values in hex for highest value `colorMax`, lowest value `colorMin` and no data available `colorNoData`. Default: `#CC0033` for `colorMax`, `#FFE5D9` for `colorMin`, `#E2E2E2` for `colorNoData`

* `flagType` (`'emoji'`, `'image'`) The type of the flag in the tooltip. Default: `image`

* `flagURL` (`string`) The URL to the flags when using flag type `image`. The placeholder `{0}` will get replaced with the lowercase [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) country code. Default: `https://cdn.jsdelivr.net/gh/hjnilsson/country-flags@latest/svg/{0}.svg`

* `hideFlag` (`boolean`) Decide whether to show the flag option or not

* `noDataText` (`string`) The default text to be shown when no data is present

* `countries` (`object`) Additional options specific to countries:

  * `EH` (`boolean`) When set to `false`, Western Sahara (EH) will be combined with Morocco (MA)

* `data` (`object`) The chart data to use for coloring and to show in the tooltip. Use a unique data-id as key and provide following options as value:

  * `name` (`string`) The name of the data, it will be shown in the tooltip

  * `format` (`string`) The format for the data value, `{0}` will be replaced with the actual value

  * `thousandSeparator` (`string`) The character to use as thousand separator

  * `thresholdMax` (`number`) Maximal value to use for coloring calculations

  * `thresholdMin` (`number`) Minimum value to use for coloring calculations

* `applyData` (`string`) The ID (key) of the data that will be used for coloring

* `values` (`object`) An object with the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) country code as key and the chart data for each country as value

* `countryNames` (`object`) An object with the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) country code as key and the country name as value

## Localize

Use the option `countryNames` to translate country names. In the folder `local` you can find translations in following languages: Arabic, Chinese, English, French, German, Hindi, Portuguese, Russian, Spanish, Urdu

To create your own translations, check out [country-list](https://github.com/umpirsky/country-list) by [Sa??a Stamenkovi??](https://github.com/umpirsky).

## Attribution

If you need more detailed maps or more options for your data, there is a great open source project called [datawrapper](https://github.com/datawrapper/datawrapper) out there, with a lot more power than svgmap-next.

svgmap-next uses [svg-pan-zoom](https://github.com/ariutta/svg-pan-zoom) by [Anders Riutta](https://github.com/ariutta).

The country flag images are from [country-flags](https://github.com/hjnilsson/country-flags) by [Hampus Nilsson](https://github.com/hjnilsson).

Most data in the demos was taken from [Wikipedia](https://www.wikipedia.org).
