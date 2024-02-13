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

### Trusy and Falsy

The specific list of "falsy" values in JavaScript is as follows:

- `""` (empty string)
- `0`, `-0`, `NaN` (invalid number)
- `null`, `undefined`
- `false`

Any value that's not on this "falsy" list is "truthy." Here are some examples of those:

- `"hello"`
- `42`
- `true`
- `[ ]`, `[ 1, "2", 3 ]` (arrays)
- `{ }`, `{ a: 42 }` (objects)
- `function foo() { .. }` (functions)

It's important to remember that a non-boolean value only follows this "truthy"/"falsy" coercion if it's actually coerced to a boolean. It's not all that difficult to confuse yourself with a situation that seems like it's coercing a value to a boolean when it's not.

### Equality

There are four equality operators: ==, ===, !=, and !==. The ! forms are of course the symmetric "not equal" versions of their counterparts; non-equality should not be confused with inequality.

The difference between == and === is usually characterized that == checks for value equality and === checks for both value and type equality. However, this is inaccurate. The proper way to characterize them is that == checks for value equality with coercion allowed, and === checks for value equality without allowing coercion; === is often called "strict equality" for this reason.

Consider the implicit coercion that's allowed by the == loose-equality comparison and not allowed with the === strict-equality:

```js
var a = "42";
var b = 42;

a == b; // true
a === b; // false
```

We're not going to cover all the nitty-gritty details of how the coercion in == comparisons works here. Much of it is pretty sensible, but there are some important corner cases to be careful of. You can read section 11.9.3 of the ES5 specification (http://www.ecma-international.org/ecma-262/5.1/) to see the exact rules, and you'll be surprised at just how straightforward this mechanism is, compared to all the negative hype surrounding it.

To boil down a whole lot of details to a few simple takeaways, and help you know whether to use `==` or `===` in various situations, here are my simple rules:

- If either value (aka side) in a comparison could be the true or false value, avoid == and use ===.
- If either value in a comparison could be one of these specific values (0, "", or [] -- empty array), avoid == and use ===.
- In all other cases, you're safe to use ==. Not only is it safe, but in many cases it simplifies your code in a way that improves readability.

<b style="color:tomato;">Note </b>You should take special note of the `==` and `===` comparison rules if you're comparing two non-primitive values, like objects (including function and array). Because those values are actually held by reference, both == and === comparisons will simply check whether the references match, not anything about the underlying values.

`Note`: For more information about the == equality comparison rules, see the ES5 specification (section 11.9.3) and also consult Chapter 4 of the Types & Grammar title of this series; see Chapter 2 for more information about values versus references.

### Inequality

The <, >, <=, and >= operators are used for inequality, referred to in the specification as "relational comparison." Typically they will be used with ordinally comparable values like numbers. It's easy to understand that 3 < 4.

```js
var a = 41;
var b = "42";
var c = "43";

a < b; // true
b < c; // true
```

What happens here? In section 11.8.5 of the ES5 specification, it says that if both values in the < comparison are strings, as it is with b < c, the comparison is made lexicographically (aka alphabetically like a dictionary). But if one or both is not a string, as it is with a < b, then both values are coerced to be numbers, and a typical numeric comparison occurs.

```js
var a = 42;
var b = "foo";

a < b; // false
a > b; // false
a == b; // false
```

Wait, how can all three of those comparisons be false? Because the b value is being coerced to the "invalid number value" NaN in the < and > comparisons, and the specification says that NaN is neither greater-than nor less-than any other value.

The == comparison fails for a different reason. a == b could fail if it's interpreted either as 42 == NaN or "42" == "foo" -- as we explained earlier, the former is the case.

`Note`: For more information about the inequality comparison rules, see section 11.8.5 of the ES5 specification and also consult Chapter 4 of the Types & Grammar title of this series.

## Variables

In JavaScript, variable names (including function names) must be valid identifiers. The strict and complete rules for valid characters in identifiers are a little complex when you consider nontraditional characters such as Unicode. If you only consider typical ASCII alphanumeric characters though, the rules are simple.

An identifier must start with a-z, A-Z, $, or \_. It can then contain any of those characters plus the numerals 0-9.

`Note`: For more information about reserved words, see Appendix A of the Types & Grammar title of this series.

### Function Scopes

You use the var keyword to declare a variable that will belong to the current function scope, or the global scope if at the top level outside of any function.

<b>Hoisting</b>

Wherever a var appears inside a scope, that declaration is taken to belong to the entire scope and accessible everywhere throughout.

Metaphorically, this behavior is called hoisting, when a var declaration is conceptually "moved" to the top of its enclosing scope. Technically, this process is more accurately explained by how code is compiled, but we can skip over those details for now.

```js
var a = 2;

foo(); // works because `foo()`
// declaration is "hoisted"

function foo() {
  a = 3;

  console.log(a); // 3

  var a; // declaration is "hoisted"
  // to the top of `foo()`
}

console.log(a); // 2
```

<b>Nested Scopes</b>

When you declare a variable, it is available anywhere in that scope, as well as any lower/inner scopes. For example:

```js
function foo() {
  var a = 1;

  function bar() {
    var b = 2;

    function baz() {
      var c = 3;

      console.log(a, b, c); // 1 2 3
    }

    baz();
    console.log(a, b); // 1 2
  }

  bar();
  console.log(a); // 1
}

foo();
```

