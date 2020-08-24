<h1>-Bourne Again Shell (BASH)-</h1>
This is the notes I prepared from my lessons at MIT Missing Semester.

//todo: migrate your other notes to here too. Use this readme as index, etc.

<h2>Course overview + The Shell</h2>
Source is here: https://missing.csail.mit.edu/2020/course-shell/

**Environment Variables:**
They are some foundation variables that are set whenever you start your shell.

**Absolute(Full) Path:** 
They are the paths that fully determine the location of a file.
Relative Paths: These are relative to where you currently are.

**pwd(Print Working Directory)**

**cd(Change Directory)**<br>
	At route, "." means current directory. ".." means the parent directory. 

**ls**<br>
	Lists the files in the current directory. Also you can give it a route to list files at that spot.
	using "ls -l" is especially helpful. Still gives the list of files but shows more detail. 

**~**<br>
At route, tilde always expands to the home directory.

**programnamehere --help**
Most of the programs has this, if you --help it will helpfully print out bunch of info.<br>
Example:
```shell script
anil@anil-SATELLITE-L50-B:~$ ls --help
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      with -l, scale sizes by SIZE when printing them;
                               e.g., '--block-size=M'; see SIZE format below
  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                               modification of file status information);
                               with -l: show ctime and sort by name;
                               otherwise: sort by ctime, newest first
  -C                         list entries by columns
      --color[=WHEN]         colorize the output; WHEN can be 'always' (default
                               if omitted), 'auto', or 'never'; more info below

(list goes beyond this)
```
 The way to read that usage line is: <br>
 "..." means zero or one or more. <br>
 [] means optional.<br>

"-a, --all" these are flags. Anything that doesnt takes a value is flag.
"-C or --color[=WHEN]" is an option.

 <h3>Permissions & File Management</h3>
 
 ```shell script
 anil@anil-SATELLITE-L50-B:~$ ls -l
 total 20900
 -rwxr-xr-x  1 anil anil  1933813 May 11 11:14  composer.phar
 -rw-rw-r--  1 anil anil   277120 May 11 11:13  composer-setup.php
 drwxr-xr-x  7 anil anil     4096 Ağu 19 19:02  Desktop
 drwxr-xr-x  4 anil anil     4096 Ağu 20 14:46  Documents
 drwxr-xr-x  5 anil anil     4096 Ağu 19 15:45  Downloads
 -rw-rw-r--  1 anil anil 19120179 Haz  9 13:44 'İstatistik Ders Notları.pdf'
 drwxr-xr-x  2 anil anil     4096 May  8 00:47  Music
 drwxrwxr-x  5 anil anil     4096 Haz 25 19:19  myApp
 drwxrwxr-x  8 anil anil     4096 Ağu 20 15:26  PhpstormProjects
 drwxr-xr-x  4 anil anil    12288 Ağu 20 09:27  Pictures
 drwxr-xr-x  2 anil anil     4096 May  8 00:47  Public
 drwxrwxr-x  6 anil anil     4096 Haz 25 13:05  RiderProjects
 drwxr-xr-x 13 anil anil     4096 Haz 26 10:49  snap
 drwxr-xr-x  2 anil anil     4096 May  8 00:47  Templates
 drwxr-xr-x  2 anil anil     4096 May  8 00:47  Videos
 drwxrwxr-x  3 anil anil     4096 May 28 13:06  VS
```

We take one row from this an example:
``` shell script
 drwxr-xr-x  5 anil anil     4096 Ağu 19 15:45  Downloads
```
 Lets dissect this. If we seperate this into meaningful parts, it looks like this:<br>
 d * rwx * r-x * r-x 
 First character, d means this is a directory. I will address this as a file at this example this for simplicity<br>
 The first group, the rwx is the permissions for the owner of the file.
 The second group, the r-x is the permissions for the group that owns this file.
 The third group, the other r-x is the permissions for the everyone else.
 
 Lets dissect further. rwx means: Read Write Execute. Meanings of those differs a bit between files & directories.
 if the letter is missing, than that thing is unauthorized for the client.
 Read and Write is self explanatory.
 Execute: TODO: Write this later
 
 For directories: 
 Read: Are you allowed to see the contents of this directory?
 Write: Are you allowed to rename/create/remove files in this directory?
 Execute: Are you allowed to enter this directory?
 
 **mv**<br>
    It can rename and move a file.
 
 **cp**
     It can copy a file.
 
 **rm**
      For removing files. It's not recursive by default.
      
