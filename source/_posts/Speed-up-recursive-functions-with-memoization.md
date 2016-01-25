title: Speed up recursive functions with memoization
date: 2016-01-25 10:10:17
tags:
 - JavaScript
categories:
 - 技术杂谈
---

Fibonacci sequence is very familiar to everybody. we can write the following function in 20 seconds.
```js
var fibonacci = function(n){
    return n <= 1 ? n : fibonacci(n-1) + fibonacci(n-2);
}
```
it works, but not efficient. it did lots of duplicate computing works, we can cache its previously computed results to speed it up.
```js
var fibonacci = (function(){
    var cache = {
        0: 0,
        1: 1
    };
    return function(n){
        return n <= 1 ? cache[n] : (cache[n] = cache[n-1] + cache[n-2]);
    }
})()
```
Also, we can define a higher-order function that accepts a function as its argument and returns a memoized version of the function.
```js
var memoize = function(func){
    var cache = {};
    return function(){
        var key = Array.prototype.slice.call(arguments).toString();
        return key in cache ? cache[key] : (cache[key] = func.apply(this,arguments));
    }
}
fibonacci = memoize(fibonacci);
```
we can use `memoize()` in many other situations
* GCD(Greatest Common Divisor)

```js
var gcd = memoize(function(a,b){
    var t;
    if (a < b) t=b, b=a, a=t;
    while(b != 0) t=b, b = a%b, a=t;
    return a;
})
gcd(27,183); //=> 3
```
* Factorial calculation

```js
var factorial = memoize(function(n) {
    return (n <= 1) ? 1 : n * factorial(n-1);
})
factorial(5); //=> 120
```
