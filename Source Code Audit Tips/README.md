# Source code audit tips

> This page contains multiple bugs for each specific languages, it may help us while auditing source code.

## Summary

- [Javascript](#javascript)
- [References](#references)

## PHP
TODO

## Javascript
#### Stupid bug while checking an input string using Javascript regex, for example `RegExp.prototype.test()` function.
```js
// this input can be used to bypass the regex validation
let userInputUrl = "javascript://alert(1);//https://something.example.com";

// this function only check a substring inside the user input url.
// the regex should contains ^ and $ for matching begin and end of string
if (/https:\/\/.*.example.com/.test(userInputUrl)) {
  location.href = userInputUrl;
}
```
- Ref: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test


#### DOM-based XSS bug with `Element.innerHTML` property.
```js
// this property is vulnerable to XSS, don't use it.
document.body.innerHTML = "<img src=x onerror=alert(1)>";
```

#### Vue.js XSS with v-html
```html
<!-- userInput = "<img src=x onerror=alert(1)>" -->

<div v-html="userInput"></div>
```

## Golang

#### Race condition in for-loop (common bug pattern)
```go
for _, v := range arr {
  go func () {
    // v will be changed while the for-loop is executing
    v.someMethod() // <- race condition bug happend here
  }();
}
```


## References

- [Blog title - Author, Date](https://example.com)