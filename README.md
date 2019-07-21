Instagram Hashtag Scrapper
==============
NodeJS module for loading media from Instagram by hashtag, individual media and location media without API access by means of scraping.

## Disclamer
Instagram has gone to great lengths to prevent scraping and other unauthorized access to their public content. This module is dependant on the markup the public-facing instagram.com. Should that change this module might also stop working as intended. It also only loads the 17 posts that are displayed on first-load without following pagination to load more images. You should take this into consideration when deciding whether this module will work for you.

## Installation

`npm install instagram-hashtag-scrapper`

## Usage

The most basic usage will allow you to load the first 17 posts for any given hashtag with basic info and URLs to the full post media.

### Tage page scraping

```javascript
var ig = require('instagram-hashtag-scrapper');

ig.scrapeTagPage('miami').then(function(result){
    console.dir(result);
})
```

Example response:

```json
{
    "total": 5854,
    "count": 17,
    "media": [{
        "code": "BMm39DKD6DB",
        "date": 1478733183,
        "dimensions": {
            "width": 750,
            "height": 750
        },
        "comments_disabled": false,
        "comments": {
            "count": 0
        },
        "caption": "Lorem ipsum... #quote #margaretmead #restmycase",
        "likes": {
            "count": 52
        },
        "owner": {
            "id": "393767493"
        },
        "thumbnail_src": "https://instagram.fosl1-1.fna.fbcdn.net/t51.2885-15/s640x640/sh0.08/e35/14719160_341462716214777_3017677686123266048_n.jpg?ig_cache_key=MTM4MDAzNjQyMzY3MTg0OTE1Mw%3D%3D.2",
        "is_video": false,
        "id": "1380036423671849153",
        "display_src": "https://instagram.fosl1-1.fna.fbcdn.net/t51.2885-15/s750x750/sh0.08/e35/14719160_341462716214777_3017677686123266048_n.jpg?ig_cache_key=MTM4MDAzNjQyMzY3MTg0OTE1Mw%3D%3D.2"
    }
}
```

As you can see, only the basic info required for listing images is returned. If you need further info, like more info about the owner of the post or the location, you can perform these queries separately or all in one go with the included `deepScrapeTagPage` method which populates the original tag page response with the corresponding data from the postPage and locationPage methods.

### Deep tag page scraping

```javascript
var ig = require('instagram-hashtag-scrapper');

ig.deepScrapeTagPage('miami').then(function(result){
    console.dir(result);
})
```

The response from this call is so vast that to see what it contains I recommend you perform it and log out the result.

### Post page scraping

The post page scraping method takes a `code` argument (like the one returned for each post via the `scrapeTagPage`).

```javascript
var ig = require('instagram-hashtag-scrapper');

ig.scrapePostPage('B0EktnOgLqq').then(function(result){
    console.dir(result);
})
```

### Location Page Scraping

The location page scraping method takes a numeric `id` argument (like the one returned for each post via the `scrapeTagPage`) and returns lat/lng coordinates for the post location among many other things.

```javascript
var ig = require('instagram-hashtag-scrapper');

ig.scrapeLocationPage(542401).then(function(result){
    console.dir(result);
})
```
