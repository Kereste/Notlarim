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
    mkdir -p "$1" # $1 is first argument
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