**rmdir**
    For removing directories. Only if its empty.
    
**mkdir**
    Creates a new directory.

**man**
    Shows us a manual page for the program.
    
**ctrl + l**
    Clears up the console and goes to the top.
    
**cat**<br>
    Prints the contents of a file.<br>
Example:
``` shell script
cat /etc/*-release
```
Seeing the operating system version & info   

**#**<br>
    Adding this to the beginning of the row means: "Run this as root."
``` shell script
anil@anil-SATELLITE-L50-B:/sys/class$
```
$ at there means I'm currently not running things as root.

**sudo su**
    Here, what su does is elevating you to the shell as a super user.

**tee**
    Takes its input and writes it output, but also to standard output.

<h3>Rewiring Console Input/Output</h3>
Shell gives us an ability to rewire input/output streams.
Most straightforward way to do this is using angle brackets
"< filename" means rewire the input of this program to be the contents of this file.
"> filename" means rewire the output of this program to be the contents of this file.<br>
Example:
``` shell script
echo hello > hello.txt
```
This prints the output of echo into the hello.txt file.

``` shell script
cat < hello.txt
```
In this instance, shell is going to open hello.txt, take its contents and set those to be the input of cat.
And then the cat is gonna print its output to the terminal.

Also, these can be used at the same time:
``` shell script
cat < hello.txt > hello2.txt
```
In here, I'm telling the cat program nothing at all. Do your normal thing. Cat program knows nothing about this redirection.
But we are telling the shell use hello.txt as an input for the cat, and to write anything cat prints to hello2.txt .


**>>**
    This is append, not overwrite. So if we do this:
``` shell script
cat < hello.txt >> hello2.txt
```
it doesn't overwrite the contents of hello2.txt, but adds to that.

**|**
    Means take the output of the program to the left, and make it the output of the program to the right.
    
**tails** 
    This prints the last end lines of it's input.<br>
Example:
``` shell script
ls -l / | tail -n1
```

<h3>KERNEL</h3>
<strong>cd ~/sys && ls</strong>
    This is a whole new world. These are not files, these are kernel parameters.

**Example:**
**Changing the laptops brightness**
``` shell script
anil@anil-SATELLITE-L50-B:/sys/class$ ls
ata_device   devfreq-event   i2c-adapter    misc          pps           scsi_generic  vfio
ata_link     dma             i2c-dev        mmc_host      printer       scsi_host     video4linux
ata_port     dmi             ieee80211      nd            ptp           sound         virtio-ports
backlight    drm             input          net           pwm           spi_master    vtconsole
bdi          drm_dp_aux_dev  iommu          pci_bus       rapidio_port  spi_slave     wakeup
block        extcon          kfd            pci_epc       regulator     thermal       watchdog
bluetooth    firmware        leds           phy           remoteproc    tpm           wmi_bus
bsg          gpio            mdio_bus       powercap      rfkill        tpmrm
dax          graphics        mei            power_supply  rtc           tty
devcoredump  hidraw          mem            ppdev         scsi_device   usbmisc
devfreq      hwmon           memstick_host  ppp           scsi_disk     vc
anil@anil-SATELLITE-L50-B:/sys/class$ cd backlight/intel_backlight
anil@anil-SATELLITE-L50-B:/sys/class/backlight/intel_backlight$ ls
actual_brightness  brightness  max_brightness  scale      type
bl_power           device      power           subsystem  uevent
anil@anil-SATELLITE-L50-B:/sys/class/backlight/intel_backlight$ cat brightness 
892
anil@anil-SATELLITE-L50-B:/sys/class/backlight/intel_backlight$ sudo su
[sudo] password for anil: 
root@anil-SATELLITE-L50-B:/sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-eDP-1/intel_backlight# echo 500 > brightness
```

