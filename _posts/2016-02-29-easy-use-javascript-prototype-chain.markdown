---
layout: post
title:  "Javascript - how to use javascript prototype chain"
date:   2016-02-29 12:15:00 +0800
categories: javascript
---
Javascript prototype has the feature of object inheritance!
Prototype allows me to add new properties to an existing prototype.
Here is a simple example that add new properties to existing prototype through prototype.


{% highlight javascript %}
function Person(firstName){
    this.firstName = firstName;
}

Person.prototype.lastName = "Lin";

var andy = new Person('Teng Yung');
console.log(andy.firstName + ", " + andy.lastName); // Teng Yung, Lin

{% endhighlight %}

###### the **new** keyword is to create new empty object and call the contructor function (in this case : function Person() )

###### "constructor" in JavaScript is "just" a function that happens to be called with the new keyword.

In this case, I just add ``lastName`` property to my ``Person`` prototype and I can access ``lastName`` property after ``new Person``.
It's just kind of inheritance feature that javascript give me.

When you call Object's property. Javascript first look into the Object's own properties. If the Object properties
don't have such property it will look for the Object's prototype.

The following is another example
{% highlight javascript %}
function Person(firstName){
    this.firstName = firstName;
}

Person.prototype.lastName = 'Lin'; // set property attach to Person prototype
console.log(Person.prototype);  //Person { lastName: 'Lin' }

var andy = new Person('Teng Yung');//Person { firstName: 'Teng Yung'}
console.log(andy.lastName); // Lin  ---> andy object can access to Person.prototype property
//jsvascript object is pass by reference means andy point to Person object

andy.lastName = 'andyNo.10'; //set lastName property to andy object (Person object)

console.log(andy); //Person { firstName: 'Teng Yung', lastName: 'andyNo.10' }
console.log(Person.prototype); //Person { lastName: 'Lin' }
console.log(andy.firstName + ", " + andy.lastName); //Teng Yung, andyNo.10
{% endhighlight %}

First javascript search for object's property **lastName**, and it cannot be found, so javascript continue to search object's prototype, and then ``lastName`` is **Person.property.lastName -> Lin**

after I set lastName property to Object, javascript won't search for prototype, cause the Object has it't own property called lastName.

------

You can chain lots of prototypes together, but there may have performance problems cause javascript engine has to trace and find property through your prototype chain.

Prototype Chain is a good way to implement inheritance feature. You can find more on MDN
[Inheritance and the prototype chain][Inheritance and the prototype chain]


[Inheritance and the prototype chain]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
