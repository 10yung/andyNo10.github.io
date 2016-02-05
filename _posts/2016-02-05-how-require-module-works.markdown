---
layout: post
title:  "Node.js - how require and module.exports work"
date:   2016-02-05 17:10:00 +0800
categories: node
---
Node let us use functions in different javascript file. It's very convenient to reuse code and build scalable applications.
Here is a simple example.

We create a javascript file called **greet.js**
{% highlight javascript %}
/*greet.js*/
var greet = function(){
  console.log('hello');
}
greet();
{% endhighlight %}

As we see that greet.js run a function inside itself.
But we need other javascript file to call this function.

In Nodejs we use ``module.exports`` object so the object can used by other javascript files. In this case we use
``module.exports = greet;`` so that greet object can be reused.
{% highlight javascript %}
/*greet.js*/
var greet = function(){
  console.log('hello');
}

module.exports = greet;
{% endhighlight %}

Then we create a file called **app.js** to call greet( ) function in **greet.js**.
{% highlight javascript %}
/*app.js*/
var greet = require('./greet2');

greet();
{% endhighlight %}

We use ``require () `` function ( provided by node ), and put the greet.js path in that function, so we
can use greet() function.

Here is my file structure.
{% highlight ruby %}
.
|-- node-modules
|-- app.js
|-- greet.js
{% endhighlight %}

This simple example just show how to use node-modules, but why !?

---

Here is what Node do for you.

1. require get the javascript file path.

2. load the file content

3. wrapped it to a function ( like immediate invoke function
  ``(var greet = function(){ console.log('hello'); } module.exports = greet;,'()');`` )



4. run the function

5. return module.exports object to a variable

This is how Node ( v8 engine ) done for you, so you can use javascript function easily  and conveniently without worrying about the name and scope.

---

And you should remember the following two point :

**1. require is a function that pass a path to a variable, module.exports is what the require function return**

**2. your code is wrapped in a function so you don't need to worry about the variable**
