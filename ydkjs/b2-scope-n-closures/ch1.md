# Chapter 1: What is Scope?

One of the most <b>fundamental paradigms</b> of nearly all programming languages is <b>the ability to store values in variables, and later retrieve or modify those values</b>. In fact, the ability to store values and pull values out of variables is what gives a program <b>state</b>.

=> where do those variables live? In other words, where are they stored? And, most importantly, how does our program find them when it needs them?

These questions speak to the need for a well-defined set of rules for storing variables in some location, and for finding those variables at a later time. We'll call that set of rules: Scope.

## Compiler Theory

JS in fact a compiled language, not a dynamic nor interpreted.

JavaScript engine performs many of the same steps, albeit in more sophisticated ways than we may commonly be aware, of any traditional language-compiler.

In a traditional compiled-language process, a chunk of source code, your program, will undergo typically three steps before it is executed, roughly called "compilation":

1. <b>Tokenizing/Lexing: </b>breaking up a string of characters into meaningful (to the language) chunks, called tokens.

e.g: `var a = 2;`.

This program would likely be broken up into the following tokens:

- `var`,
- `a`,
- `=`,
- `2`,
  and `;`.

Whitespace may or may not be persisted as a token, depending on whether it's meaningful or not.

2. <b>Parsing: </b> taking a stream (array) of tokens and turning it into a tree of nested elements, which collectively represent the grammatical structure of the program. This tree is called an "AST" (**A**bstract **S**yntax **T**ree).

3. <b>Code-Generation</b>: the process of taking an AST and turning it into executable code. This part varies greatly depending on the language, the platform it's targeting, etc.

So, rather than get mired in details, we'll just handwave and say that there's a way to take our above described AST for var a = 2; and turn it into a set of machine instructions to actually create a variable called a (including reserving memory, etc.), and then store a value into a.

The <b style="color: tomato;">JavaScript engine is vastly more complex than just those three steps</b>, as are most other language compilers. For instance, in the process of parsing and code-generation, there are certainly steps to optimize the performance of the execution, including collapsing redundant elements, etc.

JavaScript engines don't get the luxury of having plenty of time to optimize, because JavaScript compilation doesn't happen in a build step ahead of time, as with other languages.

## Understanding Scope

# Review

Scope is the set of rules that determines where and how a variable (identifier) can be looked-up. This look-up may be for the purposes of assigning to the variable, which is an LHS (left-hand-side) reference, or it may be for the purposes of retrieving its value, which is an RHS (right-hand-side) reference.

LHS references result from assignment operations. Scope-related assignments can occur either with the = operator or by passing arguments to (assign to) function parameters.
