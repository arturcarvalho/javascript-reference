# Javascript Reference

## typeof null is object

The type of null is not null as expected. It's object.

```javascript
// www.justjavascript.com
typeof null === "object"; // true
```

## Add element at the beginning (left) of the array using the spread operator.

```javascript
const arr = [1, 2, 3];
return [0, ...arr]; // [0, 1, 2, 3]
```

## Add element at the beginning (left) of the array using unshift.

```javascript
const arr = [1, 2, 3];
arr.unshift(0); // returns new length: 4
return arr; // [0, 1, 2, 3]
```

## Add element at end (right) of the array using the spread operator.

```javascript
const arr = [1, 2, 3];
return [...arr, 4]; // [1, 2, 3, 4]
```

## Add element at the end (right) of the array using push.

```javascript
const arr = [1, 2, 3];
arr.push(4); // returns new length: 4
return arr; // [1, 2, 3, 4]
```

## Capitalize first letter

```javascript
// https://stackoverflow.com/a/1026087/1013
function capitalizeFirstLetter(string) {
  return string.charAt(0).toUpperCase() + string.slice(1);
}
```

## Get random item from array

```javascript
// https://stackoverflow.com/a/5915122/1013
function rand(items) {
  return items[Math.floor(Math.random() * items.length)];
}
```

## Falsy values

There are only **6 falsy values**. The others are truthy.

```javascript
// https://developer.mozilla.org/en-US/docs/Glossary/Falsy
function f() {
  // prettier-ignore
  return [
      Boolean(false),
      Boolean(''),
      Boolean(``),
      Boolean(""),
      Boolean(0),
      Boolean(-0),
      Boolean(NaN),
      Boolean(null),
      Boolean(undefined)]
}
f(); // [false, false, false, false, false, false, false, false, false]
```

## Unexpected Truthy Values

```javascript
// https://developer.mozilla.org/en-US/docs/Glossary/Falsy
function f() {
  return [
    Boolean(new Boolean(false)),
    Boolean("false"),
    Boolean({}),
    Boolean([]),
    Boolean(-1),
  ];
}
f(); // [true, true, true, true, true]
```

## Double bang is the same as Boolean

```javascript
!!0; // false
```

## Right associative makes a global variable

```javascript
// https://stackoverflow.com/questions/1758576/multiple-left-hand-assignment-with-javascript/1758912#1758912
function f() {
  //prettier-ignore
  var a1 = a2 = 1 // this is like var a1 = (a2 = 1)
  //prettier-ignore
  var b1 = 1, b2 = 1
  return [window.a1, window.a2, window.b1, window.b2];
}

f(); // [undefined, 1, undefined, undefined]
```

## Main types

```javascript
// 2020-5-8
// bigint at 70% https://caniuse.com/#feat=bigint
// symbol 93% https://caniuse.com/#feat=mdn-javascript_builtins_symbol

typeof undefined; // "undefined"
typeof null; // "object"
typeof true; // "boolean"
typeof 1; // "number"
typeof 1.1; // "number"
typeof 2n; // "bigint"
typeof "some text"; // "string
typeof Symbol("some value"); // "symbol"
typeof function g() {}; // "function"
typeof {}; // "object"
typeof []; // "object"
typeof new Date(); // "object"
```

## Double typeof

```javascript
typeof typeof 10; // "string" (typeof returns string "number")
```

## Promises vs setTimeout

```javascript
// What the heck is the event loop https://www.youtube.com/watch?v=8aGhZQkoFbQ
// Jaffa Cake Asia: https://www.youtube.com/watch?v=cCOL7MC4Pl0
// Sync BEFORE promises (microtask) BEFORE settimeout (macrotask)
const result = [];
function f() {
  setTimeout(() => {
    result.push("settimeout");
  }, 0);
  Promise.resolve().then(() => result.push("promise"));
  Promise.resolve().then(
    result.push("this is not a function, so it executes sync")
  );
  result.push("sync");
}
f();
setTimeout(() => {
  console.log(result);
}, 1);
```

## bigints have comparison gotchas

```javascript
// https://javascript.info/bigint

2n > 1; // true
1n > 1; // false
1n == 1; // true
1n === 1; // false
1n < 1; // false
```

## Automatic semicolon insertion

```javascript
//  ASI https://stackoverflow.com/a/2846298/1013
function f() {
  return {
    a: "hello",
  };
}

function g() {
  return;
  {
    a: "hello";
  }
}

f(); // {a: "hello"}
g(); // undefined
```

## Infinity

```javascript
//
function f() {
  return 2 / 0 === Infinity;
}
f(); // true
```

## Not a Number

```javascript
Number.isNaN(0 / 0); // true
Number.isNaN("hey" / 0); // true
Number.isNaN("hey"); // false
```

## Floating point math error

```javascript
// https://0.30000000000000004.com/
// For some reason JS is famous for this, but there are many languages
// that do the same.
// A way to think of it is it's like 1/3 is 0.3333(3) on base10.
// In base2 this thing happens for 0.1 + 0.2.

0.1 + 0.2 == 0.3; // false
0.1 + 0.2 === 0.3; // false
0.1 + 0.2; // 0.30000000000000004
```

## palindrome in less than 160 characters

```javascript
// The same word if written back and forth.
// https://www.toptal.com/javascript/interview-questions
function f(str) {
  return str === str.split("").reverse().join("");
}

f("aba"); // true
f("aab"); // false
```

# Notes

`mdjs` and `mdjsf` to add snippets on vscode. Don't forget the ctrl + space!