<h2>Lecture 2: Shell Tools and Scripting (2020)</h2>
**Source:** https://missing.csail.mit.edu/2020/shell-tools/ <br>

* Spaces are really important in bash. It seperates the arguments.

* For strings, "" and '' is different.
"" allows using variables in the string. So some parts of the string can be dynamic with that option.
'' is for literal strings.

**Defining variables:** You can define variables with "="
Example:
``` shell script
anil@anil-SATELLITE-L50-B:~$ foo=hello
anil@anil-SATELLITE-L50-B:~$ echo $foo
hello
```


As with most programming languages, bash supports control flow techniques including if, case, while and for. 
Similarly, bash has functions that take arguments and can operate with them. 
Here is an example of a function that creates a directory and cds into it.
``` shell script
mcd () {
    mkdir -p "$1"
    cd "$1"
}
```

Unlike other scripting languages, bash uses a variety of special variables to refer to arguments, error codes, and other relevant variables. Below is a list of some of them. A more comprehensive list can be found here.

    $0 - Name of the script
    $1 to $9 - Arguments to the script. $1 is the first argument and so on.
    $@ - All the arguments
    $# - Number of arguments
    $? - Return code of the previous command
    $$ - Process identification number (PID) for the current script
    !! - Entire last command, including arguments. A common pattern is to execute a command only for it to fail due to missing permissions; you can quickly re-execute the command with sudo by doing sudo !!
    $_ - Last argument from the last command. If you are in an interactive shell, you can also quickly get this value by typing Esc followed by .

//todo: Sort this lesson some other way. Video is chaotic.

<h2>Lecture 3: Editors (Vim)</h2>
**Source:** https://missing.csail.mit.edu/2020/editors/ <br>

* Vim is a modal editor.
* Vim's interface itself is a programming language. 
That means, different key combinations has different effects and once you learn the different effects you can actually combine them 
together, just like a programming language you can learn different functions and stuff and then glue them all together 
to make an interesting program in the same way once you learn vims different and editing commands and things like that, 
you can talk to vim by programming vim through its interface, and once this becomes muscle memory you can basically edit files
at the speed which you think.

<h3>Keys & Fundemental Commands</h3>
i = Goes to insert mode.
esc = Goes back to normal mode.

**Undo**
u = undo
If you press "u" after going out of insert mode to normal mode, then it will undo everything you did in that previous insert mode 

^R = redo

:w = save changes?
:q = Quit
:qa = Quit all

x = deletes a character
d + w = delete a word
d + e = deletes the end of the word
dd = deletes the whole row

y = copy
p = paste

~ = Changes case of the selection

**r(replace)**
r + ? = takes another char as an argument and replaces cursors char 

**C (Change) These commands puts vim into insert mode after completion** 
c + e = deletes the end of a word
c + c = deletes the line

o = inserts line below (At normal mode)
O = inserts line above (At normal mode)

<h3>Navigation</h3>
Navigating the cursor can be done with h j k l .
These buttons corresponds to: left, down, up, right.
Dont waste time by moving your hand to the arrow keys they say. 

w = moves the cursor forward by one word.
d = moves the cursor back by one word.
e = moves the cursor to the end of a word.

b = Goes back but I dunno the difference between this and d
0 = goes to the beginning of the current line,
$ = goes to the end of the current line.
^ = goes to the first non-empty character of the current line.

^u = scrolls up
^d = scrolls down

**--Visual Mode--**
v = enters Visual mode.
Once you are in visual mode, you can use most of your normal mode keys to move your pointer around. 
w = to move by words.

**--Visual Line Mode--**
V = Enters Visual Line mode
Can be used to select whole rows of text. 

**--Visual Block Mode--**
^V = Enters Visual Block mode
Can be used to select rectangular blocks.

**Counts**
You can give vim a number to do some particular thing some number of times.
For example, if you wanna go down 4 rows, you can press 4 + j and you will go down four rows instead of one.

**Modifiers**



<h2>Data Wrangling</h2>
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
    

<h2>Lecture 6: Version Control (Git)</h2>

