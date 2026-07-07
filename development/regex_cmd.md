# Regular Expressions

## Any Character Except New Line
```bash
\d      - Digit (0-9)
\D      - Not a Digit (0-9)
\w      - Word Character (a-z, A-Z, 0-9, _)
\W      - Not a Word Character
\s      - Whitespace (space, tab, newline)
\S      - Not Whitespace (space, tab, newline)

\b      - Word Boundary
\B      - Not a Word Boundary
^       - Beginning of a String
$       - End of a String

[]      - Matches Characters in brackets
[^ ]    - Matches Characters NOT in brackets
|       - Either Or
( )     - Group

Quantifiers:
*       - 0 or More
+       - 1 or More
?       - 0 or One
{3}     - Exact Number
{3,4}   - Range of Numbers (Minimum, Maximum)
```

## Example of Regular Expressions
```bash
1. [a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+   # mathch E-mail addresses
2. M(r|s|rs)                                        # find groups of regx e.g. Mr or Ms or Mrs
3. [\(\)\<\>\[\]\{\}]+                              # find parentheses
4. [\[\(\<\{]\s*\b\d*\w*\b\s*[\]\)\>\}]             # find parentheses including content
5. \b\d+\b                                          # find all digits
6. \b(?=\w*)-\s)|(\s-(?=\w)\b                       # remove hyphens at the beginning and at the end of a word. 
                                                    # https://www.youtube.com/watch?v=DeIWR4gv1-8&# list=TLPQMDQwNDIwMjBbHMctH4n7yw&index=2
7. .*?                                              # match any character (except line terminators)
8. #.*                                              # find every comment in a python script
9. ^((?!#.*).)*$                                    # Invert the expression (finds everything that is not 
a comment)
```

## Videos
* [How to Match Any Pattern of Text](https://www.youtube.com/watch?v=sa-TUpSx1JA)
* [Python based](https://www.youtube.com/watch?v=K8L6KVGG-7o)