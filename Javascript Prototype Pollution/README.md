# Javascript prototype pollution

> Prototype Pollution is a vulnerability affecting JavaScript. Prototype Pollution refers to the ability to inject properties into existing JavaScript language construct prototypes, such as objects. JavaScript allows all Object attributes to be altered, including their magical attributes such as `__proto__`, `constructor` and `prototype`. An attacker manipulates these attributes to overwrite, or pollute, a JavaScript application object prototype of the base object by injecting other values. Properties on the Object.prototype are then inherited by all the JavaScript objects through the prototype chain. When that happens, this leads to either denial of service by triggering JavaScript exceptions, or it tampers with the application source code to force the code path that the attacker injects, thereby leading to remote code execution.

## Summary

- [Vulnerable code](#vulnerable-code)

## Vulnerable code

Get the object constructor function via `constructor` property, change `prototype` property of the constructor function.
```js
x = {};
x.constructor.prototype.test = "test";
y = {};
console.log(y.test); // Output: test
```

We can access the object's prototype using `__proto__` via object instance.
```js
x = {};
x.__proto__.test = "test";
y = {};
console.log(y.test); // Output: test
```

## References

- https://github.com/Kirill89/prototype-pollution-explained