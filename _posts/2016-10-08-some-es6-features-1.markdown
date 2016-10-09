---
layout: post
title:  "Some ES6 features - PART1"
date:   2016-10-08 12:30:00 +0800
categories: javascript
---
Here are some ES6 features. I just make some note about some features that I usually use.

***


### **1. Default Value**
In ES6, you can set default variables value other then ``var test = test || 'defaultValue' ``

The following is some example about how ES6 set default value.

```javascript
function sayHello (name = 'world') {  //This line set the default name to 'world'
    console.log('hello ' + name + ' !');
}

sayHello(); // This print out : hello world !
sayHello('andy');  // This print out hello andy !
```

You can also set default variables to an object. Like...

```javascript
var defaultName = {name: 'Anonymous'};

function greetUser ( user = defaultName ) {
    console.log('Hello ' + user.name + ' !');
}

greetUser();
greetUser({name: 'andy'});
```

### **2. Template String**
You don't have to type lots of `` + `` and `` '' `` to insert variables into string in ES6. All you have to type is `` ` text ${variable}`  `` and you can put variables and string in side that black text. Here is example...

```javascript
function greet (name = 'andy') {
    console.log('hello ' + name + ' !');  //old syntax
    console.log(`Hello ${name} !`);  // Use ${variable} to represent variable
}

greet();
greet('andyNo.10');

//Use template strign straight in text
console.log(`1 + 6 = ${1 + 6}`);  //print 1 + 6 = 7

var author = { name: 'andy' };
var place = { nation: 'Taiwain', area: 'Asia'};
var message = `Hello, my name is ${author.name} and I am from ${place.nation}, ${place.area}. Nice to meet you ~ `;
console.log(message);

// Template string can tell 'enter'(new line)
console.log(`Hey,

This kindof content area!

--Andy`);

```

### **3. New way to declare variables : `const` `let`**
Javascirpt use `var` keyword to assign value to variable, but the problem is that `var` is local scoping (function scoping). Sometime I'll unwillingly change the value of that variable and hard to maintain variables.
So `const` `let` are some awesome new feature that make javascipt variable more convenient to maintian.

`const`

A **blocked-scoping**, **constant** variable. You cannot change the value of const variable and you must declare value just after your variable. Here are some example...

```javascript
const PORT = 3000;
// const a;  //const must assign value immidiately or ERROR occur
var Port = 3000;

console.log(PORT);

// PORT = 3001; //const cannot re-assign value or ERROR occur
Port = 3001;
console.log(Port);
```

`let`

A **blocked-scoping** variable that live inside any curly bracket. Like...

```javascript
var varVariable = 0;

if (true) {
    let letVaribale = 1;
    var varVariableinsideif = 2;
    console.log(letVaribale); //logout letVaribale
}

console.log(varVariableinsideif);
console.log(letVaribale); //this occur ERROR because the outside environment cannot get letVaribale instide if statement

for ( var i = 0; i < 3; i++) {
    console.log(i);  // This will print out i value in each loop, 0, 1, 2 in this case
}
console.log(i); // log out fianl i value, '3' in this case

for(let t = 0; t < 3; t++) {
    console.log(t); // This will print out t value in each loop, 0, 1, 2 in this case (means let live instide for loop)
}
console.log(t); //this occur ERROR because the outside environment cannot get t instide for statement```
```

`var`

This keyword is an old way to declare variable, I think we should not use this one to prevent variables disaster. Here is an [previous post][var scoping] about var scoping.

### **4. Arrow Function**

In ES6, We got an more easy way to write anonymous function. We can now use `(param1, param2) => { return param1 + param2 }` to represent  `function (param1, param2) { return param1 + param2 }`. The following are some example...

```javascript

var people = ['andy', 'nicky', 'faith'];

people.forEach(function (name) {
    console.log(name);
});

people.forEach( (name) => console.log(name));  //single line statement

people.forEach((name) => {
    console.log('welcome');
    console.log(name);
});

//Original function definition
function add (a, b) {
    return a + b;
}

console.log(add(2,9));

var multiply = (a, b) => { return a * b; };

console.log(multiply(2, 9));

```

### **5. For of**
`for of` let you have ability to customize each iteration behavior. You can do whatever you want to each value inside the target array. like...

```javascript
var locations = [];

locations.push({
    name: 'Taipei',
    weather: 22
});

locations.push({
    name: 'USA',
    weather: 18
});

for ( let locaion of locations ) {  //each location in locations array
    console.log(`It's ${locaion.weather} in ${locaion.name}`);
}

```

Here are some awesome features in ES6. I'll write more in PART2.

[var scoping]: [http://andyno10.github.io/javascript/2016/07/09/oh!-so-it-is-var-scoping.html]
