# Regular Expressions

To create a regular expression you use 2 ways

```js
let regex1 = /abc/;
let regex2 = new RegExp("abc");
```

| Literal            | abc123              | LiteralCharacter                                             |
| ------------------ | ------------------- | ------------------------------------------------------------ |
| Boolean or         | on\|off             | "on" or "off"                                                |
| Grouping           | o(?:n\|ff)          | "o" followed by "n" or "ff"                                  |
| Wildcard           | .                   | Any character                                                |
| Zero or one        | ?                   | Colou?r                                                      |
| Zero or more       | *                   | Mooo*n                                                       |
| One or more        | +                   | Moo+n                                                        |
| Exact Number       | {n}                 | Mo{2}n                                                       |
| min                | {min,}              | Mo{2,}n                                                      |
| max                | {,max}              | Mo{,2}n                                                      |
| Min max            | {min, max}          | Mo{2,5}n                                                     |
| Bracket expression | [abc]               | a\|b\|c                                                      |
| negation           | [^abc]              | Any character except a or b or c                             |
| Nth group          | (.)\1+              | Any character followed by the same character 1 or more times |
| Named groups       | (?<char>.)\k<char>+ |                                                              |
| Word character     | \w                  | [a-zA-Z0-9_]                                                 |
| Digit              | \d                  | [0-9]                                                        |
| Non word           | \W                  | [^a-zA-Z0-9_]                                                |
| non digit          | \D                  | [^0-9]                                                       |

---

#### test

```js
let regex = /mo{2,}n/
regex.test("moon") // => true
regex.test("mooooooooon") // => true
regex.test("mon")	//=> false
regex.test("moon landing")	//=> false
regex.test("the moon landing")	//=> true
```

#### Match

```js
let regex = /m(?<group>o{2,})n/  //=> Looks for only the first
let string = "We are going to the moon"
string.match(regex)
// > Array ["mooon", "ooo"]
// > index 20

let regex2 = /m(?<group>o{2,})n/g //=> checks the global all in the string`/g` 
string.match(regex2) //=> ["mooon"]
```



## Further Study

- exec function
- matchAll function
- replace function
- Assertions in regex
- Character classes
- Unicode property escapes