Reputation-api
==============

Documentation on Using Olery Reputation APIs

Making a Request
----------------
All URLs start with https://api.olery.com/reputation/v1/. SSL only. If we change the API in backward-incompatible ways, we'll bump the version marker and maintain stable support for the old URLs.

To make a request for all reviews in a certain period, you'd append the reviews index path to the base url to form something like https://api.olery.com/reputation/v1/reviews.json. In curl, that looks like:

````shell
curl -u user:pass -H 'User-Agent: MyApp (yourname@example.com)' https://api.olery/com/reputation/v1/reviews.json
````

To create something, it's the same deal except you also have to include the Content-Type header and the JSON data:

````shell
curl -u username:password \
  -H 'Content-Type: application/json' \
  -H 'User-Agent: MyApp (yourname@example.com)' \
  -d '{ ["title": "My new review!"] }' \
  https://api.olery.com/reputation/v1/reviews.json
````

That's all!

Authentication
--------------

The api(v1) requires api_token authentication. If you don't have an api-token request a token with your account representative.

Please provide a

    auth_token=[your token here]

either as part of the params in the url or post it as a parameter with the request.

APIs in Development
-------------------

* [Reviews](https://github.com/olery/reputation-api/blob/master/sections/reviews.md) (in development, not operational yet)
* [Hotel Widget](https://github.com/olery/reputation-api/blob/master/sections/hotel-widget.md) (currently in Beta)

General notes
-------------

### Only SSL

We require that all requests are done over SSL.

### UTF-8 Encoding

Every string passed to and from the Olery API needs to be UTF-8 encoded. For maximum compatibility, normalize to Unicode Normalization Form C (NFC) before UTF-8 encoding.

### No XML, just JSON

We only support JSON for serialization of data. Our format is to have no root element and we use snake_case to describe attribute keys. This means that you have to send Content-Type: application/json; charset=utf-8 when you're POSTing or PUTing data into Basecamp. All API URLs end in .json to indicate that they accept and return JSON.

You'll receive a `415 Unsupported Media Type` response code if you attempt to use a different URL suffix or leave out the Content-Type header.

### Date Format
All dates in the API are strings in the following format:

    "2012-01-30 15:30:20 +0000"

In code format, which can be used in all programming languages that support strftime or strptime:

    "%Y-%m-%d %H:%M:%S %z"
