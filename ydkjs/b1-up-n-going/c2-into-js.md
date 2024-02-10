# Chapper 2: Into JS

## Values n Types

Js has typed values, not typed variables

1. `string`
2. `number`
3. `boolean`
4. `null` and `undefined`
5. `object`
6. `symbol` (ES6)

JavaScript provides a typeof operator that can examine a value and tell you what type it is:

typeof null is an interesting case, because it errantly returns "object", when you'd expect it to return "null".

## Objects

The object type refers to a compound value where you can set properties (named locations) that each hold their own values of any type. This is perhaps one of the most useful value types in all of JavaScript.

```js
var obj = {
  a: "hello world",
  b: 42,
  c: true,
};
```

Note: For more information on JavaScript objects, see the this & Object Prototypes title of this series, specifically Chapter 3.

## Array

An array is an object that holds values (of any type) not particularly in named properties/keys, but rather in numerically indexed positions. For example:

```js
var arr = ["hello world", 42, true];
```

## Function

The other object subtype you'll use all over your JS programs is a function:

```js
function foo() {
  return 42;
}

foo.bar = "hello world";

typeof foo; // "function"
typeof foo(); // "number"
typeof foo.bar; // "string"
```

Again, functions are a subtype of objects -- typeof returns "function", which implies that a function is a main type -- and can thus have properties, but you typically will only use function object properties (like foo.bar) in limited cases.

<b>Note</b>: For more information on JS values and their types, see the first two chapters of the Types & Grammar title of this series.

## Built-In Type Methods

The built-in types and subtypes we've just discussed have behaviors exposed as properties and methods that are quite powerful and useful.

```js
var a = "hello world";
var b = 3.14159;

a.length; // 11
a.toUpperCase(); // "HELLO WORLD"
b.toFixed(4); // "3.1416"
```

The "how" behind being able to call a.toUpperCase() is more complicated than just that method existing on the value.

Briefly, there is a String (capital S) object wrapper form, typically called a "native," that pairs with the primitive string type; it's this object wrapper that defines the toUpperCase() method on its prototype.

When you use a primitive value like "hello world" as an object by referencing a property or method (e.g., a.toUpperCase() in the previous snippet), JS automatically "boxes" the value to its object wrapper counterpart (hidden under the covers).

A string value can be wrapped by a String object, a number can be wrapped by a Number object, and a boolean can be wrapped by a Boolean object. For the most part, you don't need to worry about or directly use these object wrapper forms of the values -- prefer the primitive value forms in practically all cases and JavaScript will take care of the rest for you.

<b>Note</b>: For more information on JS natives and "boxing," see Chapter 3 of the Types & Grammar title of this series. To better understand the prototype of an object, see Chapter 5 of the this & Object Prototypes title of this series.

## Comparing Values

There are two main types of value comparison that you will need to make in your JS programs: _equality_ and _inequality_. The result of any comparison is a strictly boolean value (true or false), regardless of what value types are compared.

### Coercion

Coercion comes in two forms in JavaScript: explicit and implicit. Explicit coercion is simply that you can see obviously from the code that a conversion from one type to another will occur, whereas implicit coercion is when the type conversion can happen as more of a non-obvious side effect of some other operation.
