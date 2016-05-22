---
layout: post
title:  "Javascript - Few notes about Promise"
date:   2016-05-21 12:30:00 +0800
categories: javascript
---
Javascript itself has  synchronous features, the javascript engine trigger each line of code form top to down. But when we need request to call some data from the Internet (We call this behavior "Ajax"). Things go different, because javascript engine won't automatically  wait for data coming back (It just execute next line of code). This condition make javascript asynchronous. Sometimes we have to "make" javascript wait for the data and **then** do the next step (maybe process coming back data). SO javascript engine provide us a **Standard Object - "Promise"**, and let us be more controllable to the javascript async process.

###**Some Concept**###

Promise is kind of wrapper, at least you can see it as a box that hold your code inside it. It's a little bit like
``try{...} catch{..}`` （once the "try" throw some event out, "catch" will present it).

Promise will lock all your code inside it until you have the "**key**" to open the lock and your code will execute to the next part. And the key are ``resolve`` and ``reject``!!!

Wait a minute, what exactly are the key meaning. Before that we should go through the statement that promise have.

Promise have four statements

* Fulfilled (Resolve) : It works!

* Rejected : It didn't work properly

* Pending : still waiting

* Settled : Something happened !

When you use Promise object, it will be pending statement until Fulfill or Reject. Either way happens will take promise to the next step. ``.then()`` is a build in Promise property, it return a promise and can be chained.

We can see promise process flow below.

![Promise flow]({{ site.url }}/assets/Promise_flow.png)

As the picture, We can use ``.then()`` to control our process. So lets see some example.

###**Some Code**###

One key concept to write async code is that you must wrap your async code in ``Promise`` section. There are lots of sample code on **[MDN Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** (Mozila developer network) . After you go through MDN Promise description, you can see how to chain async code together as below. In MDN ``.then()`` method take previous promise resolved value and can be chained (see more on [MDN  then function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)). So it is useful to use .then() after the promise is resolve.

But!!!  ``.then`` won't process code like promise (it cannot handle async code). As the code below I use promise to wrap all my async code and make the flow controllable. I use ``.then`` to chain then together and every ``.then`` return a promise to lock the async code. I use ``Promise`` inside the ``.then`` function just to show how they work. (maybe not the best way)


{% highlight javascript %}
//step1 : Wait for 3 second and log the the messege
var p = new Promise(function(resolve, reject){
        window.setTimeout(function(){
                console.log('step1 : Wait for 8 second');
                resolve('4000')
            },8000)
    }
);

//step2 : Wait for 2 second and log the the messege
var p2 = p.then(function(val){
    return new Promise(function (resolve) {
        window.setTimeout(function(){
                console.log('step2 : Wait for 4 second');
                resolve('2000')
            },val) //val = 4000
        });
    }
)

//step3 : Wait for 1 second and log the the messege
p2.then(function(val){
    window.setTimeout(function(){
            console.log('step3 : Wait for 2 second');
        },val); //val = 2000
    }
);

//step4 : Wait for 1 second and log the the messege
p2.then(function(val){
    window.setTimeout(function(){
            console.log('step4 : Wait for 2 second');
        },val); //val = 2000  || equal to step 3
    }
);
{% endhighlight %}

Result

![Promise Sample Code]({{ site.url }}/assets/Promise_samplecode.png)

Step3 and Step4 show up together. We can see that ``.then()`` will get previous resolve value and just execute the code top to down(won't wait async code finish). So we should always wrap async code in **Promise** section.



[MDN Promise]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[MDN THEN FUNCTION]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then
