# Regex tutorial

This Regex tutorial will help you better understand the sequence of special characters to verify a search term. this allows you to located specific search patterns of characters in a string when inculded in code or search algorithms. They can also be used to validate input data. 

## Summary

The following code will give examples for how Regex can be used. The code will be used to find the IP address in a string. The regular expression below will find an IPv4 address at the beginning of, at the end of, or within a string.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

Patterns must be wrapped in slashes ("/") because JavaScript likes to treat Regex as a literal. To be able to use JavaScript's .matchAll() method we must use the flag "g" at the end. This will allow us to find all IP addresses in the string, not just the first one.

/^(?:(?:25[0-5]|2[0-4]\d|[01]?\d?\d)\.){3}(?:25[0-5]|2[0-4]\d|[01]?\d?\d)$/g;

### Anchors
The start/end of the string and the boundaries between words are the two anchors for regexes. For this specific regex, we do not need either beccause we want to find the pattern no matter the position in the string.

If you have a log and have already split it into an array at each line break and wish to find only IP addresses that are located in the beginning of the string, you can place a ^ at the beginning of the code.

/^(?:(?:25[0-5]|2[0-4]\d|[01]?\d?\d{1})\.){3}(?:25[0-5]|2[0-4]\d|[01]?\d?\d{1})/, "g"

If you wish placeing a \b at the beginning and the end of the code will allow you to find only IP addresses that are separated by whitespace.

/\b(?:(?:25[0-5]|2[0-4]\d|[01]?\d?\d{1})\.){3}(?:25[0-5]|2[0-4]\d|[01]?\d?\d{1})\b/, "g"

### Quantifiers

Qualifiers tell the regex how many times to find a subexpression. This specific regex uses two quantifiers: {1} and {3}. The {1} is used to find exactly one instance of a digit (0-9) so there is at least one digit found in the subexpression. The {3} is used to find exactly three instances of numbers followed by a period. The regex also uses the "lazy" quantifier ? a few times. The lazy quantifier matches as few instances as possible, in our case 0 or 1 instance of a digit (number from 0 to 9).

### Grouping Constructs

Regular expressions allow you to find subexpressions within a string. In our case, we want to find two subexpressions: three sets of numbers followed by a period, and one set of numbers not followed by a period. We can achieve this by using grouping constructs. In this example, we are using non-capturing groups because our regex is not particularly complex. We use the "(?:" syntax to create a group, and then apply quantifiers to match multiple occurrences of that subexpression. We have two groups in our regex: the first group contains another grouping of subexpressions, which is used to find instances of numbers followed by a period; the second group contains a single subexpression that finds a single instance of numbers not followed by a period.

### Bracket Expressions

Bracket expressions in regular expressions begin with the "[" character and end with the "]" character. They define a set of characters that can be matched by the expression. The set can include individual characters or a range of characters specified by a hyphen. For example, [A-Z] matches any uppercase letter, and [0-9] matches any digit. In our case, we are using bracket expressions to find the digits of numbers that are in the range 0 to 255. However, we cannot simply use [0-255] because this would match any character that is either 0, 1, 2, 5, or a hyphen. Instead, we need to check each digit individually using the appropriate range, like [0-9] for the first digit and [0-5][0-9] for the second and third digits.

### Character Classes

In addition to bracket expressions, regular expressions in our example are using the shorthand character class for digits, \d, which is equivalent to [0-9]. We use it multiple times to check the digits of the numbers that we are trying to match. However, in some cases, we use [0-n] instead of \d, where n is the upper bound of the digits we want to match.

Finally, we use the | operator to specify alternatives in our regex. It allows us to match one of several possible patterns in a single regular expression. In our example, we use the | operator to specify three alternatives for the first set of numbers in the IP address: either "25" followed by a number between 0 and 5, "2" followed by any two digits, or "1" or "0" followed by any two digits. By using the | operator, we can match any one of these alternatives and still get a successful match.

### The OR Operator

In our regex pattern, we need to check whether a number is between 0 and 255, but since we can only check one digit at a time, we use the OR operator, represented by the | character. The OR operator works similarly to the OR logical operation in JavaScript. In this tutorial, we are looking for three possibilities: numbers that begin with "25" and end with any digit (\d); numbers that begin with "2" and have any two digits (\d\d); and numbers that begin with 0 or 1 ([01]) and have any two digits (\d\d). We use the subexpression 25[0-5] to find numbers from 250 to 255, 2[0-4]\d to find numbers from 200 to 249, and [01]?\d\d to find numbers from 0/000 to 199. Since we need to match only one of these possibilities, we use the OR operator to combine them into a single regex pattern.

### Flags

When using regular expressions in JavaScript, you can use the /g flag to perform a global search. This flag will keep track of the index of the last match, allowing subsequent searches to start looking after the previous match. The /g flag is particularly useful when using JavaScript's .matchAll() method to find all instances of the regex pattern in a string.

### Character Escapes

Regular expressions can search for characters that are used as operators in the regex syntax, such as brackets, slashes, and periods. In our particular regex, we are using a one-character escape sequence, "\.", to search for the period at the end of each number that makes up an IP address.

## Author

This ttutorial was created by Frank Sabogal

Github : franksabogal04
