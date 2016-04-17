---
layout: post
title:  "Javascript - hum, so this is javascript __proto__ right?"
date:   2016-04-07 12:30:00 +0800
categories: javascript
---
Long time ago, Firefiox got non-standard property \__proto__. It wasn't included in the ECMAScript (until ECMAScript 6) , but lots of modern browsers decided to copy and implement it. So now we can see that browser (IE, Chrome) use \__proto__

All function, object that you create have \__proto__ property. As you can see below.

{% highlight javascript %}
/*__proto__ example.js*/
var obj = {};
var fn = function() {};
var arr = [];
{% endhighlight %}

and you can see in chrome developer tool that

**obj.\__proto__ = Object{}**

**fn.\__proto__ = function Empty(){}**

**arr.\__proto__ = [ ]**

This means that every object has its own \__proto__ porperty.
And it's said that \__proto__ is point to the prototype of its' father object.


**so \__proto__ is just an property that represent it's father object.**
