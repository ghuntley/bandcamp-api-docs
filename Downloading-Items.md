## Preface

This section covers downloading purchased items only. Streamed "public" tracks through the website are in mp3-v0. This covers all available formats, and deals with pages only available to those who have purchased their items.

## A note on `redownload_urls`

As mentioned in the notes of [API Data and Its Usages](https://github.com/har-nick/bandcamp-api-docs/wiki/API-Data-and-Its-Usages/), the links given in the `redownload_urls` map are indirect. As far as I am able to tell, you cannot avoid going to this page. Specific pieces in the response data on this page are not provided by any API endpoints, and cannot be generated or sourced from existing data.

## An Initial Look-See

The Download link given on the webpage leads to a `p4.bcbits.com` url, a separate CDN domain to `f4.bcbits.com`, which is used to host album art.

Let's take a look: (Relevant data changed)

`https://p4.bcbits.com/download/album/125475mjj14k9244i23i431j37k61ij4i/mp3-v0/1461245367?id=1461252468&sig=j3k453m2hhhjm2jm20li91150i588h6h&sitem_id=128245613&token=1668184914_9i0786k1k6h787l873437l06lj095591967k8249`

Yeah, no. Far too many variables that can't be pulled from existing data sources.

## A Deep(er) Dive

When checking the HTML response through a proxy toolkit, a Blob can be found containing the direct links to each file format of your choice. Success!

I won't show the full-length Blob here as it's far too large. Here's a raw snippet of a download link: (Again, data changed)

`https://popplers5.bandcamp.com/download/album?enc=mp3-v0&amp;id=3315244259&amp;sig=n3o453q2lllnq2nq20pm91150m588l6l&amp;sitem_id=489132465&quot`

Much less painful to work with.

## The Breakdown

Let's break those parameters down!

| Parameter | Notes                                                                                                                                                                        | Can be found / generated? |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| album     | See [Item Types](https://github.com/har-nick/bandcamp-api-docs/wiki/Items,-Packages,-Albums,-and-Tracks#item-types).<br>Packages and Albums are `album`. Tracks are `track`. | Yes. Use `item_type`      |
| enc       | See [Encoding](https://github.com/har-nick/bandcamp-api-docs/wiki/Encoding).                                                                                                 | Yes.                      |
| id        |                                                                                                                                                                              | Yes. Use `item_id`        |
| sig       | Unique to each encoding type.                                                                                                                                                | Only for mp3-v0 encoding.           |
| sitem_id  |                                                                                                                                                                              | Yes. Use `sale_item_id`   |

I've looked through every desktop web request and was unable to find the signature for anything but the already given mp3-v0 encoding from `redownload_urls`. Maybe there's a way out there, but it seems unlikely.