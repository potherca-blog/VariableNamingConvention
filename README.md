---
permalink: /
title: Variable Naming Convention for weak and/or dynamic typed languages
---

[![Project Stage Badge: Production Ready][project-stage-image]][project-stage-badge]
[![GitHub tag][GitHub tag badge]][GitHub latest release]

* auto-gen TOC:
{:toc}

## Introduction

This document explains the naming convention meant to be used with 
dynamic and/or weakly typed languages (as defined in [the Typing 
Quadrant on the Cunningham Wiki]) such as PHP, Javascript, Perl, and Bash.

The idea behind the coding convention is that a developer should be able 
to _**see**_ when something is wrong. Either when something from another 
scope is used without validation (parameters in public methods, for 
instance) or when a certain type is addressed as though it were another 
type.

## Stating the use of this Convention

To link to this convention from code, the following header is recommended:

    /**
     * @NOTE: The variable naming scheme used in this code is an adaption of
     * Systems Hungarian which is explained at http://blog.pother.ca/VariableNamingConvention/
     */

## The Convention

The convention used for variables is a derived form of Systems 
[Hungarian notation] that consist of a 3 part prefix: the Scope of a 
variable, a Delimiter, and the Type of a variable.

For variables in a closed scope (usually a function) the Scope and 
Delimiter are omitted and only the Type is prefixed. 

A delimiter is added in order to separate the scope from the rest of the 
name. This delimiter is a conscious eyesore to make variables from other 
scopes stand out, as using variables from another scope can lead to 
painful situations. 

Some languages require a variable name to start with a [sigil]. For 
developers used to such a language, Hungarian Notation will feel more 
natural than for developers used to languages that do not require sigils.

The letters used to denote the Scope and Type are explained in the 
"Scope" and "Type" sections below.

For the various languages this convention pertains to this gives us:

|  Language  |  Example  |      Sigil       |       Scope     |  Delimiter  |  Type  | Name |
| ---------- | --------- | ---------------- | --------------- | ----------- | ------ | ---- |
| BASH       | `$g_xFoo` | `$`              | `g`/`m`/`p`/`t` | `_`         | `x`    | Foo  |
| Javascript | `g_xFoo`  |                  | `g`/`m`/`p`/`t` | `_`         | `x`    | Foo  |
| Perl       | `$g_xFoo` | `$`/`@`/`%`/`&`  | `g`/`m`/`p`/`t` | `_`         | `x`    | Foo  |
| PHP        | `$g_xFoo` | `$`              | `g`/`m`/`p`/`t` | `_`         | `x`    | Foo  |

<small>
    Strictly speaking the `$` character used in Bash isn't truly a sigil 
    but  "an unary operator for lexical indirection". The effect, 
    however, is much the same.
</small>

### Scope

To help identify where variables come from and for easier fetching of 
name-lists in scope-aware editors, a scope flag is prefixed to variables 
that aren't in a function/method's closed scope.

Available flags for the scope are:

| Prefix | Scope | Rational |
| ------ | ----- | -------- |
| g | global | |
| t | temporary variables | variables that are created only to be temporarily used and then overwritten or discarded, as often occurs in loops.
| p | function parameters | Things from "the outside" can often _not_ be trusted. This prefix helps to indicate when values move across scopes. 
| m | class members |


### Types

