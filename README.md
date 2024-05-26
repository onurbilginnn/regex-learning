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
- \* -> Zero or more occurences of the character that precedes this asterisk <br>
a* -> Zero or more occurences of 'a' (The character just preceding the asterisk) <br>
Example: fooa*bar -> selects foo that is followed by the character a or no character -> foobar, fooabar, fooaaaaaa..bar etc.. <br>
Linux terminal command: grep 'fooa*bar' ./module1/regex01.txt (Executes Regex search 'fooa*bar' in regex01.txt file)

- . -> A wildcard that represents any character<br>
foo.bar -> All foo that are followed by any 1 character (fooxbar, foowbar etc)<br>
foo..bar -> All foo that are followed by any 2 characters (fooxdbar, foowhbar etc)<br>
grep 'fooa.bar' ./module1/regex02.txt

- .\* -> Zero or more occurences of wildcard, which means zero or more occurences of any character<br>
foo.*bar -> All foo that are followed by any character or no character(foobar, fooxbar, fooqbar etc)<br>
grep 'foo.*bar' ./module1/regex03.txt

- \s -> Represents whitespace<br>
foo\s*bar -> All foo that are followed by whitespace or no character(foobar, foo bar, foo  bar etc)<br>
grep 'foo\s*bar' ./module1/regex04.txt

- [pqr] -> A single character which can be either p,q or r<br>
[fcl]oo -> Finds all foo, coo, loo<br>
grep '[fcl]oo' regex05.txt <br>
grep '[fcdplb]oo' ./module1/regex06.txt

- [^pq] -> Excludes p or q<br>
[^mh]oo -> Excludes moo and hoo that are begining with m or h <br>
grep '[^mh]oo' ./module1/regex06.txt 

- [a-d] -> A single character that falls in the range of a,b,c,d <br>
[j-m]oo -> Finds all joo, koo, loo, moo from character j to m all characters are included <br>
grep '[j-m]oo' ./module1/regex07.txt <br>

- [a-cx] -> One of the characters falling in the range OR any of the other coices given in square brackets (a,b,c,x) <br>
[j-mz]oo -> Finds all joo, koo, loo, moo and zoo from character j to m and z all characters are included <br>
grep '[j-mz]oo' ./module1/regex07.txt

- [a-cA-Cx] One of the characters falling in one of the ranges OR any of the other coices given in square brackets (a,b,c,A,B,C,x) <br>
[j-mJ-Mz]oo -> Finds all joo, koo, loo, moo, Joo, Koo, Loo, Moo, zoo from character j to m and J to M and z all characters included <br>
grep '[j-mJ-Mz]oo' ./module1/regex08.txt

- x*\\.y* Zero or more occurences of x with following .(dot) following Zero or more occurences of y (xxx.yyy or x.y or .y etc) <br>
Following characters should be escaped with a backlash as these characters have special meaning otherwise: ^$*.[()\ <br>
grep 'x*\\.y*' ./module1/regex09.txt

- ^pattern -> ^ is an anchor tag that represents the beginning of the line<br>
- pattern$ -> $ is an anchor tag that represents the end of the line<br>