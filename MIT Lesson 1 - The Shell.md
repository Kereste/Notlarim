<h2>Lecture 1: Course overview + The Shell</h2>
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
	-l is especially helpful. Still gives the list of files but shows more detail. 
	-a shows all files. Even the hidden ones. (todo: be sure of this)

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