- More [information about types in PHP is available in the PHP manual](http://php.net/manual/en/language.types.intro.php)
- More information about types in Javascript is available in [the MDN page on JavaScript data types and data structures](http://php.net/manual/en/language.types.intro.php)
- More information about types in Bash is available in the Linux Documentation Project on the [Bash Guide page about Types of variables](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_10_01.html)

| Prefix |     Type     |  Language(s)  | Category  | Notes |
| ------ | -------------| ------------- | --------- | ----- |
| $      | jQuery Object| JS            | Other     | Only relevant when working with code that uses the jQuery Library. <sup>[1]</sup><sup>[2]</sup>
| a      | Array        | BASH/JS/PHP   | Compound  |   |
| b      | Boolean      | BASH/JS/PHP   | Scalar    |   |
| c      | Callback     | BASH/JS/PHP   | Other     | A callback, also known as a Function.<sup>[3]</sup>
| f      | " | " | " | "
| d      | Double       | BASH/JS<sup>[4]</sup>/PHP   | Scalar    | A double, also know as a "Float", a floating-point number. |
| i      | Integer      | BASH/JS<sup>[4]</sup>/PHP   | Scalar    |   |
| j      | (reserved)   | JS            | Other     | Set aside just in case the `$` character (for jQuery Objects) is to be replaced. See <sup>[2]</sup>. |
| m      | Mixed        | BASH/JS/PHP   | Other     |   |
| n      | Numeric      | BASH/JS/PHP   | Scalar    | Can be either an integer or a numeric string <sup>[5]</sup>.
| o      | Object       | JS/PHP        | Compound  |   |
| r      | Resource     | PHP           | Other     |   |
| s      | String       | BASH/JS/PHP   | Scalar    |   |
| u      | Unknown      | BASH/JS/PHP   | Other     |   |

#### Notes
1. In the Angular framework the dollar character `$` has other significant, denoting a variable, parameter, property, or method that belongs to the core of Angular and prevent elements from being iterated (or interpreted) in certain directives.
2. The fact that this character can lead to confusion as it is a sigil in other languages has lead to the idea that it might be better to use `j` for jQuery objects instead. That idea is still under revision.
3. In Bash this refers to variables declared with the `-f` flag.
4. Javascript only has one "Number" type which is used for both floating-point numbers and integers
5. A string that has a value that represents an integer or double.

- Javascript (since ES6) has a "Symbol" type (also know as "Atoms" in other languages, similar to enumeration types).
  In PHP the closest thing to this is using a [Constant](http://php.net/manual/en/language.constants.php).
  The Bash equivalent is declaring a variable readonly with the `-r` flag.
  As Symbols/Constants are the familiar exceptional to the rule and do
  not adhere to this standard. they should be declared in so called SCREAMING_SNAKE_CASE<sup>[6](https://www.google.nl/search?hl=en&q=%22SCREAMING_SNAKE_CASE%22)</sup>

### Name

The "Name" part of a variable should describe what the variable is in 
the problem domain it represents. Be as descriptive as possible but 
hold these two rules of thumb in the back of your head when coming up
with a name:

- Variable names should suggest a property or noun. UserName, Width, etc.
- Names should be descriptive, but also concise. Wherever possible, keep 
variable names to under 3 words or 15 characters but  be prepared to 
sacrifice a few extra characters to improve clarity.

##  Syntax Diagram

Putting all of this together we get the following syntax diagram:

    VariableName ::=  ( [$@%&]* ([gmpt] '_')*  [abcdfijmnorsu$] [A-Z] [a-zA-Z0-9]+ )

![Railroad Diagram][Railroad Diagram]

<sup>Generated using the [Railroad Diagram Generator]</sup>

## History

This convention has been evolving ever since [Potherca] started 
programming Perl in the mid-nineties and branched out into PHP in the 
early noughties. Yet it was never put into writing until encourage to do 
so by [Sander Krause] in 2009.

## Copyright

<p class="created-by">
    <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">
        <img alt="Creative Commons Licence" style="border-width:0" src="http://i.creativecommons.org/l/by/4.0/88x31.png" />
    </a><br />
    The <span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">
        <a xmlns:dct="http://purl.org/dc/terms/" href="http://pother.ca/VariableNamingConvention/" rel="dct:source">
            Variable Naming Convention
        </a>
    </span> by
    <a xmlns:cc="http://creativecommons.org/ns#" property="cc:attributionName" rel="cc:attributionURL"
       href="http://pother.ca/" class="potherca"
    >Potherca</a> and
    <a xmlns:cc="http://creativecommons.org/ns#" href="https://twitter.com/sanderkrause" property="cc:attributionName" rel="cc:attributionURL">
        Sander Krause
    </a> is licensed under the
    <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">
        Creative Commons Attribution 4.0 International License
    </a>
    .
</p>

[project-stage-badge]: http://bl.ocks.org/potherca/raw/a2ae67caa3863a299ba0
[project-stage-image]: http://img.shields.io/badge/Project%20Stage-Production%20Ready-brightgreen.svg 
[GitHub tag badge]: https://img.shields.io/github/tag/potherca-blog/VariableNamingConvention.svg
[GitHub latest release]: https://github.com/potherca-blog/VariableNamingConvention/releases/latest
[Hungarian notation]: http://en.wikipedia.org/wiki/Hungarian_notation
[sigil]: https://en.wikipedia.org/wiki/Sigil_(computer_programming)
[the Typing Quadrant on the Cunningham Wiki]: http://c2.com/cgi/wiki?TypingQuadrant
[Potherca]: https://pother.ca/
[Sander Krause]: https://twitter.com/sanderkrause
[Railroad Diagram Generator]: http://bottlecaps.de/rr/ui
[Railroad Diagram]: http://blog.pother.ca/VariableNamingConvention/syntax-diagram.svg
