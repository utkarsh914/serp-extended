# serp-extended
This module is an extention to 'serp' module.
It adds an option to exclude whichever websites you want from your search results.
It to execute search on Google with or without proxies.
It provides different options for scraping the google results (either the list of the referenced sites or the number of results).


# Installation

``` bash
$ npm install serp-extended
```


# Simple usage

``` javascript
const serp = require("serp-extended");

var options = {
  host : "google.be",
  ignore: ['youtube.com', 'twitter.com'],
  qs : {
    q : "test",
    filter : 0,
    pws : 0,
    nfpr: 1
  },
  num : 10
};

const links = await serp.search(options);
```

*Understanding the options structure :*
- For google.com, the param host is not necessary.
- ignore contains an array of websites you want to exclude from your search results
- qs can contain the usual Google search parameters : https://moz.com/ugc/the-ultimate-guide-to-the-google-search-parameters.
- options.qs.q is the keyword
- nfpr for exclusion of results from an auto-corrected query: 1 is disabled (default is 0)
- num is the number of desired results (defaut is 10).
- The options object can also contain all request options like http headers, ... . SERP is using the request module :  https://github.com/request/request
- The user agent is not mandatory. Default value will be : 'Mozilla/5.0 (Windows NT 6.1; WOW64; rv:40.0) Gecko/20100101 Firefox/40.1'


## With proxy

You can add the proxy reference in the options

``` javascript
const serp = require("serp-extended");

var options = {
  qs : {
    q : "test",
  },
  proxy : "http://username:password@host:port"  
};


const links = await serp.search(options);
```

You can also use the module simple proxy if you have several proxies (see : https://github.com/christophebe/simple-proxies).

``` javascript
const  serp = require("serp-extended");

var options = {
  qs : {
    q : "test",
  },
  proxyList : proxyList
};

const links = await serp.search(options);
```

## Delay between requests

It is possible to add a delay between each request made on Google with the option *delay* (value in ms).
The delay is also applied when the tool read the next result page on Google.


``` javascript
const serp = require("serp-extended");

var options = {

  qs : {
    q : "test"
  },
  num : 100,
  delay : 2000 // in ms
};

const links = await serp.search(options);
```

## Retry if error

If an error occurs (timeout, network issue, invalid HTTP status, ...), it is possible to retry the same request on Google. If a proxyList is set into the options, another proxy will be used.

``` javascript
const serp = require("serp-extended");

var options = {

  qs : {
    q : "test"
  },
  num : 100,
  retry : 3,
  proxyList : proxyList
};

const links = serp.search(options);
```

## Get the number of results

You can get the number of indexed pages in Google by using the following code.


``` javascript
const serp = require("serp-extended");

var options = {
  host : "google.fr",
  numberOfResults : true,
  qs : {
    q   : "site:yoursite.com"
  },
  proxyList : proxyList
};

const numberOfResults = await serp.search(options);
```
