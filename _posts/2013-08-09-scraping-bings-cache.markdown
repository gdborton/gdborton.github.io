---
layout: post
date: 2013-08-09 06:00:00
title: "Scraping Bing's Cache"
categories: ["Coding for Fun"]
permalink:  /2013/08/09/scraping-bings-cache/
---

I've finally found a practical use for [Bing](https://www.bing.com/)!  I was browsing one of my favorite forums last week, and saw a thread mentioning a blog that recently disappeared.  It seems that the owner of the blog said something in a way that he shouldn't have, and found himself in a lawsuit.  As part of the settlement he was required to remove the content in question, as well as clear all cached content from popular search engine and archival websites.  He took it to the extreme, and removed all of his content completely, removed it from the [way back machine](http://archive.org/web/web.php), and even asked [Google](https://www.google.com/) to clear their cache of it.  This made a bunch of people sad pandas because his content was a great [financial independence]({{site.url}}/2013/08/07/im-going-to-retire-early/) resource.

## Enter Bing

Bing is actually a pretty good search engine these days.  It provides similar results as Google, as well as many similar
features.  One of the more important ones is cached pages.  Apparently Bing didn't make his popularity cut, as his posts
were still cached there.  In order to preserve my ability to read said content, and for little bit of fun, I wrote the
below userscript to scrape Bing's cached content.

{% highlight javascript %}
// ==UserScript==
// @name       Bing scraper
// @namespace  http://www.garyborton.com
// @require http://ajax.googleapis.com/ajax/libs/jquery/2.0.0/jquery.min.js
// @version    1.0
// @description  Prints bing cache url for all search results on page to the console.
// @match      http://www.bing.com/*
// @copyright  2013+, Gary Borton
// ==/UserScript==

$(document).ready(function(){
    $('.sa_cc').each(
        function(index, element){
            var totalString = "";
            totalString = $(element).attr('u');
            if(totalString !== "" && totalString) {
                var attr = totalString.split('|');
                var link = "http://cc.bingj.com/cache.aspx" + location.search.split('&')[0] + "&d=" + attr[2] + "&mkt=en-US&setlang=en-US&w=" + attr[3];
                console.log(link);
            }
        }
    );
});
{% endhighlight %}


## How it works

The script was a bit more complicated than just searching the DOM for a cached page link.  It isn't immediately apparent, but Bing doesn't actually create it's cached page link until the user clicks a drop down arrow.  After a bit of fiddling I found that the cached pages always use two query parameters to locate and display cached content, d and w.

    http://cc.bingj.com/cache.aspx?q=monkey&d=4861925562714075&mkt=en-US&setlang=en-US&w=ZWyKzxkdgYWi8uTeyaUqhqFshVcMNxbe

A little more searching and I found that these were in the DOM as an attribute on a div tag with the class “sa_cc” for each result in Bing.

{% highlight html %}
<div class="sa_cc" u="0|5032|4861925562714075|ZWyKzxkdgYWi8uTeyaUqhqFshVcMNxbe">...</div>
{% endhighlight %}


After finding that, it was pretty simple to split the string into the prospective query parameters, and print all the cached pages to console.

Once you've got the list, you can store it in a text file and run the below command in linux to pull all of the content down and save it to disk.

{% highlight bash %}
wget -i <file>
{% endhighlight %}


I doubt this will see any more love, but here is the [GitHub repo](https://github.com/gdborton/bing-cached-url-scraper) for this userscript.