Reviews Api
===========

**This api is in active development and not operational yet** However, the API definition is close to final, so feel free to start implementing.

Create new Reviews
------------------

The reviews API provides partners from Olery an endpoint to push reviews or collections of reviews
to Olery Reputation. The reviews will be part of the numerical analysis, like the average review
ratings, as well as the sentiment analysis when a review text is provided.

### Create review

* `POST /reviews.json` will create a new review from the parameters passed.

````json
{
    "auth_token": "Your auth token",
    "reviews":[
    {
      "title": "This is my new review!",
      "comment": "This is my review comment, made up in markdown",
      "author": {
        "name": "Some reviewer",
        "age" : "Age indicator",
        "origin" : "Someplace, Somecountry"
      },
      "ratings": {
        "overall" : 90,
        "cleanliness" : 85,
        "value" : 10
      }
    },
    {"title": "Some other review"}]
}
````

This will return `201 Created`, the reviews are queued for processing and will appear in your Olery Reputation account soon.

If the api-key is invalid, you'll see `401 Unauthorized`.
If the api-key has reached the project limit, you'll see `429 Too Many Requests`.

### Required and Optional Fields

A review consists of several required and optional fields. Below these fields are listed, including an example.

* `title` (optional) - `String`. Example: `It was amazing!`
* `publish_date` (required) - `Date`. Example: `2012-01-30`
* `source_url` (required) - `String`. A url, preferably a deep-link to the origin of the review. Example: `http://my-review-site.com/review/review-id`
* `comment` (optional) - `Text`. Example: `Very Very nice hotel.`
* `management_response` (optional) - `Text`. Example: `Thank you for staying in the hotel. Hope to see you next time`
* `author` (optional)
    - `author.name` (optional) - `String`. Example: `John Doe`
    - `author.age` (optional) - `String`. Example `25-39`
    - `author.location` (optional) - `String`. Example `Atlanta, Georgia`
    - `author.reason` (optional) - `String`. Example `Business` other options are `Leisure`
* `ratings`
    - `ratings.overall` (required) - `Float` [10-100].
    - `ratings.value` (optional) - `Float` [10-100].
    - `ratings.rooms` (optional) - `Float` [10-100].
    - `ratings.cleanliness` (optional) - `Float` [10-100].
    - `ratings.location` (optional) - `Float` [10-100].
    - `ratings.service` (optional) - `Float` [10-100].
    - `ratings.food` (optional) - `Float` [10-100].

