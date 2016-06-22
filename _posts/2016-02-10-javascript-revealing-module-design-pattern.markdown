---
layout: post
title:  "Javascript - the Revealing Module Design Pattern"
date:   2016-02-10 17:00:00 +0800
categories: nodejs
---
Before the Revealing Module Design Pattern, we can see the Javascript Module Design Pattern first.

We know that javascript is in OOP languages family, but it's **not Class-based language**.

------

Javascript is **Prototype-based**, (means no ``class`` keyword in Javascript) so we use Module Pattern.

**The Module Pattern** is used to mimic classes, in order to focus on public and private access to methods & variables and
decrease the chance of collision with other code in an application.

In Node.js, it's is very easy to implement Module Pattern. We just need to separate javascript file and use ``module.exports``
, ``require()`` keyword, so we can combine javascript files together.

-------

**The Revealing Module Pattern** is just like the module pattern. It focus on public & private methods.
The difference is that all methods and variables are kept private until they are explicitly exposed.

the following is a simple example （Node.js version）.
We create a javascript file called **greet.js**
{% highlight javascript %}
/*greet.js*/
var greetStr = 'private var : greet!!!';

function greetProtect() {
  console.log(greetStr);
}

//the above section are hidden from outside
//greet object let the require function use the name to call the value
module.exports = {
  greet : greetProtect //greet represent greetProtect function
}
{% endhighlight %}

In my app.js, I can use ``require('./greet')``  with the appended  **.greet**  to call the greetProtect function in the greet.js file.

{% highlight javascript %}
/*app.js*/
var greet = require('./greet').greet;
greet();

{% endhighlight %}

this is my file structure.

{% highlight ruby %}
.
|-- node-modules
|-- app.js
|-- greet.js
{% endhighlight %}

In this case, I can't directly call greetProtect function outside greet.js file. I can only use greet(the name) to represent
greetProtect function. This means the function is hidden from outside.

here are other simple example.
{% highlight javascript %}
var myRevealingModule = (function () {

        var privateVar = " ",
            publicVar = "Hey there!";

        function privateFunction() {
            console.log( "Name:" + privateVar );
        }

        function publicSetName( strName ) {
            privateVar = strName;
        }

        function publicGetName() {
            privateFunction();
        }

        // Reveal public pointers to
        // private functions and properties

        return {
            setName: publicSetName,
            greeting: publicVar,
            getName: publicGetName
        };

    })();

myRevealingModule.setName( "AndyNo.10" );
{% endhighlight %}

We can use the pattern to make the syntax of our scripts to be more consistent.
It also makes it more clear at the end of the module which of our functions and variables may be accessed publicly which eases readability.

------

Find more about Revealing Module Pattern on O'reilly online book

[Essential JS Design Patterns][Essential-JS-Design-Patterns]


[Essential-JS-Design-Patterns]:https://addyosmani.com/resources/essentialjsdesignpatterns/book/#revealingmodulepatternjavascript
