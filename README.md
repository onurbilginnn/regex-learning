> [!CAUTION]
> Please check raw text in order to see actual regex code !!!


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
- * -> Zero or more occurences of the character that precedes this asterisk <br>
a* -> Zero or more occurences of 'a' (The character just preceding the asterisk) <br>
Example: fooa*bar -> selects foo that is followed by the character a or no character -> foobar, fooabar, fooaaaaaa..bar etc.. <br>
Linux terminal command: grep 'fooa*bar' ./module1/regex01.txt (Executes Regex search 'fooa*bar' in regex01.txt file)

- . -> A wildcard that represents any character<br>
foo.bar -> All foo that are followed by any 1 character (fooxbar, foowbar etc)<br>
foo..bar -> All foo that are followed by any 2 characters (fooxdbar, foowhbar etc)<br>
grep 'fooa.bar' ./module1/regex02.txt

- .* -> Zero or more occurences of wildcard, which means zero or more occurences of any character<br>
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

- Following characters should be escaped with a backlash as these characters have special meaning otherwise: ^$*.[()\ <br>
x*\.y* -> Zero or more occurences of x with following .(period) following Zero or more occurences of y (xxx.yyy or x.y or .y etc) <br>
grep 'x*\.y*' ./module1/regex09.txt <br>
If a .(period) inside square brackets, it need NOT be escaped <br>
grep '[#:.]' ./module1/regex10.txt <br>
If any of the characters ^ or - appear inside square brackets, it needs to be escaped with a backslash as these 2 characters have special meaning inside square brackets <br>
grep '[\^#:]' ./module1/regex11.txt <br> 
The backslash it self should always be escaped with a backslash, irrespective of its position within the regex <br>
grep 'x[\^#\\]' ./module1/regex12.txt <br>
grep 'x*\\' ./module1/regex12.txt

#### Regex: The Basic Set: Anchors
- ^pattern -> ^ is a placeholder that signifies beginning of a line. The interpretation of ^ differs wihtin square brackets and outside of it. Inside square brackets, ^ stands for negation. Outside, it is a placeholder for beginning of line. <br>
^foo.* -> Returns only text that begins with foo the following character after foo could be anything <br>
grep '^foo.*' ./module1/regex13.txt

- pattern$ -> $ is an anchor tag that represents the end of the line<br>
.*foo$ -> Returns only text that ends with foo the preceeding character before foo could be anything <br>
grep '.*foo$' ./module1/regex13.txt

- ^pattern$ -> ^ is a placeholder that signifies beginning of a line; $ is a placeholder that signifies end of a line<br>
^foo$ -> Returns only foo text<br>
grep '^foo$' ./module1/regex14.txt

### Regex: The Extended Set

```diff
! grep -E '<regex>' <file_path> -> -E flag is required if you are using Regex extended set on terminal commands
```

- + -> One or more occurences of the character that precedes this + symbol <br>
fooa+bar -> One or more occurences of 'a' (The character just preceding the plus symbol, fooabar, fooaaaabar...) <br>
grep -E 'fooa+bar' ./module2/regex04.txt <br>
- ? -> Zero or 1 occurence of the character that precedes this question mark<br>
a? -> Zero or 1 occurence of a (The character just preceding the question mark)<br>
https?://website -> http://website or https://website accepted only. <br>
grep -E 'https?://website' ./module2/regex05.txt
- pat1|pat2 -> Matches either the pattern pat1 or the pattern pat2 <br>
(ply|log)wood ->  Accepted plywood or logwood<br>
grep -E '(ply|log)wood' ./module2/regex06.txt
- () -> Divides patterns into groups <br>
Parenthesis is used to group and treat as single entity <br>
(ha){4,} -> Select min 4 to max unlimited ha words <br>
(ha){1,2} -> Select min 1 to max 2 ha words <br>
grep -E '(ha){4,}' ./module2/regex03.txt <br>
grep -E '^(ha){1,2}$' ./module2/regex03.txt <br>
- {m} -> Exactly 'm' occurences of whatever precedes <br>
a{m} represents exactly m repetitions of a <br>
^[0-9][0-9][0-9]$ -> 3 digit numbers only <br>
Same expression of above line = ^[0-9]{3}$ -> 3 digit number only <br>
grep -E '^[0-9]{3}$' ./module2/regex01.txt
- {m,n} -> At least m and at most n occurences of whatever precedes. <br>
Only one of m, n is mandatory. Other can be left blank. <br>
^[a-z]{4,5}$ -> Fetches min 4 to max 5 english charactered texts <br>
 grep -E '^[a-z]{4,5}$' ./module2/regex02.txt 

 ### Regex: Group Capture, Find & Replace
 1- Understand the requirement. What to replace? What to put as replacement?

 2- Represent patterns using Regex. Enclose the patterns that needs to be replaced with parantheses to segregate them into capture groups.

 3- Come up with a substitution string by using captured pattern groups.

 4- Use a regex engine (Grep, JS, Java, etc..) to apply the replacement.

 5- Linux command structure: sed -r 's/pattern/replacement/g' inputfile

#### Monitor Resolutions
- ./module3/regex01.txt
- Group capture -> ([0-9]+)x([0-9]+) -> Gives 1280x720, 34242x534534, etc...
- Replace -> \1 pix by \2 pix -> Gives '1280 pix by 720 pix'
- sed -r 's/([0-9]+)x([0-9]+)/\1 pix by \2 pix/g' ./module3/regex01.txt

#### First Name & Last Name
- ./module3/regex02.txt
- Group capture -> ([a-zA-Z]+) ([a-zA-Z]+) -> Gives Ali Baba, Dayi reis, etc...
- Replace -> \2,\1
- 1st cmd: sed -r 's/([a-zA-Z]+)[[:space:]]([a-zA-Z]+)/\2,\1/g' ./module3/regex02.txt
- 2nd cmd: sed -r 's/([a-zA-Z]+) ([a-zA-Z]+)/\2,\1/g' ./module3/regex02.txt

#### The Clock Time
- ./module3/regex03.txt
- Group capture -> ([0-9]{1,2}):([0-9]{2}) -> Gives 2:59, 12:30, etc...
- Replace -> \2 mins past \1
- cmd: sed -r 's/([0-9]{1,2}):([0-9]{2})/\2 mins past \1/g' ./module3/regex03.txt

#### Phone Numbers
- ./module3/regex04.txt
- Group capture -> [0-9]{3}\.[0-9]{3}\.([0-9]{4}) -> Gives 123.523.6233, 853.251.5923, etc...
- Replace -> xxx.xxx.\1 -> As there is only on paranthesis pair() in group capture, we have only \1 group.
- cmd: sed -r 's/[0-9]{3}\.[0-9]{3}\.([0-9]{4})/xxx.xxx.\1/g' ./module3/regex04.txt

#### Date
- ./module3/regex05.txt
- Group capture -> ([a-zA-Z]{3}) ([0-9]{1,2})[a-z]{2} [0-9]{2}([0-9]{2}) -> Gives Jan 5th 1987, Mar 2nd 1923, etc...
- Replace -> \2-\1-\3 -> Take attention to the paranthesis and group usage
- cmd: sed -r 's/([a-zA-Z]{3}) ([0-9]{1,2})[a-z]{2} [0-9]{2}([0-9]{2})/\2-\1-\3/g' ./module3/regex05.txt

#### Phone Numbers - 2
- ./module3/regex06.txt
- Group capture -> \(([0-9]{3})\).([0-9]{3}).([0-9]{4}) -> Gives (692).217.7432, (556).342.7590, etc...
- Replace -> \1.\2.\3
- 1st cmd: sed -r 's/\(([0-9]{3})\).([0-9]{3}).([0-9]{4})/\1.\2.\3/g' ./module3/regex06.txt
- 2nd cmd: sed -r 's/\(([0-9]{3}))(\.[0-9]{3}\.[0-9]{3})/\1\2/g' ./module3/regex06.txt

#### Challenge
- ./challenge/regex01.txt
- Find -> ^[a-z0-9._\-]+@([a-z]+)\.([a-z]+) -> email regex lets English characters, numbers and [.-_] characters then @xxx.xxx
- grep -E '^[a-z0-9._\-]+@([a-z]+)\.([a-z]+)' ./challenge/regex01.txt