If you try to access a variable's value in a scope where it's not available, you'll get a ReferenceError thrown. If you try to set a variable that hasn't been declared, you'll either end up creating a variable in the top-level global scope (bad!) or getting an error, depending on "strict mode" (see "Strict Mode"). Let's take a look:

```js
function foo() {
  a = 1; // `a` not formally declared
}

foo();
a; // 1 -- oops, auto global variable :(
```

Note: For more information about scope, see the Scope & Closures title of this series. See the ES6 & Beyond title of this series for more information about let block scoping.

## Conditionals

## Functions As Values

## Closure

Closure is one of the most important, and often least understood, concepts in JavaScript. I won't cover it in deep detail here, and instead refer you to the Scope & Closures title of this series. But I want to say a few things about it so you understand the general concept. It will be one of the most important techniques in your JS skillset.

You can think of closure as a way to "remember" and continue to access a function's scope (its variables) even once the function has finished running.

```js
function makeAdder(x) {
  // parameter `x` is an inner variable

  // inner function `add()` uses `x`, so
  // it has a "closure" over it
  function add(y) {
    return y + x;
  }

  return add;
}
```

The reference to the inner `add(..)` function that gets returned with each call to the outer `makeAdder(..)` is able to remember whatever x value was passed in to `makeAdder(..)`. Now, let's use `makeAdder(..)`:

```js
// `plusOne` gets a reference to the inner `add(..)`
// function with closure over the `x` parameter of
// the outer `makeAdder(..)`
var plusOne = makeAdder(1);

// `plusTen` gets a reference to the inner `add(..)`
// function with closure over the `x` parameter of
// the outer `makeAdder(..)`
var plusTen = makeAdder(10);

plusOne(3); // 4  <-- 1 + 3
plusOne(41); // 42 <-- 1 + 41

plusTen(13); // 23 <-- 10 + 13
```

<b>Modules</b>

The most common usage of closure in JavaScript is the module pattern. Modules let you define private implementation details (variables, functions) that are hidden from the outside world, as well as a public API that is accessible from the outside.

```js
function User() {
  var username, password;

  function doLogin(user, pw) {
    username = user;
    password = pw;

    // do the rest of the login work
  }

  var publicAPI = {
    login: doLogin,
  };

  return publicAPI;
}

// create a `User` module instance
var fred = User();

fred.login("fred", "12Battery34!");
```

The `User()` function serves as an outer scope that holds the variables username and password, as well as the inner `doLogin()` function; these are all private inner details of this User module that cannot be accessed from the outside world.

<b style="color: yellow;">Warning</b>: We are not calling new User() here, on purpose, despite the fact that probably seems more common to most readers. User() is just a function, not a class to be instantiated, so it's just called normally. Using new would be inappropriate and actually waste resources.

<b>`this` Identifier</b>

Another very commonly misunderstood concept in JavaScript is the this identifier. Again, there's a couple of chapters on it in the this & Object Prototypes title of this series, so here we'll just briefly introduce the concept.

While it may often seem that this is related to "object-oriented patterns," in JS `this` is a different mechanism.

If a function has a `this` reference inside it, that `this` reference usually points to an `object`. But which `object` it points to depends on how the **function was called**.

It's important to realize that this does not refer to the function itself, as is the most common misconception.

**Note**: For more information about this, see [Chapters 1 and 2 of the this & Object Prototypes](#TBD) title of this series.

## Prototypes

The prototype mechanism in JavaScript is quite complicated. We will only glance at it here. You will want to spend plenty of time reviewing [Chapters 4-6 of the this & Object Prototypes](#TBD) title of this series for all the details.

When you reference a property on an `object`, if that property doesn't exist, JavaScript will automatically use that object's internal prototype reference to find another `object` to look for the property on. You could think of this almost as a fallback if the property is missing.

The internal prototype reference linkage from one object to its fallback happens at the time the object is created. The simplest way to illustrate it is with a built-in utility called `Object.create(..)`.

```js
var foo = {
  a: 42,
};

// create `bar` and link it to `foo`
var bar = Object.create(foo);

bar.b = "hello world";

bar.b; // "hello world"
bar.a; // 42 <-- delegated to `foo`
```

```mermaid
graph TD
    A[a:42]-->|prototype link|B[b:"hello world"]
```

This linkage may seem like a strange feature of the language. The most common way this feature is used -- and I would argue, abused -- is to try to emulate/fake a "class" mechanism with "inheritance."

But a more natural way of applying prototypes is a pattern called "behavior delegation," where you intentionally design your linked objects to be able to delegate from one to the other for parts of the needed behavior.

<b>Note</b>: For more information about prototypes and behavior delegation, see [Chapters 4-6 of the this & Object Prototypes](#TBD) title of this series.

## Review

The first step to learning JavaScript's flavor of programming is to get a basic understanding of its core mechanisms like values, types, function closures, this, and prototypes.

Of course, each of these topics deserves much greater coverage than you've seen here, but that's why they have chapters and books dedicated to them throughout the rest of this series. After you feel pretty comfortable with the concepts and code samples in this chapter, the rest of the series awaits you to really dig in and get to know the language deeply.

The final chapter of this book will briefly summarize each of the other titles in the series and the other concepts they cover besides what we've already explored.
