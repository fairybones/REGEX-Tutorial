# Regular Expression Tutorial & Study Guide
This tutorial introduces regular expressions with a email-validating example deconstructed under #regex-components, then explores these components in detail with syntactical and real world examples.

## Summary

The following regular expression validates that an email contains

## Table of Contents

- [Regex Components](#regex-components)
- [Anchors](#anchors)
- [Bracket Expressions](#bracket-expressions)
- [Boundaries](#boundaries)
- [Quantifiers](#quantifiers)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Grouping and Capturing](#grouping-and-capturing)
- [Back-references](#back-references)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`
Where `/ /` means the expression should be interpreted literally
`^` = anchor matches the start position
`()` = first capturing group
`[]` = bracket expression holds what we want to match
`a-z` = range of letters allowed (case-sensitive)
`0-9` = specifies allowed range of numbers
`_\.-` = characters allowed
`+` = quantifier used to match pattern 1 or more times
~ end first capturing group ~
`@` = must include literal text
`()` = second capturing group
`[]` = bracket expression holds pattern two
`\d` = character class used to match any digit 0-9
`a-z` = range of letters allowed (case-sensitive)
`\.-` = characters allowed
`+` = quantifier used to match pattern 1 or more times
~ end second capturing group ~
`.` = must include literal text
`()` = third capturing group
`[]` = bracket expression holds what we want to match
`a-z` = range of letters allowed (case-sensitive)
`\.` = characters allowed
`{2,6}` = quantifier specifying that the previous expression can match 2-6 times
~ end third capturing group ~
`$` = anchor matches the end position of a line or string

### Anchors
To validate that a string strictly follows a pattern, we use anchors to control where & how the pattern must occur. To check that the start or end of the string matches, use the character `^` or `$` respectively. We can also search for whole words or all occurances of the word by using word boundaries `\b` to represent the position between word/non-word character and `\B` which matches a non-word boundary.
Example: `\bword\b` will match all "word" but not "sword" or "password". 

### Bracket Expressions
The pattern or specifications for matching in a regex are in `[bracket expressions]` and are used to specify a choice among multiple characters, allowing for flexible and efficient pattern definitions & matching. There are two main types:
- Positive character group: brackets outline the characters we want to include
- Negative character group: by adding `[^ ]` to the start, negate characters we do NOT want to include

### Boundaries
To specify the exact positions where matches should occur, boundaries allow us to match position rather than specific characters. For example, we can match word boundaries with `\b` or inversely, `\B`
- line boundaries, where `^` indicate the start of a line or string, `$` indicates the end
- string boundaries, where `\A` can be used to specify the start of a line or string, `\z` for the absolute end, and `\Z` specifies the end of a string before a new line begins

### Quantifiers
To specify the extent of pattern matching, quantifiers are used to set limits on the number of times the regex should match. By default, quantifiers are designed to match as many occurences of the regex pattern or a section of particular pattern as possible, making quantifiers inherently greedy. To match the least amount while still satisfying the pattern, we use non-greedy versions of the standard(greedy) quantifiers. These counterparts are called lazy quantifiers.

### Greedy and Lazy Match
- Greedy quantifiers include: `*` - matches 0 or more times, `+` - matches 1 or more times, `?` - matches 0 or 1 time,
`{n}` - matches exactly n times, `{n, }` - matches at least n times, `{n,m}` - matches between n and m times

- Lazy quantifiers include: `*?` - 0 or more times ~ as few as possible, `+?` - 1 or more times ~ as few as possible, `??` - 0 or 1 time ~ as few as possible, `{n,}?` - at least n times ~ as few as possible, `{n,m}?` - matches between n and m times ~ as few as possible

### Grouping and Capturing
As the complexity of regular expressions increases, we can divide parts into subexpressions to check that different sections fulfill specific requirements. By default, each subexpression will only accept an exact match. Grouping constructs can be described as capturing, indicated by parentheses (), or non-capturing (?:). Capturing means that the matched string will be saved in memory in the results array, and will be stored with a backreference. Non-capturing can be more efficient and optimal if saving the matched substring is not necessary.

### Back-references
To reference the match of an existant capturing group, we can use `\N` where N is the integer representing a backreference

### OR Operator
Sometimes logic is needed outside of a bracket expression, especially with subexpressions and grouping constructs. The symbol `|` signifies an OR operator that combine & simplify regex. For example, 
- matching fruits can be as simple as `apples|oranges` 
- `|` can be used in complex conditions where parts of text may vary, such as `cat(s|)` will match cats or cat
- handles matching variations of a word or phrase, for example matching gray & grey with `gr(a|e)y`
- can be used with other regex components like anchors, quantifiers, and word/digit boundaries
- i.e. matching a digit or word with `\d|\w`

### Character Classes
Offer a practical and efficient way to match & define character sets, enhancing functionality and simplifying the regex, which can reduce errors

Basic Character Classes:
- Negation: matches any character NOT in the bracket expression when ^ is first
- Range: matches within specified range, indicated with a hyphen
- Simple: matches any 1
- Escapes: a backslash, `\` exempts a character that would otherwise be interpreted literally 

Predefined Character Classes:
- `\d` matches any digit : `[0-9]`
- `\D` matches any non-digit : `[^0-9]`
-`\w` matches any word (alphanumeric & underscore) : `[a-zA-Z0-9_]`
- `\W` matches any non-word : `[^a-zA-Z0-9_]`
- `\s` matches any whitespace character including spaces, tabs & linebreaks : `[\t\r\n\f\v]`
- `\S` matches any non-whitespace : `[^\t\r\n\f\v]`

### Flags
A way to define additional functionality or limitations outside of the \regex literal\, after the second slash. There are 6 different types:
- Global search, `g` will use regex to evaluate all possible matches in a string
- Case-Insensitive search, `i` will ignore capitalization while searching the string
- Multi-line search, `m` allows lengthy inputs to be treated as multiple lines
- Verbose search, `x` allows for whitespaces within the pattern for better readability
- Dot-all, `s` uses (.) to match new lines
- Unicode search, `u` enables emoji/unicode matching

### Look-ahead and Look-behind
To specify conditions about what precedes or follows the current position in the string to determine if a match is possible, we use lookaround assertations that can be positive `(?=pattern)` or negative `(?!pattern)`. A positive lookaround will attempt to match what follows/precedes the current position in the string IF it matches the pattern inside of the lookaround, while a negative lookaround will assert that what follows/precedes the current position can NOT match the pattern inside of the lookaround.
- Lookahead asserts content to the right of specified position (follows)
- Lookbehind asserts content to the left of specified position (precedes)

## Author
Annie Schalnat, https://github.com/fairybones