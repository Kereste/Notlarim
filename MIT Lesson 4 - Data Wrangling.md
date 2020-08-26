<h2>Lecture 4: Data Wrangling</h2>
**Source:** https://missing.csail.mit.edu/2020/data-wrangling/

**grep**
grep is a command-line utility for searching plain-text data sets for lines that match a regular expression.
It is one of the most useful commands on Linux and Unix-like system.

**sed(Stream EDitor)**
sed is a Unix utility that parses and transforms text, using a simple, compact programming language.
It can perform lot’s of function on file like, searching, find and replace, insertion or deletion.

**Regex(REgular EXpressions)**<br>
todo-RegexTutorialFromSource: https://regexone.com/

    . means “any single character” except newline
    * zero or more of the preceding match
    + one or more of the preceding match
    [abc] any one character of a, b, and c
    (RX1|RX2) either something that matches RX1 or RX2
    ^ the start of the line
    $ the end of the line

if you use ^ and $ together, then we say it has to match complete line.

**wc(Word Count)**
    Counts the number of words in the file.
    -l gives the line count.

**uniq**
    Gets the sorted data and only prints them once.
    -c = counts the number of duplicates and prints them with unique words.

**sort**
    Sorts unique data. Default is alphabetical.
Example:
example and it's regex is too big, so it's not showed here. You can see it in the source.
``` shell script
example regex | sort | uniq -c | sort -nk1,1 | tail -n10
```
This does the regex, sorts it alphabetically, then finds duplicates, counts them and sorts them again, then gives the last 10 lines.

sort -nk1,1
n means numeric sort.
k1,1 means on the first column of the input.
k lets you select a white space seperated column from the input to sort by.
1,1 is for starting and stopping at the first column.

After all of this, the example data looks like this:
```
1115 123
1141 ftpuser
1415 oracle
1444 postgres
1561 ubuntu
1951 user
3326 admin
3345 test
3782 123456
10892 root
```

After this, we can further develop our script to shape the data more:
``` shell script
example regex | sort | uniq -c | sort -nk1,1 | tail -n10 | awk '{print $2}' | paste -s,
```

**paste**
    takes a bunch of lines and pastes them together into a single line.
    I dont get what the -s used for.

**awk**<br>
    This is a column based stream processor. It deserves attention because it is a powerful language for this type of data wrangling
    awk by default, will parse its input in whitespace seperated columns and then you operate on those columns seperately.
    In the example below, we are saying print the second column.

An odd example with awk:
example regex | sort | uniq -c | awk '$1 == 1 && $2 ~ /^c.*e$/ {print $0}'
This only gives unique results that starts with c, ends with e only.
Result:
```
1 cachestore
1 calmejane
1 camise
1 cande
1 candyce
... vs vs
```

**bc (Basic Calculator)**
Example:
``` shell script
echo "1 + 2" | bc -l
```
Result is: 3

**gnuplot**
    For visiualising data, you can use gnuplot. Commands look like not too complex and you can easily output your data as histogram, etc.

**xargs**
    Takes lines of input and turns them into arguments.

**ffmpeg**
    This is for encoding and decoding video, and to some extent, images.
    A detailed explanation of it is in the source video, around minute 47.

**gzip**
    Compresses files.
