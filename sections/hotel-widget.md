Olery Reputation - Hotel Widget
===============================

**this api is currently in Beta**

With the Olery hotel widget it is possible to include a summary of the hotel information present in Olery Reputation on another website or intranet.

Examples
--------

Olery currently offers 2 layouts for the widget:

* Bar-layout
* Block layout

Below you see two example images. More [detailed examples can be found here](https://github.com/olery/reputation-api/blob/master/images/hotel-widget).

![bar-layout](https://raw.github.com/olery/reputation-api/master/images/hotel-widget/bar-1.png)

![block-layout](https://raw.github.com/olery/reputation-api/master/images/hotel-widget/block-1.png)

Examples of how to embed the widget in HTML [can be found here](https://github.com/olery/reputation-api/blob/master/examples/hotel-widget).

Authentication Token
--------------------

In order to get information for 1 or more hotels you need to request an Olery API access token. You can request a token at your Olery Sales representative or by mailing support@olery.com. This token is formatted like:

    OLERY-XXXXXXXXXXXX

Script Inclusion
----------------

To include the Olery widget include the following scripts at the bottom of the page right above the body-tag.

```html
<script src="http://widgets.olery.com/hotel.js" type="text/javscript"></script>
<script type="text/javascript">
try{
  _olery._initialize_widgets("OLERY-XXXXXXXXXXX");
} catch(err) {}
</script>
```

Also include the defauls Olery Widget CSS file into your HTML document. Preferably in the HEAD section of the document

```html
<link rel="stylesheet" href="http://widgets.olery.com/hotel.css"/>
```

Then within your webpage you can include a div containing the specific information about the hotel. In the example below the hotel has an id of "XXXX". In case of a list of hotels, you repeat this div for each hotel.

```html
<div class="olery-hotel-widget" data-hotel="XXXX" data-type="bar" data-locale="en">
  <a href="http://gei.olery.com/hotels/XXXX">Check the Guest Experience of this Hotel</a>
</div>
```

The basic Javascript will take care that, as long as the widget is not loaded, the link is not shown, given that the user has javascript enabled. If the user has javascript disabled the plain text link will show up which links to a page hosted at olery, which represents the review information to the user in a "non-javascript" way.

On initialization the Widget Javascript will find all div-elements with a olery-hotel-widget class and initialize all data. Replacing the HTML and loading data with an AJAX call per hotel.

If you want to disable the tooltip of a particular widget you can do so by adding `data-tooltip="false"` to the widget:

```html
<div class="olery-hotel-widget" data-hotel="XXXX" data-type="bar" data-locale="en" data-tooltip="false">
  <a href="http://gei.olery.com/hotels/XXXX">Check the Guest Experience of this Hotel</a>
</div>
```

Locales
-------

Currently the widget supports 2 locales:

* en - English
* nl - Dutch

You can set the locale by setting `data-locale="en"` attribute on the `.olery-hotel-widget` element.

Styles
------

Currently 2 styles are supported. Bar and Block. (see images on top of the document). You can set the style of the widget by setting the `data-type` attribute on the `.olery-hotel-widget` element.

In order to get a bar widget include `<div class="olery-hotel-widget" data-type="bar" ... > ... </div>`. By changing `"bar"` into `"block"` the style of the widget will change.

Generated HTML
--------------

The generated HTML per hotel will look like this:

```html
<div class="olery-hotel-widget olery-initialized" data-hotel="XXXX" data-type="bar" data-locale="nl">
  <div class="olery-guest-reviews">Guest reviews</div>
  <div class="olery-graph">
    <div class="olery-rating-lines">
      <span class="olery-rating-img olery-orange" style="width: 80%">&nbsp;</span>
      <span class="olery-clear"/>&nbsp;</span>
    </div>
    <div class="olery-summary">
      <a href="#" class="rating">8.0 / 10</a> based on <a href="number"> 616 </a> reviews
    </div>
  </div>
  <div id="olery-source-overlay-XXXX" class="olery-overlay">
    <ul>
      <li>
        Booking.com (533)
        <div class="olery-rating-lines">
          <span class="olery-rating-img olery-orange" style="width: 80%">&nbsp;</span>
          <span class="olery-clear"/>&nbsp;</span>
        </div>
        <div class="olery-summary"> 8.1 </div>
      </li>
    </ul>
  </div>
  <div id="olery-ratings-overlay-XXXX" class="olery-overlay">
    <ul>
      <li>
        Value
        <div class="olery-rating-lines">
          <span class="olery-rating-img olery-orange" style="width: 80%">&nbsp;</span>
          <span class="olery-clear"/>&nbsp;</span>
        </div>
        <div class="olery-summary"> 8.0 </div>
      </li>
    </ul>
  </div>
</div>
```
