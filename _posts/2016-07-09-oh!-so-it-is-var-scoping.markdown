---
layout: post
title:  "Oh! So it is \"var\" scoping"
date:   2016-07-09 16:30:00 +0800
categories: javascript
---
javascript scoping is **lexical**. I can't totally understand that meaning until I read a book [Eloquent Javascript - nested scope](http://eloquentjavascript.net/03_functions.html#h_c/Ms2Ed/N0).

I understand that each function has it's own scope. The following show some code.

``` javascript

var parent = function(){
    var result ='';

    var child1 = function(length1){
        var b = '_ ';
        for (var i = 0; i < length1; i++) {
            result += b;
            //this will log i variable in for loop
            console.log(i);
        }
    }

    var child2 = function(length2){
        var c = '0';
        for(var j=0; j<=length2; j++){
            result += c;
        }
    }

    // You cannot access b variable in child1()
    // console.log(b);
    child1(2);
    child2(3);
    child1(4);
    child2(6);

    return result;

}

console.log(parent());

// result : _ _ 0000_ _ _ _ 0000000

```


In this case we can see that `child1()` and `child2()` can access to `result` variable since they are inside `parent()` that define `result` variable.
But `parent()` function cannot access any variable inside child function.

Each function can access its outer function variable. The set of variable visible inside a funciton is determined by the place of that function in the **programing text**. And this is called **lexiczl scoping**.

**NOTE :**

> Javascript scoping is not defined by any block of code inside `{ } ` but it is defined by `function`.

``` javascript
var testBrace = function(){
    var outsideBrace = 'outsideValue';

    if(true){
        var insideBrace = 'insideValue'
    }

    console.log(insideBrace);
}

testBrace();

//result: insideValue

```

We can access variable outside `if` statement event if there are braces wrapping `insideBrace`.

In both example, I understand that **`var` keyword create variables which local to the enclosing function** not enclosing block (braces ).

> Note :
> ES6 have `let` keyword that create variables local to enclosing block (braces).
