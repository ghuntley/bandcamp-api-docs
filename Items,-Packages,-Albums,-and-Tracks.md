## Preface

<sup>Whoever worked on this was a monster. Who hurt you, you poor soul?</sup>

The best way to describe it is that every "album" or "track" you visibly see in your library isn't so. It's treated by the API as a record of your purchase with other details added in.

To use the underlying terminology, EVERYTHING you see is classed as an "Item", however that item can be multiple types.

## Item Types

Here's a graph of item types with details added in where appropriate.

In JSON data, the item type can be represented in one of two String formats, an initial or a full word. These have also been included.

| Type    | Details                                                                                                                                        | Data Representation |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| Album   | What you'd expect. A standard album.                                                                                                           | "a"<br>"album"      |
| Track   | Similar formatting to an album, with most data nullified.                                                                                 | "t"<br>"track"      |
| Package | To simplify it, this is a Track or Album with merchandise.<br>An example of this would be a vinyl purchase which includes online album access. | "p"<br>"package"    |

For an exhaustive breakdown of the data contained in each item type, head to [API Data and Its Usages](https://github.com/har-nick/bandcamp-api-docs/wiki/API-Data-and-Its-Usages).