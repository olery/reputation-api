Reviews Api
===========

** This api is in active development and not operational yet ** However, the API definition is close to final, so feel free to start implementing.

Create new Reviews
------------------

The reviews API provides partners from Olery an endpoint to push reviews or collections of reviews
to Olery Reputation. The reviews will be part of the numerical analysis, like the average review
ratings, as well as the sentiment analysis when a review text is provided.

### Create review

* `POST /reviews.json` will create a new review from the parameters passed.

````json
    {
      "title": "This is my new review!",
      "comment": "This is my review comment, made up in markdown",
      "author": {
        "name": "Some reviewer",
        "age" : "Age indicator",
        "origin" : "Someplace, Somecountry"
      },
      "ratings" {
        "overall" : 9.0,
        "cleanliness" : 8.0,
        "value" : 10
      }
    }
````

This will return `201 Created`, with the location of the new review in the Location header along with the current JSON representation of the reviews if the creation was a success.

If the api-key does not have access to create new reviews or the account has reached the project limit, you'll see `403 Forbidden`.

### Required and Optional Fields

A review consists of several required and optional fields. Below these fields are listed, including an example.

* `title` (optional) - `String`. Example: `It was amazing!`
* `publish_date` (required) - `Date`. Example: `2012-01-30 15:30:20 +0000`
* `comment` (optional) - `Text`. Example: `Very Very nice hotel.`
    - `comment.management_response` (optional) - `Text`. Example: `Thank you for staying in the hotel. Hope to see you next time`
* `author` (optional) - `String`. Example: `John Doe`
    - `author.age` (optional) - `String`. Example `25-39`
    - `author.location` (optional) - `String`. Example `Atlanta, Georgia`
    - `author.reason` (optional) - `String`. Example `Business` other options are `Leisure`
* `source`
    - `source.uri` (required) - `String`. A url, preferably a deep-link to the origin of the review. Example: `http://my-review-site.com/review/review-id`
* `ratings`
    - `ratings.overall` (required) - `Float` [10-100].
    - `ratings.value` (optional) - `Float` [10-100].
    - `ratings.rooms` (optional) - `Float` [10-100].
    - `ratings.cleanliness` (optional) - `Float` [10-100].
    - `ratings.location` (optional) - `Float` [10-100].
    - `ratings.service` (optional) - `Float` [10-100].
    - `ratings.food` (optional) - `Float` [10-100].

