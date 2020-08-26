<h2>Lecture 2: Shell Tools and Scripting (2020)</h2>
**Source:** https://missing.csail.mit.edu/2020/shell-tools/ <br>

* Spaces are really important in bash. It seperates the arguments.

* For strings, "" and '' is different.
"" allows using variables in the string. So some parts of the string can be dynamic with that option.
'' is for literal strings.

**Variables:** You can define variables with "="
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
    mkdir -p "$1" # $1 is the first argument
    cd "$1"
}
```

**EXAMPLES:**
``` shell script
# feeding pwd to echo
anil:~$ echo "We are in $(pwd)"
We are in /home/anil

# date variable (predefined by shell):
anil:~$ echo $(date)
Çrş 26 Ağu 2020 13:45:46 +03

# Feeding echo with the result
anil:~$ grep README edit.sh < echo
vim README.md

# This is an alternative to command above, but using < feels like the right way for this
anil:~$ echo $(grep README edit.sh)
vim README.md
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

    
**source**
    Read and execute commands from FILENAME in the current shell.
    
**!!**
     Most of the time you can use this when you forget sudo. Example:
     

``` shell script
anil@anil-SATELLITE-L50-B:~/PhpstormProjects/untitled$ apt-get update
Reading package lists... Done
E: Could not open lock file /var/lib/apt/lists/lock - open (13: Permission denied)
anil@anil-SATELLITE-L50-B:~$ sudo !!
sudo apt-get update
[sudo] password for anil: 
Hit:1 http://tr.archive.ubuntu.com/ubuntu focal InRelease
...
```

**grep**
    Searching a file for a string. Probably used for much more.
``` shell script
anil:~$ grep aramametni edit.sh 
anil:~$ echo $?
1 # this means string is not found
anil:~$ echo $(grep README edit.sh)
vim README.md
anil:~$ echo $(grep README edit.sh -c)
1
```

    || - OR operator
    && - And operator. Will only execute if the first one is successfull.
    
    
**touch**
    The touch command is a standard command used in UNIX/Linux operating system which is used to create, change and modify timestamps of a file. Basically, there are two different commands to create a file in the Linux system which is as follows:

        cat command: It is used to create the file with content.
        touch command: It is used to create a file without any content. The file created using touch command is empty. This command can be used when the user doesn’t have data to store at the time of file creation.

21:00'da kaldık. Karışık anlatıyor çocuk açıklamıyor komutları. Belki sonra geri dönerim bu videoya.