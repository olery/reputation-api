Reviews Api
===========

**This api is in beta** Please report any issues, improvement or requested
changes.

Create new Reviews
------------------

The basic endpoint for review creation is:

```
https://api.olery.com/v1/reputation/reviews.json
```

The reviews API provides partners from Olery an endpoint to push reviews or
collections of reviews to Olery Reputation. The reviews will be part of the
numerical analysis, like the average review ratings, as well as the sentiment
analysis when a review text is provided.

### Create review

* `POST /reviews.json` will create a new review from the parameters passed.

```json
{
    "auth_token": "Your auth token",
    "reviews":[
    {
      "publish_date": "2012-12-31",
      "title": "This is my new review!",
      "comment": "This is my review comment, made up in markdown",
      "reviewer": {
        "name": "Some reviewer",
        "age" : "Age indicator",
        "origin" : "Someplace, Somecountry"
      },
      "ratings": {
        "overall" : 90,
        "cleanliness" : 80,
        "value" : 95
      }
    },
    {
      "publish_date": "2013-01-01",
      "title": "This is another review",
      "comment": "So nice to be able to push an array of reviews",
      "reviewer": {
        "name": "Some reviewer",
        "age" : "Age indicator",
        "origin" : "Someplace, Somecountry"
      },
      "ratings": {
        "overall" : 90,
        "rooms" : 80,
        "childfriendliness" : 90,
        "value" : 100
      }
    }]
}
```

This will return `201 Created`, the reviews are queued for processing and will
appear in your Olery Reputation account soon.

If the api-key is invalid, you'll see `401 Unauthorized`.
If the api-key has reached the project limit, you'll see `429 Too Many Requests`.

### Required and Optional Fields

A review consists of several required and optional fields. Below these fields
are listed, including an example.

* `title` (optional) - `String`. Example: `It was amazing!`
* `publish_date` (required) - `String`, formatted as ISO 8601 ('%Y-%m-%d' would be the strftime format). Example: `2012-01-30`
* `source_url` (optional) - `String`. A url, preferably a deep-link to the origin of the review. Example: `http://my-review-site.com/review/review-id`
* `comment` (optional) - `Text`. Example: `Very Very nice hotel.`
* `management_response` (optional) - `Text`. Example: `Thank you for staying in the hotel. Hope to see you next time`
* `reviewer` (optional)
    - `reviewer.name` (optional) - `String`. Example: `John Doe`
    - `reviewer.age` (optional) - `String`. Example `25-39`
    - `reviewer.location` (optional) - `String`. Example `Atlanta, Georgia`
    - `reviewer.reason` (optional) - `String`. Example `Business` other options are `Leisure`
* `ratings`
    - `ratings.overall` (required) - `Integer` [10-100].
    - `ratings.value` (optional) - `Integer` [10-100].
    - `ratings.rooms` (optional) - `Integer` [10-100].
    - `ratings.cleanliness` (optional) - `Integer` [10-100].
    - `ratings.location` (optional) - `Integer` [10-100].
    - `ratings.service` (optional) - `Integer` [10-100].
    - `ratings.food` (optional) - `Integer` [10-100].
    - `ratings.CUSTOM-RATING` (optional) - `Integer` [10-100].

Here `CUSTOM-RATING` should be replaced by whatever rating names you can come
up with. There's no limit to the amount of ratings and their names.

However, please contact Olery before sending in any custom ratings so that we
can map them to the list of known ratings. Without this reviews will **not** be
saved as our system discards reviews with unknown ratings.
