## REGEX

What is Regex: Regular expressions are a way to search for patterns within data sets.
Regex is NOT a programming language.

Almost all Regex engines are POSIX (Portable Operating System Interface) standards compliant.

### Steps to build Regex
1- Understand the requirement. What to include, what to exclude?

2- Identify patterns as an inclusions list or an exclusions list

3- Represent patterns with Regex

4- Use a regex engine (Grep, JS, Java, etc..) to apply regex pattern on the input

### Regex: The Basic Set
- \* -> Zero or more occurences of the character that precedes this asterisk
a* -> Zero or more occurences of 'a' (The character just preceding the asterisk)
Example: fooa*bar -> selects foo that is followed by the character a or no character -> foobar, fooabar, fooaaaaaa..bar etc..
Linux terminal command: grep 'fooa*bar' regex01.txt (Executes Regex search 'fooa*bar' in regex01.txt file)

- . -> A wildcard that represents any character
foo.bar All foo that are followed by any 1 character (fooxbar, foowbar etc)
foo..bar All foo that are followed by any 2 characters (fooxdbar, foowhbar etc)
grep 'fooa.bar' regex02.txt

- .\* -> Zero or more occurences of wildcard, which means zero or more occurences of any character
foo.*bar All foo that are followed by any character or no character(foobar, fooxbar, fooqbar etc)
grep 'foo.*bar' regex03.txt

- \s -> Represents whitespace
foo\s*bar All foo that are followed by whitespace or no character(foobar, foo bar, foo  bar etc)
grep 'foo\s*bar' regex04.txt

- [pqr] -> A single character which can be either p,q or r
[fcl]oo Finds all foo, coo, loo
grep '[fcl]oo' regex05.txt

- [a-d] -> A single character that falls in the range of a,b,c,d
- [^pq] -> A single character that is neither p nor q
- ^pattern -> ^ is an anchor tag that represents the beginning of the line
- pattern$ -> $ is an anchor tag that represents the end of the line