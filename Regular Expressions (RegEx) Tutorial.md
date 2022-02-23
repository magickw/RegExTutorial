# Regular Expressions (RegEx) Tutorial

A regular expression (shortened as regex or regexp) is a sequence of characters that specifies a search pattern in text. Regex is supported in all scripting languages (such as Perl, Python, PHP, and JavaScript); as well as general purpose programming languages such as Java. This tutorial explains how a specific regular expression, functions by breaking down each part or component i.e. #regex-components of the expression and describing what it does.

## Summary

In many programming languages, programmers use regular expressions to search through text, test if the input of a program is correct, and check if the users made mistakes. For example, the following regular expression can be used to verify if the user's input is a valid email address:

    /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

It looks daunting. Actually, it can be broken down into a series of letters, digits, dots, underscores, `%` signs and hyphens, followed by an `@` sign, followed by another series of letters, digits and hyphens, finally followed by a single dot and two or more letters. With that being said, this pattern describes an email address.

In order to better understand how does this regular expression work, I will break it down in details below.

## Table of Contents

- [Regular Expressions (RegEx) Tutorial](#regular-expressions-regex-tutorial)
  - [Summary](#summary)
  - [Table of Contents](#table-of-contents)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [Grouping Constructs](#grouping-constructs)
    - [Bracket Expressions](#bracket-expressions)
    - [Character Classes](#character-classes)
    - [The OR Operator](#the-or-operator)
    - [Flags](#flags)
    - [Character Escapes](#character-escapes)
  - [Author](#author)

## Regex Components

### Anchors

The characters `^` and `$` are both considered to be anchors. An anchor symbolized as `^` (beginning anchor) signifies a string that starts with characters following it, and an anchor symbolized as `$` (closing anchor) signifies a string that ends with the characters that precede it. For examples:

    in$  -->  ending with 'in'
    ^testing 123$ -->  Matches only one pattern
    ^[0-9]+$ --> Numeric string

`\b` and `\B` are also considered as position anchors. `\b` matches the boundary of a word, and `\B` matches the non-word-boundary. For example:

    \dog\b --> matches the word "dog" in the input string "It is a dog.", but does not match the input "It is a dogie."

### Quantifiers

Quantifiers set the limits of the string that your regex matches. Let's have a look at the subexpression `.([a-z\.]{2,6})` as shown in the Summary section. The `{2,6}` part is a quantifier which limits the minimum and maximum number of characters that your regex is looking for. It means this part of the string must be between 2 and 6 characters in length. By default, a quantifier tells the engine to match as many occurrences of particular patterns as possible. This behavior is called greedy. The quantifiers include:

    +,*,? and {n}
    
Note: `{}`—Curly brackets can provide three different ways to set limits for a match: `{n}`, `{n,}` and `{n,m}`. There must be no space after the comma in {n,m}, otherwise it will not match correctly.

### Grouping Constructs

As regular expressions grow more complicated, it's important to use grouping constructs to partition regex using () in order to match only a portion of the string at a time. In our case, the regex is divided by three sections: `([a-z0-9_\.-]+)`, `([\da-z\.-]+)`, and `([a-z\.]{2,6})`. Each portion is also called as a subexpression.

### Bracket Expressions

A bracket expression represents a list of characters enclosed by `[]`. Let's take the first bracket expression, `[a-z0-9_\.-]`, in our case as an example. Instead of listing all characters, we use a range expression inside the bracket. `a-z` defines a range of characters specifically lowercase letters from "a" through to "z", and `0-9` defines a range of numbers from "0" through to "9". Likewise, if inside the brackets, there is `a-d`, it's the same as `[abcd]`. That would include "a", "b", "c" or "d".

### Character Classes

A character class defines a set of characters, any of which can appear in the input string for a successful match. Consider a practical task - we have a phone number such as `+1(911)-123-4567` and we need to convert it to a plain number: `19111234567`. To do this, we can find and delete everything that is not a number. Character classes can help with this. The most common character classes are as follows:

    \d ("d" comes from "digit") -----> Numbers: Characters from 0 to 9.
    \D  -----> Non-digit characters.
    \s ("s" comes from "space") ----->Space symbols: include spaces, tabs \t, newline \n and other rare characters such as \v, \f and \r.
    \S - except \s.
    \w ("w" comes from "word") ----->"Latin letters or numbers or underscore '_'. Non-Latin letters (such as Cyrillic or Hindi) do not belong to \w.
    \W -----> except \w.
    . -----> any character with the flag 's', otherwise any character except a newline \n.

Let's explore the "Number" class. Without the flag `g`, the regular expression looks only for the first match, which is the first digit \d. Let's add the flag g to find all numbers:

    let str = "+1(911)-123-4567";
    let regexp = /\d/g;
    alert( str.match(regexp) ); // array of matches: 1,9,1,1,1,2,3,4,5,6,7
    // let's make the digits-only phone number
    alert( str.match(regexp).join('') ); // 19111234567


### The OR Operator

| represents the OR operator. For example, we need to find a programming language: HTML, PHP, Java or JavaScript.

    let reg = /html|php|css|java(script)?/gi;
    let str = "First HTML appeared, then CSS, then JavaScript";
    alert( str.match(reg) ); // 'HTML', 'CSS', 'JavaScript'

### Flags

Also known as modifiers, the flags in regular expressions are used to specify additional matching strategies. Flags are not written in the regular expression, but outside of the expression, with a format as follows:

    /pattern/flags

In JavaScript, there are 6 optional flags, but the most common are below:

    g — Global search. Look back the phone number example above, I used 'g' to find all matches
    i — Case-insensitive search, see the example below
    m — Multi-line search, see the example below

Example 1. Find `LOVE` in a string:

    let str = "I love JavaScript!";
    alert( str.search(/LOVE/) ); // -1（not found, because it's case sensitive by default）
    alert( str.search(/LOVE/i) ); // 2

Example 2. Find `door` in a string:

    var str="doorgoogle\nyahoo\ndoorbing";
    var n1=str.match(/^door/g);   // one match
    var n2=str.match(/^door/gm); //multi-line matches

### Character Escapes

The backslash (\) in a regex escapes a character that otherwise would be interpreted literally. To use a special character as a regular character, just precede it with a backslash. For example, we need to find a dot `.`. A dot in a regular expression refers to "any character except a newline", so if we want to actually express a query for a "dot", we can add a backslash before the dot.

    alert( "Chapter 5.1".match(/\d\.\d/) ); // 5.1

## Author

This Regular Expressions (RegEx) Tutorial is created by [Baofeng Guo](https://github.com/magickw). Click [here](https://github.com/magickw/RegExTutorial) for repo.
