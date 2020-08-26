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
todo: add this after experimenting more.

