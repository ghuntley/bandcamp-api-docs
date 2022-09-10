## Preface

This page will cover some of the output data of each endpoint, including variations due to differing data in each item type.

As a warning, this page shouldn't be relied upon when parsing and deserializing data. While I haven't experience it myself over around a year, names and their values' datatypes can obviously be changed at any time.

## Endpoint Data

### Summary Endpoint

As mentioned in [API Endpoints](https://github.com/har-nick/bandcamp-api-docs/wiki/API-Endpoints), the Summary endpoint contains basic information on your account and the items in your library: At the top-level, this includes your fan (user) ID, your username, and a list of item data objects.

The output data is used when contacting the Item endpoint, but I also use this data as a way to check if cached data is out of date. The reason for this is because the Summary output data contains _all_ items in your library. If you hide an item in your library [like so](https://raw.githubusercontent.com/har-nick/bandcamp-api-docs/main/assets/hide-album-example.png), it will still show in the output data. This is not the case for the Item endpoint.

### Item Endpoint

Here's the fun stuff. The Item endpoint contains three datasets, `items`, `redownload_urls`, and `tracklists`, and a Boolean, `more_available`, which should be false if your endpoint request is structured properly.

`items` is a list of JSON objects containing the information that represents an item. Everything from the id, title, and the artist, to the number of streamable tracks and the date it was purchased.

`redownload_urls` is String Map containing the URL to download the relevant item.

`tracklists` is another String Map containing lists of JSON objects representing each track. This includes the url to stream the track in mp3v0 format.

## Notable Tidbits

Just some data I got hung up on and thought might be useful putting down with some workarounds.

### Item Endpoint Tidbits

`items`

* The POST request's `older_than_token` parameter can take a timestamp in the future, but that's probably not a good idea.
* `album_id` and `items/X/album_title` are null when not actually an Album. Use `item_id` and `item_title` instead.
* `featured_track` and its related values default to the information of the first track in the album. Rely on `featured_track_is_custom` to display conditional featured track data.
* `genre_id` is useless, as far as I can tell
* `hidden` is always null. Again, useless.

`redownload_urls`

* The URLs aren't direct. They lead to webpages forcing you to select your desired download format. I'm working on finding a way to conjure up direct download URLs.
* Every key in the Map is prefixed with "p" for package, even other Item types. Unsure why. I just drop the prefix when handling that data.
* _Seems_ to be ordered by the date your purchased them? Unsure. Haven't checked properly.

`tracklists`
* `track_number` is null when dealing with Track type Items. Tracks are in the correct order anyways, so just rely on their key index.