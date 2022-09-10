(To get a proper grip of this guide you should probably read the other pages first. I'll be going all in on the terminology here.)

## Introduction

<sup>I've never written an API guide before, and I hope I never have to again.</sup>

There are two main endpoints to Bandcamp's API. For the sake of my sanity and yours, I'll refer to them as the "Summary" and "Item" endpoints.

The Summary endpoint is your first port of call. As you'd expect, it contains a summary of all items in your library.

The Item endpoint contains ALL of the data you need when referencing items and their relative information. It also includes streaming and download URLs, cover art URLs, and tracklists for each item.

"So", I hear you ask, "if the Item endpoint has everything I need, why do I need the Summary endpoint?", and for that we need to get into the nitty-gritty.

## The Nitty-Gritty

The process you want to use when accessing data via Bandcamp's API is as follows:

1. Call the Summary endpoint via GET request
2. Using the output data from the Summary endpoint as request parameters, call the Item endpoint

Both endpoints require the existence of a browser cookie called Identity. You can equate that to a mutable (but not really) service token.

### Calling the Summary Endpoint

Below is an example of a GET request to the Summary endpoint in JavaScript.

```js
await (await fetch("https://bandcamp.com/api/fan/2/collection_summary", {
    "method": "GET"
})).json();
```

### Calling the Item Endpoint

Below is an example of a POST request to the Item endpoint in JavaScript.

```js
await (await fetch("https://bandcamp.com/api/fancollection/1/collection_items", {
    "body": '{"fan_id":8124620,"older_than_token":"1893456000::a::","count":100}',
    "method": "POST"
})).json();
```

And now let's break those parameters down:

| Parameter        | Data Type | Data Source                                             | Notes                                            |
|------------------|-----------|---------------------------------------------------------|--------------------------------------------------|
| fan_id           | Long      | Collection Summary - Under `fan_id`                     | Not to be confused with your Identity token      |
| older_than_token | String    | Should be generated at request-time                     | Why is the `::a::` suffix needed? Hell if I know |
| count            | Int/Long  | Collection Summary - Count children of `tralbum_lookup` |                                                  |