# Chapter 3: Into YDKJS

Serious developers in other languages expect to put in the effort to learn most or all of the language(s) they primarily write in, <b>but JS developers seem to stand out from the crowd</b> in the sense of typically <b>not learning very much of the language</b>. This is not a good thing, and it's not something we should continue to allow to be the norm.

The You Don't Know JS (YDKJS) series stands in stark contrast to the typical approaches to learning JS, and is unlike almost any other JS books you will read. <b>It challenges you to go beyond your comfort zone and to ask the deeper "why" questions for every single behavior you encounter</b>. Are you up for that challenge?

## Scope n Closures

One of the most fundamental things you'll need to quickly come to terms with is how scoping of variables really works in JavaScript.

Is JS an "interpreted language" and therefore not compiled. Nope.

The JS engine compiles your code right before (and sometimes during!) execution. So we use some deeper understanding of the compiler's approach to our code to understand how it finds and deals with variable and function declarations. Along the way, we see the typical metaphor for JS variable scope management, "Hoisting."

This critical understanding of "lexical scope" is what we then base our exploration of closure.

Closure is perhaps the single most important concept in all of JS, but if you haven't first grasped firmly how scope works, closure will likely remain beyond your grasp.

## this & Object Prototypes

One of the <b>most widespread and persistent mistruths about JavaScript</b> is that the <b style="color: tomato">`this` keyword refers to the function it appears in</b>. Terribly mistaken.

The `this` keyword is _dynamically bound_ based on how the function in question is executed, and it turns out there are **four simple rules** to understand and fully determine this binding.

Prototype mechanism, _which is a look-up chain for properties_, similar to how lexical scope variables are found. But wrapped up in the prototypes is the other huge miscue about JS: the idea of emulating (fake) `classes` and (so-called "prototypal") inheritance.

Read more about [Behavior Delelgation - or prototypal inheritance](https://www.linkedin.com/pulse/behavior-delegation-javascript-yogita-singla)

Delegation is an entirely different, and more powerful, design pattern, one that replaces the need to design with classes and inheritance.

## Types & Grammar

## Async & Performance

patterns on top of the language mechanics for managing asynchronous programming

Asynchrony is not only critical to the performance of our applications, it's increasingly becoming the critical factor in writability and maintainability.

The book starts first by clearing up a lot of terminology and concept confusion around things like "async," "parallel," and "concurrent," and explains in depth how such things do and do not apply to JS.

examining _callbacks as the primary method of enabling asynchrony_. But it's here that we quickly see that the _callback alone is hopelessly insufficient for the modern demands of asynchronous programming_. We identify <b>two major deficiencies of callbacks-only coding: Inversion of Control (IoC) trust loss and lack of linear reason-ability.</b>

To address these two major deficiencies, ES6 introduces two new mechanisms (and indeed, patterns): promises and generators.

**Promises** are a time-independent wrapper around a "future value," which lets you reason about and compose them regardless of if the value is ready or not yet. Moreover, they effectively solve the IoC trust issues by routing callbacks through a trustable and composable promise mechanism.

Generators introduce a new mode of execution for JS functions, whereby the generator can be paused at `yield` points and be resumed asynchronously later. The pause-and-resume capability enables synchronous, sequential looking code in the generator to be processed asynchronously behind the scenes. By doing so, we address the non-linear, non-local-jump confusions of callbacks and thereby make our asynchronous code sync-looking so as to be more reason-able.

Writing JavaScript effectively means writing code that can break the constraint barriers of being run dynamically in a wide range of browsers and other environments. It requires a lot of intricate and detailed planning and effort on our parts to take a program from "it works" to "it works well."
