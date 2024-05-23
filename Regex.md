# Regex

## *Character Classes*


| Metacharacter | Description                  |
|---------------|------------------------------|
| .             | any character except newline |
| \w \d \s      | word, digit, whitespace      |
| \W \D \S      | Not word, digit, whitespace  |
| [abc]         | any of a,b or c              |
| [^abc]        | not any of a, b or c         |
| [a-z]         | range between a to z         |

| Anchors | Description                      |
|---------|----------------------------------|
| ^abc$   | start/end of string              |
| /b /B   | word boundary, not word boundary |


| Escaped Characters | Description                       |
|--------------------|-----------------------------------|
| \. \*  \\          | escaped special characters        |
| \t  \n  \r         | tab, new line and carriage return |


| Groups & Lookaround | Description               |
|---------------------|---------------------------|
| (abc)               | capture group             |
| \1                  | backreference to group #1 |
| (?:abc)             | non-capturing group       |
| (?=abc)             | positive lookahead        |
| (?!abc)             | negative lookahead        |

| Quantifiers & Alternation | Description                  |
|---------------------------|------------------------------|
| a* a+ a?                  | 0 or more, 1 or more, 0 or 1 |
| a{5} a{2,}                | exactly 5, 2 or more         |
| a{1,3}                    | between 1 and 3              |
| a+? a{2,}?                | match as few as possible     |
| ab│cd                     | match ab or cd               |

## Examples

### *Email*

An email address is composed of the following:

(name) @ (domain) . (extension) (.optional extension)
   1        2           3                  4
   
1. any letters, numbers, dots and/or hyphens
2. any letters, numbers and/or hyphens
3. any letters
4. a (dot) and then any letters

`Regex: ^([a-z\d\-._]+)@{1}([a-z\d\-.]+)(\.[a-z]{2,3})(\.[a-z]{2,3})?$
`
```
^$              - Start and end of a string
()              - A Groups
[a-z\d\-.]      - The range of letters from a to z, digits, a hyphen and a dots
+               - One or more of these Characters
```

```
@               - The literal '@' Character
{1}             - Only one occurences
```

```
[a-z\d\-.]      - Same as above
+               - Same as above
```

```
\.[a-z]{2,3}    - 2 to 3 occurences of a to z with a dot leading

(\.[a-z]{2,3})? = Optional extension with same meaning as above
```

[Index](index.md)
