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
     * Systems Hungarian which is explained at http://pother.ca/VariableNamingConvention/
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

### Scope

To help identify where variables come from and for easier
fetching of name-lists in scope-aware editors, we prepend a
scope flag to variables that aren't in a function/method's closed scope.
Available flags for the scope are:

- <span class="main">g</span> for global variables <span
        class="small">(These shouldn't really exist, 'cause we <em>really</em>
    don't want any global var lying about. Use <code>$_SERVER</code>, <code>$_SESSION</code> or <code>$_SETTINGS</code>
    instead) </span>
- <span class="main">t</span> for localized temporary variables
  <span class="small">(variables that are created only to be
  temporaraly used and then overwritten or discarded, as often occurs in
  loops.)
- <span class="main">p</span> for a function/method parameter
- <span class="main">m</span> for class members

### Types

Because PHP is a loosely typed language, undesired effects (and
thus bugs) can easily arise if you do not check your var types properly.
Because we don't want to have to skip back to the point where a var was
set (and because we like readable code), we prepend a type flag to
variables. Please be <em>very</em> aware of the fact that this flag is
mostly a <span class="">hint</span> and can't be trusted blindly,
even when taking our Best Practises into account. Available flags for
variable types are:

#### Compound Types

- <span class="main">a</span> for an <strong>Array</strong>
- <span class="main">e</span> for an <strong>Exception</strong>
  <div class="reasoning"><span class="handle">reasoning</span>
  <span>
  Dispite the fact that Exceptions are objects we feel they differ
  enought from "normal" objects to validate their own type.
  </span>
  </div>
- <span class="main">o</span> for an <strong>Object</strong> <span
  class="small">(Please
  note this means an instance of a class, not the class itself. If it has
  not been constructed, it is <em>not</em> an object)</span>

#### Scalar Types

- <span class="main">u</span> for an
    <strong>unknown</strong> type <span
        class="small">(this should <em>only</em> be used for skeleton
    methods where it has not yet been decided what type a parameter should
    be.</span>
- <span class="main">v</span> for a
    <strong>variant</strong> type <span
        class="small">(used only when updating old/deprecated code to
    the current coding convention. Newer code should adhere to the rule
    "Use type safe coding") </span>
- <span class="main">n</span> for a <strong>numeric</strong> string (an
                                integer /
                                double / decimal / float represented as a
                                string)
    <div class="reasoning"><span class="handle">reasoning</span> <span>Because
    PHP is a loosely type cast language, any variable that needs to be an
    integer or double should be type cast as such as early as possible in the
    code. The use of <code>n</code> (numeric) anywhere in the bussiness logic
    should be a warning that bad things might happen. (PHP interprets "1" and 1
    pretty much the same for MOST situations, but the result may be different
    than you think. Avoid speculation. <em>Type cast</em>!)</span></div>
- <span class="main">i</span> for an <strong>integer</strong> <span
        class="small">(and
    I do mean <em>integer</em>, not a numeric string!)</span>
- <span class="main">d</span> for a <strong>decimal</strong>/double/float
- <span class="main">b</span> for a <strong>boolean</strong>
- <span class="main">s</span> for a <strong>string</strong>

#### Special Types

- <span class="main">r</span> for a <a
    href="http://php.net/manual/language.types.resource.php"><strong>Resource</strong></a>
<span class="small">(see <a
        href="http://php.net/manual/resource.php">http://php.net/manual/resource.php</a>
for a full list of Resource Types)</span>

### Name

- <span class="">Variable names should suggest a
property or noun.</span> UserName, Width, etc.
- <span class="">Names should be descriptive, but
also concise.</span> Wherever possible, keep variable names to under 3 
words or 15 characters but be prepared to sacrifice a few extra 
characters to improve clarity.

##  Syntax Diagram

Putting all of this together we get the following syntax diagram:

    Variable ::=  [gmpt]_[abdeinorsu]([A-Z][a-zA-Z0-9])

![Railroad Diagram][Railroad Diagram]

<sup>Generated using the [Railroad Diagram Generator]</sup>

## History

This convention has been evolving ever since [Potherca] started 
programming Perl in the min-nineties and branched out into PHP in the 
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
[GitHub tag badge]: https://img.shields.io/github/tag/potherca/VariableNamingConvention.svg
[GitHub latest release]: https://github.com/Potherca/VariableNamingConvention/releases/latest
[Hungarian notation]: http://en.wikipedia.org/wiki/Hungarian_notation
[sigil]: https://en.wikipedia.org/wiki/Sigil_(computer_programming)
[the Typing Quadrant on the Cunningham Wiki]: http://c2.com/cgi/wiki?TypingQuadrant
[Potherca]: http://pother.ca/
[Sander Krause]: https://twitter.com/sanderkrause
[Railroad Diagram Generator]: http://bottlecaps.de/rr/ui
[Railroad Diagram]: http://pother.ca/VariableNamingConvention/syntax-diagram.svg
