---
layout: post
title: "BodyBuilding and Userscripts"
date: 2013-07-19 06:00:00
categories: ["Coding for Fun"]
---

For my [get sexy goal](http://www.garyborton.com/2013/04/16/get-sexy/), I used bodybuilding.com a lot.  It really helped
me with both my diet and my workout, and it helped me to filter out all of the bro science that floats around out there.
The best part of the site is the forum, and while like any forum there is a lot of misinformation coming from people
that are wrong or just fuzzy on an idea,  I would say that there is an equal number of people that are skeptics, and
demand studies for proof that something is or isn’t effective.

Outside of looking for advice to help me shape my lifestyle, there are several body transformation threads with before
and after pictures.  As much as I love this thread, I noticed a deficiency in that on most posts the images are linked
to like an attachment.  This means that you need to open them in a new tab, and it certainly slows down mindless
browsing.  I decided to write a userscript (use with
[greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/) or
[tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en)) to let me
avoid the hassle of opening these images in a new tab.  The result is below.

It’s a pretty simple script that runs only on forum.bodybuilding.com pages.  Replaces the inline links to images with
their source being set to the href of the original link.

{% highlight javascript %}
// ==UserScript==
// @name       Body Building Forum Enhancer
// @namespace  http://www.garyborton.com
// @require http://ajax.googleapis.com/ajax/libs/jquery/2.0.0/jquery.min.js
// @version    0.1
// @description  Changes links to media to embedded media.
// @match      http://forum.bodybuilding.com/*
// @copyright  2013+, Gary Borton
// ==/UserScript==

$(document).ready(function(){
    var fileTypes = [".jpg", ".jpeg", ".png", ".gif"];
    var allLinks = $('a');

    allLinks.each(function(){
        var element = $(this);

        if (validImageLink(element)) {
            element.replaceWith("<img src=\""+$(this).attr('href')+"\">"+$(this).text()+"</img>");
        }
    });

    $('.inlineimg').remove();

    function validImageLink(element) {

        var returnValue = false;

        $.each(fileTypes, function(index, value) {
            if (element.text().toLowerCase().indexOf(value) > -1) {
                returnValue = true;
                return false; // Breaks the jQuery loop
            }
        });

        return returnValue;
    }
});
{% endhighlight %}

Link to the repo - https://github.com/gdborton/body_building_forum_enhancement