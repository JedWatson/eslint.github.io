---
title: Rule eqeqeq
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Require === and !== (eqeqeq)

It is considered good practice to use the type-safe equality operators `===` and `!==` instead of their regular counterparts `==` and `!=`.

The reason for this is that `==` and `!=` do type coercion which follows the rather obscure [Abstract Equality Comparison Algorithm](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3).
For instance, the following statements are all considered `true`:

 - `[] == false`
 - `[] == ![]`
 - `3 == "03"`

If one of those occurs in an innocent-looking statement such as `a == b` the actual problem is very difficult to spot.

## Rule Details

This rule is aimed at eliminating the type-unsafe equality operators.

The following patterns are considered warnings:

```js
if (x == 42) { ... }

if ("" == text) { ... }

if (obj.getStuff() != undefined) { ... }
```

### Options

- `"smart"`

This option enforces the use of `===` and `!==` except for these cases:

* Comparing two literal values
* Evaluating the value of `typeof`
* Comparing against `null`

You can specify this option using the following configuration:

```json
"eqeqeq": [2, "smart"]
```

The following patterns are considered okay and do not cause warnings:

```js
typeof foo == 'undefined'
'hello' != 'world'
0 == 0
true == true
foo == null
```

The following patterns are considered warnings with "smart":

```js

// comparing two variables requires ===
a == b

// only one side is a literal
foo == true
bananas != 1

// comparing to undefined requires ===
value == undefined
```

- `"allow-null"`

This option will enforce `===` and `!==` in your code with one exception - it permits comparing to `null` to check for `null` or `undefined` in a single expression.

You can specify this option using the following configuration:

```json
"eqeqeq": [2, "allow-null"]
```

The following pattern is considered okay and do not cause warnings:

```js
foo == null
```

The following patterns are considered warnings with "allow-null":

```js
bananas != 1
typeof foo == 'undefined'
'hello' != 'world'
0 == 0
foo == undefined
```

## When Not To Use It

If you don't want to enforce a style for using equality operators, then it's safe to disable this rule.

## Version

This rule was introduced in ESLint 0.0.2.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/eqeqeq.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/eqeqeq.md)
