---
title: Regex
tags: [Notebooks/JS]
---

# Regex
Notes from the Regex tutorial on [FreeCodeCamp](https://www.freecodecamp.org/)
## Basic Syntax
 - Regular Expressions (Regex) are patterns used that you use to match with strings
 - All regular expressions in JS are wrapped in `/ /`
    - Use the `.test()` method of regular expressions to see if a string matches a regex
```js
const myRegex = /abc/;
console.log(myRegex.test('abcdef')); // true
```
## OR Operator
 - To search for different possible string, use the `|` symbol
```js
const validResponse = /yes|no/;
const r1 = validResponse.test("    yes"); // true
const r2 = validResponse.test("no");      // true
```
## Extracting Matches
 - *Strings* have a method called `.match()` that extracts any matching patterns in a string
    - To match multiple values in a string, the regex needs to end with a `g`
    - Otherwise, you only extract the first match
```js
const matchList = "hello".match(/l/g); // ['l', 'l`]
```
## Flags
 - Flags are added to the end of a regex like so:
```js
/<my regex>/<my flags>;
```
 - **Flags**
   - **`i`** ignore the case of matches
   - **`g`** match with multiple values in the string, not just the first
## Special Characters
 - **`.`** can match any character
## Character Classes
 - Allow you to define a group of possible characters
    - You specify options in `[]`
       - Can list out each possible character explicitly
       - Can also specify character ranges (e.g., a-z, 0-4, or A-Z)
       - Can also specify multiple character ranges in a single character class
```js
const matchAlphanumeric = /[a-zA-Z0-9]/;
const vowelRegex = /[aeiou]/ig;
```
 - Negated Character Sets
    - Use a `^` to specify all characters that **shouldn't** be matched
```js
const noVowels = /[^aeiou]/ig;
```
## Shorthand Character Classes
 - **`\w`** Match Alphanumerics
    - Same as `[A-Za-z0-9_]`
    - Note that the `_` is included as a character here
 - **`\W`** Match Non-Alphanumerics
    - Same as `[^A-Za-z0-9_]`
 - **`\d`** Match Digits
    - Same as `[0-9]`
 - **`\D`** Match Non-Digits
    - Same as `[^0-9]`
 - **`\s`** Match Space Characters
    - Same as `[ \r\t\f\n\v]`
 - **`\S`** Match Non-Digits
    - Same as `[^ \r\t\f\n\v]`
## Matching Repeating Patterns
 - `+` Match a pattern that occurs 1 or more times
 - `*` Match a pattern that occurs 0 or more times
```js
const anyNumberOfAs = /a+/g;
const a = 'abc'.match(anyNumberOfAs);
const aa = 'aabc'.match(anyNumberOfAs);
```
### Lazy Matching
 - Typically, Regex finds the largest possible string that matches a pattern when it sees a `*`
    - AKA *greedy matching*
 - Use a `?` to match the smallest possible string that follows a pattern
    - AKA *lazy matching*
```js
const str = "racer in his racecar";
const bigMatch   = str.match(/r.*r/);   // ["racer in his racecar"]
const smallMatch = str.match(/r.*?r/);  // ["racer"]
```
## Endpoint String Searching
 - `^` represents the start of the string
 - `$` represents the end of the string
```js
const properGreetingRegex = /^hello.*goodbye$/i;
const isAMatch   = "Hello asljdfjlasd goodbye".match(properGreetingRegex);
const isntAMatch = "goodbye hello goodbye".match(properGreetingRegex);
```
## Quantity Specifiers
 - To specify how many instances of a pattern you would like, use `{lower, upper)}`
    - `lower` is the lowest allowable number of instances and `upper` is the highest
    - If you don't specify `upper`
        - If you do `{lower,}`, there will be no cap on the number of instances
        - If you do `{n}`, you can only have `n` instances
```js
const twoToThreeAs = /a{2,3}h/;
twoToThreeAs.test("aaah");  // True
twoToThreeAs.test("aaaah"); // False

const moreThanThreeAs = /a{3,}h/;
moreThanThreeAs.test("aaaaaaaaaaah"); // True
moreThanThreeAs.test("ah");           // False

const onlyThreeAs = /a{3}h/;
onlyThreeAs.test("aaah"); // True
onlyThreeAs.test("aah");  // False
```
## Optional Elements
 - A `?` is used after a pattern to specify whether it is optional
```js
 // Matches 'favorite' or 'favourite'
const englishAndBritishSpelling = /favou?rite/;
```
## Lookaheads
 - Used to see if a pattern is contained further on in a string without matching with it
 - `(?=...)` Positive Lookahead
    - Ensures that a string **does** contain the pattern later on
 - `(?!...)` Negative Lookahead
    - Ensures that a string **doesn't** contain the pattern later on
```js
const qWithU   = /q(?=u)/;
const qWithNoU = /q(?!u)/;
"quiz".match(qWithU);   // ['q']
"qink".match(qWithNoU); // ['q']
```
 - Checking 2 competing conditions with lookaheads
```js
// A valid password must have > 6 characters and 2 consecutive digits
const pwRegex = /(?=\w{5,})(?=\D*\d{2})/;
/* Note that in order for these two lookaheads to work, the RegEx engine must find
 * SPECIFIC point where there are both 6 characters ahead AND 2 consecutive digits ahead.
 * If we think of the string 'abcd12', note that the point at which we start counting the six   
 * characters is different from where we have to start counting the consecutive numbers. Thus, in 
 * order to start counting from the same location, we have to include an optional set of non
 * digits in our second lookahead (\D*) so that there is a specific point in the string at which
 * both lookahead patterns are found
 */
```
 - A great explanation of the above code can be found [here](https://www.freecodecamp.org/forum/t/positive-and-negative-lookahead-consecutive-numbers/223138/4)
## Capture Groups
 - Use `()` to search for repeating substrings rather than matching for characters individually
    - When referring to a specific capture group, we use `\1` to refer to the first group, `\2` to refer to the second, etc.
```js
// Match a number that is repeated exactly 3 times with a space in between
const numberRegex = /^(\d+) \1 \1$/;
numberRegex.test("1000 1000 1000"); // true
numberRegex.test("1 1 1");          // true
numberRegex.test("1000 1000 1111"); // false
```
 - If a capture group is found, `.match()` will return a list with both the matched string followed by the capture groups 
```js
let repeatRegex = /(\w+)\s\1/;
"zach zach".match(repeatRegex); // Returns ["zach zach", "zach"]
```
## Search And Replace
 - `.replace()` is a string method used to replace a matched regex string with a new value
    - Capture groups from the regex can be referred to using `$1`, `$2`, ...
```js
// Find a name in the form "First Last"
const nameRegex = /([A-Z][a-z]+) ([A-Z][a-z]+))/;

const correctNameFormat = "Zach Breit".replace(nameRegex, '$2, $1'); // "Breit, Zach"
```
