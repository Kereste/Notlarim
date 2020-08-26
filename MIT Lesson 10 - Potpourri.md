<h1>Lecture 10: Potpourri</h1>
<strong>Source:</strong> https://missing.csail.mit.edu/2020/potpourri/ <br>

<h2>Cron</h2>
The software utility cron also known as cron job is a time-based job scheduler in Unix-like computer operating systems. 
Users that set up and maintain software environments use cron to schedule jobs (commands or shell scripts) to run periodically at fixed times, dates, or intervals.
``` shell script
man cron # This is a much useful command for understanding cron.
``` 


<h2>Keyboard Remapping</h2>
This usually involves some software that is listening and, whenever a certain key is pressed, it intercepts that event and replaces it with another event corresponding to a different key.
Details are at the source reading material.

<h2>Daemons</h2>
<p>Most computers have a series of processes that are always running in the background rather than waiting for a user to launch them and interact with them. 
These processes are called daemons and the programs that run as daemons often end with a d to indicate so. 
For example sshd, the SSH daemon, is the program responsible for listening to incoming SSH requests and checking that the remote user has the necessary credentials to log in.</p>

<p>In Linux, **systemd (the system daemon)** is the most common solution for running and setting up daemon processes.</p>

**systemctl status**<br>
    Lists the currently running deamons.<br>
    Systemd can be interacted with the systemctl command in order to **enable**, **disable**, **start**, **stop**, **restart** or check the **status** of services (those are the systemctl commands).


<h2>FUSE</h2>

FUSE (Filesystem in User Space) allows filesystems to be implemented by a user program. FUSE lets users run user space code for filesystem calls and then bridges the necessary calls to the kernel interfaces. In practice, this means that users can implement arbitrary functionality for filesystem calls.

For example, FUSE can be used so whenever you perform an operation in a virtual filesystem, that operation is forwarded through SSH to a remote machine, performed there, and the output is returned back to you. This way, local programs can see the file as if it was in your computer while in reality it’s in a remote server. This is effectively what sshfs does.

Some interesting examples of FUSE filesystems are(Links are at the source):

    sshfs - Open locally remote files/folder through an SSH connection.
    rclone - Mount cloud storage services like Dropbox, GDrive, Amazon S3 or Google Cloud Storage and open data locally.
    gocryptfs - Encrypted overlay system. Files are stored encrypted but once the FS is mounted they appear as plaintext in the mountpoint.
    kbfs - Distributed filesystem with end-to-end encryption. You can have private, shared and public folders.
    borgbackup - Mount your deduplicated, compressed and encrypted backups for ease of browsing.

<h2>Backups</h2>
Some core features of good backups solutions are versioning, deduplication and security. 
Versioning backups ensure that you can access your history of changes and efficiently recover files. 
Efficient backup solutions use data deduplication to only store incremental changes and reduce the storage overhead. 
Regarding security, you should ask yourself what someone would need to know/have in order to read your data and, more importantly, 
to delete all your data and associated backups. 
Lastly, blindly trusting backups is a terrible idea and you should verify regularly that you can use them to recover data.



<h2>APIs</h2>
[IFTTT](https://ifttt.com/) is a website and service centered around the idea of APIs — it provides integrations with tons of services, and lets you chain events from them in nearly arbitrary ways. Give it a look!


**cURL(Client URL)**<br>
cURL is a computer software project providing a library and command-line tool for transferring data using various network protocols.

``` shell script
curl https://api.weather.gov/points/42.3604,-71.094 > firstCurl.txt
```
todo: Yukarıdaki komutla dönen datayı bir ara işle bash ile.

<h2>Common command-line flags/patterns</h2>
Directly check this at the source. Find the exact header.

<h2>Window managers</h2>
It's only floating windows these days!
But you can try other types.
todo: Try [tmux](https://github.com/tmux/tmux/wiki)!


Docker, Vagrant, VMs, Cloud, OpenStack
Vagrant is a tool that lets you describe machine configurations (operating system, services, packages, etc.) in code, 
and then instantiate VMs with a simple vagrant up. Docker is conceptually similar but it uses containers instead.

You can also rent virtual machines on the cloud, and it’s a nice way to get instant access to:

    A cheap always-on machine that has a public IP address, used to host services
    A machine with a lot of CPU, disk, RAM, and/or GPU
    Many more machines than you physically have access to (billing is often by the second, so if you want a lot of computing for a short amount of time, it’s feasible to rent 1000 computers for a couple of minutes)

Popular services include Amazon AWS, Google Cloud, and DigitalOcean.
