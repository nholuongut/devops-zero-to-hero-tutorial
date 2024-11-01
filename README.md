# Maya Sekhon - DevOps Zero-to-Hero Tutorial

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>
## Index

- [DevOps Intro](#devops-intro)
- [Linux / Unix Basics](#linux--unix-basics)
  - [Unix File System Layout](#unix-file-system-layout)
  - [Unix Shells](#unix-shells)
  - [Standard Input, Standard Output and Standard Error](#standard-input-standard-output-and-standard-error)
- [Linux / Unix - Basic Commands](#linux--unix---basic-commands)
  - [File System](#file-system)
  - [String Processing](#string-processing)
  - [User Management](#user-management)
  - [Process Management](#process-management)
  - [Performance & Space Management](#performance--space-management)
  - [Networking](#networking)
  - [Logging & Tracing](#logging--tracing)
  - [Compression](#compression)
- [Networking Basics](#networking-basics)
- [SSH](#ssh)
- [Editor / IDE](#editor--ide)
- [Make / Makefiles](#make--makefiles)
- [Git](#git)
  - [Git Commands](#git-commands)
    - [Example](#example)
  - [GitHub](#github)
  - [GitHub alternatives - GitLab, BitBucket, Azure DevOps](#github-alternatives---gitlab-bitbucket-azure-devops)
- [CI/CD - Continuous Integration / Continuous Delivery](#cicd---continuous-integration--continuous-delivery)
  - [GitHub Actions](#github-actions)
  - [Azure DevOps Pipelines](#azure-devops-pipelines)
  - [CircleCI](#circleci)
  - [Travis CI](#travis-ci)
  - [Jenkins](#jenkins)
- [Virtualization](#virtualization)
  - [Popular Virtualization Software](#popular-virtualization-software)
- [Data Formats](#data-formats)

## DevOps Intro

DevOps is short for Development Operations. It's a multi-disciplinary field combining programming and
infrastructure to automate and speed up delivery of software.

DevOps refers both to the wide variety of tools used, the engineers who operate them and to the methodology of closer collaboration between infrastructure and
software engineering teams for quicker iterations.

In the real world, DevOps practitioners typically come from a Linux background and favour open-source technologies which
are free, to skip the need for licensing or paperwork such as purchase orders.
Proprietary paid for software tools are used when no free alternatives are good enough. Cloud computing, although proprietary,
is heavily underpinned by open-source technologies such that many of the open-source tools work the same and
the compute-on-demand pay-as-you-go model means lower capex at the expense of higher opex and convenience.

<img src="https://octopus.com/devops/i/x/octopus-devops-infinity.png" alt="DevOps Infinity Diagram" width=600 height=300>

## Linux / Unix Basics

Linux is the standard open source operating system, based on Unix design.

Linux is technically just the operating system kernel, while the many command line tools called Core Utils are typically provided by [GNU](https://www.gnu.org/home.en.html).
Together they form a complete operating system called GNU / Linux which is further wrapped by Linux distributions
which include easy installers and commands to download and install further software (software package management).
The most popular Linux distributions include
[Redhat](https://www.redhat.com/en)
, [Debian](https://www.debian.org/)
and [Ubuntu](https://ubuntu.com/)
or are based on one of those.
There are many more Linux distributions that fill specific niches.

### Unix File System Layout

The [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) defines the common layout you'll find across all unix style systems, including Linux.

Everything is a file on Unix, even devices (found under `/dev`).

Each open file gets its own file descriptor eg. `/dev/fd/<number>`.

Binaries & Libraries:

| Directory         | Description                                                                                                                |
|-------------------|----------------------------------------------------------------------------------------------------------------------------|
| `/bin`            | core binaries                                                                                                              |
| `/usr/bin`        | more user binaries                                                                                                         |
| `/sbin`           | system binaries                                                                                                            |
| `/usr/sbin`       | more system binaries                                                                                                       |
| `/usr/local/bin`  | 3rd party installed user binaries                                                                                          |
| `/usr/local/sbin` | 3rd party installed system binaries                                                                                        |
| `/lib`            | libraries for binaries in `/bin` and `/sbin`                                                                               |
| `/usr/lib`        | libraries for the binaries in `/usr/bin` and `/usr/sbin`                                                                   |
| `/usr/local/lib`  | libraries for the binaries in `/usr/local/bin` and `/usr/local/sbin`                                                       |
| `/opt`            | another location for installing optional / 3rd party software, often used by major installation programs such as Oracle DB |

Virtual File Systems:

| Directory         | Description                                                                                                                |
|-------------------|----------------------------------------------------------------------------------------------------------------------------|
| `/dev`            | device files representing every piece of hardware, disk, device, usb etc.                                                  |
| `/proc`           | process and kernel info exposed as virtual files                                                                           |
| `/sys`            | system info exposed as virtual files                                                                                       |

Home Directories:

| Directory         | Description                                                                                                                |
|-------------------|----------------------------------------------------------------------------------------------------------------------------|
| `/root`           | home directory for the root user                                                                                           |
| `/home`           | home directories for each user                                                                                             |
| `/User`           | home directories for each user on Mac instead of `/home`                                                                   |

System Configurations:

| Directory         | Description                                                                                                                |
|-------------------|----------------------------------------------------------------------------------------------------------------------------|
| `/boot`           | contains the Linux kernel and `initrd` used to boot the OS                                                                 |
| `/etc`            | configuration files                                                                                                        |
| `/usr/local/etc`  | 3rd party installed config files                                                                                           |
| `/mnt`            | mounted extra filesystems                                                                                                  |
| `/tmp`            | temporary files (often wiped after shutdown)                                                                               |
| `/var/tmp`        | more temporary runtime files                                                                                               |
| `/var/cache`      | temporarily cached files for running software, package manager lists                                                       |
| `/var/log`        | system log files                                                                                                           |

### Unix Shells

The Unix command line is extremely powerful and there are several shells to choose from.
The default shell on Linux is Bash, which is based on the Bourne shell (Bash stands for Bourne again shell).
Other popular shells include ZSH and Fish. Mac has in recent years switched the default shell to `zsh` to avoid GNU GPL open source licensing.

The `root` account is the superuser admin account which always has UID 0.
There should be no other account with UID 0 otherwise it would also be a root superuser account.

### Standard Input, Standard Output and Standard Error

Standard Input is the data input that is streamed into any command via an interactive prompt, or a pipe (`|`) from another command, or an input redirect (`<`) from a file.
Commands that expect standard input like `cat` or `grep`, if not given file arguments, will hang waiting until they receive some input.

Standard Output is the main output stream from any command that is printed to the terminal unless you redirect it into a pipe (`|`) to another command's Standard Input, or an output redirect (`>`/ `>>`) to a file.

Standard Error is the secondary output where only errors or logs are sent. This is also printed to the terminal unless redirected via `2>` / `2>>`

The standard file descriptors for Standard Input, Standard Output and Standard Error are 0, 1 and 2 respectively and can be used at the command line via their file descriptors at `/dev/fd/0`, `/dev/fd/1`, `dev/fd/2`.

Most Unix commands often work as standard Unix filter programs where they can accept input from Standard Input or read the contents of a file given as an argument and they output to Standard Output so that they can be chained into any number of subsequent commands separated by pipe symbols.

This combined with the rich ecosystem of bundled Unix commands is the true power of Unix shells.

## Linux / Unix - Basic Commands

Open a terminal. On Mac open `Terminal`, on Linux open `xterm` or `aterm`. These are applications in which to run
your shell in a window inside your GUI.

To find a command, it must be in the `$PATH`. You will likely need to extend the path to include custom installation directories like so:

```shell
export PATH="$PATH:/path/to/some/directory"
```

Common switches are `-h` / `--help`, `-v` / `--verbose`, `-V` / `--version`. The long options with `--` are typically GNU convention

For more detailed help, type `man <command>`. To search for manual pages run `man -k <command>`.

| Command     | Description                                                                                                                                                                                                                                          |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `echo`      | prints a given string argument to standard output                                                                                                                                                                                                    |
| `clear`     | clears the terminal screen, leaving your cursor at the top (`ctrl-l` is a shortcut)                                                                                                                                                                  |
| `tmux`      | terminal multiplexer - runs multiple shells in your terminal window and preserves your shell sessions if your terminal crashes or is accidentally closed                                                                                             |
| `which`     | shows the full path to a given command                                                                                                                                                                                                               |
| `type`      | similar to `which` but finds shell built-in commands                                                                                                                                                                                                 |
| `grep`      | filters from standard input or a file and only prints to standard output lines that match the given regex filter argument                                                                                                                            |
| `pbcopy`    | copies Standard Input to the GUI clipboard on Mac                                                                                                                                                                                                    |
| `pbpaste`   | pastes the GUI clipboard to Standard Output on Mac                                                                                                                                                                                                   |
| `xclip`     | copies Standard Input to the GUI (X) clipboard on Linux                                                                                                                                                                                              |
| `env`       | shows environment variables or sets environment variables and runs commands                                                                                                                                                                          |
| `set`       | sets shell options such as `set -e` (usually used in scripts), or without args shows everything defined in the shell such as environment variables, aliases and functions                                                                            |
| `history`   | shows list of commands previously executed in your shell                                                                                                                                                                                             |
| `diff`      | compares files line by line, shows the differing lines                                                                                                                                                                                               |
| `date`      | shows date and time, sets date and time, or shows the date / time in the format specified by a strftime string                                                                                                                                       |
| `rsync`     | transfers / synchronizes files or directories efficiently between two directories by comparing timestamps (or optionally checksums) and only copies the files that are newer than the destination                                                    |
| `find`      | finds files and directories, optionally perform commands on them, eg. `find . -name README.md`                                                                                                                                                       |
| `xargs`     | reads standard input and uses it as arguments to the given command eg. `\| xargs <command>`                                                                                                                                                          |                                                                                                                                            |
| `file`      | shows the type of a given file eg. `ASCII text` or `POSIX tar archive`                                                                                                                                                                               |
| `tar`       | creates or extracts tarballs (bundle archives of files / directories), usually used for backups eg. `tar cvfz my.tar.gz somedirectory` and `tar xvfz my.tar.gz`                                                                                      |
| `dd`        | Data Duplicator - copies raw data from one source to another. Can be used the clone hard drives, partitions or create files of given sizes from special pseudo-devices like `/dev/zero` eg. `dd if=/dev/zero of=/path/to/my/file bs=1024 count=1024` |

#### File System

| Command   | Description                                                                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pwd`     | shows present working directory                                                                                                                                            |
| `cd`      | change directory, `cd -` to jump to last directory, `cd` without args to jump to `$HOME` directory                                                                         |
| `ls -l`   | list files and directories                                                                                                                                                 |
| `cp`      | copies files or directories                                                                                                                                                |
| `mv`      | moves files or directories                                                                                                                                                 |
| `rm`      | deletes files / directories. Common switches are `-r` to recursively delete into directories, and `-f`/`--force`                                                           |
| `mkdir`   | creates a directory                                                                                                                                                        |
| `rmdir`   | deletes an empty directory, fails with an error if not empty, in which case you need to use `rm -r` to also delete the directory and its contents (files / subdirectories) |
| `chown`   | change ownership of files or directories                                                                                                                                   |
| `chgrp`   | change group ownership of files or directories                                                                                                                             |
| `chmod`   | change file octal permissions eg. `chmod 755`                                                                                                                              |
| `touch`   | updates the modified timestamp of a file or creates an empty file if it doesn't exist                                                                                      |
| `cat`     | reads the contents of the file or standard input to standard output, your terminal if not redirected or piped to another command                                           |
| `head`    | reads the first N lines of a file or standard input                                                                                                                        |
| `tail`    | reads the last N lines of a file or standard input                                                                                                                         |
| `more`    | a paging program that displays one screenfull at a time and allows you to scroll down through longer outputs such as standard output from piped commands or files          |
| `less`    | a better replacement of `more` that allows you to scroll upwards as well as downwards                                                                                      |
| `tree`    | lists contents of directories in a tree-like format                                                                                                                        |
| `>`       | overwrite file                                                                                                                                                             |
| `>>`      | append file                                                                                                                                                                |

#### String Processing

| Command  | Description                                                                                                                                                                                                                          |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tr`     | replaces characters from standard input                                                                                                                                                                                              |
| `sed`    | stream editor - replaces strings or deletes from standard input via regex searches                                                                                                                                                   |
| `awk`    | text processing language, usually used for quick one-liners, also supports regex matches, can print numbered columns                                                                                                                 |
| `cut`    | cuts out selected portions of each line by bite, character or field eg. 1st and 3rd fields `cut -d ' ' -f 1,3`                                                                                                                       |
| `column` | aligns input into vertically aligned columns, usually called as `column -t`                                                                                                                                                          |
| `vi`     | text editor, the classic Unix terminal text editor, doesn't require a GUI, almost universally available on every server. If you need to edit a config file on a server, you will need to use this or another terminal editor program |
| `vim`    | `vi` improved - fuller features replacement editor to `vi`. `vi` is more commonly available on minimalist systems such as some servers but `vim` package is available to install                                                     |

#### User Management

| Command     | Description                                                                                                                                                                                                                                             |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`        | shows the current or given user's UID, GID and group memberships                                                                                                                                                                                        |
| `who` / `w` | display who is logged in                                                                                                                                                                                                                                |
| `sudo`      | assumes the permissions of `root` or a given `-u <user>` for the duration of the following command must be pre-approved in `/etc/sudoers`) conifiguration. Prompts for the current user's password and caches for subsequent `sudo` calls within 5 mins |
| `su`        | switch user, defaults to `root` if no user arg is given. Prompts for the target user's password and starts a new shell as that user                                                                                                                     |
| `useradd`   | creates a new user account                                                                                                                                                                                                                              |
| `userdel`   | deletes a user account                                                                                                                                                                                                                                  |
| `gpasswd`   | administers the /etc/group and /etc/gshadow                                                                                                                                                                                                             |
| `pwgen`     | generates a secure, random password of configurable length and complexity eg. `pwgen -1 20`                                                                                                                                                             |

#### Process Management

| Command   | Description                                                                                                                                                                                   |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pgrep`   | finds processes by regex                                                                                                                                                                      |
| `bg`      | background run the suspended process from `ctrl-z`                                                                                                                                            |
| `ctrl-c`  | kill / cancel the current foreground process in the shell                                                                                                                                     |
| `ctrl-z`  | suspend the current foreground process, placing it into the background                                                                                                                        |
| `jobs`    | shows backgrounded jobs, suspended or running                                                                                                                                                 |
| `ps`      | shows running processes. Commonly called as `ps -ef` or `ps aux` to show all processes on a unix based system                                                                                 |
| `fg`      | foreground run the suspended process from `ctrl-z`                                                                                                                                            |
| `wait`    | waits for all background processes to finish before returning the shell prompt                                                                                                                |
| `kill`    | kills a process by PID or sends it a specific signal                                                                                                                                          |
| `killall` | same as above, by name                                                                                                                                                                        |
| `pkill`   | same as above, by regex pattern matching name                                                                                                                                                 |
| `nohup`   | no hang up - lets a command keep running even if your shell is closed eg. broken ssh connection (this usually results in a HUP signal being sent to the process causing it to exit otherwise) |

#### Performance & Space Management

| Command    | Description                                                                                                                                                                                             |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `df`       | disk free - shows disk space for one or all disks eg. `df -h` for human units, `df -h /` for disk space of root disk or `df -h .` for disk space in the current partition where you are (`$PWD`)        |
| `du`       | disk used - counts the disk space used for given files or directories, eg. `du -h -s $HOME` to see how much space your home directory has taken in human-readable units eg. GB                          |
| `time`     | times how long a command takes                                                                                                                                                                          |
| `free`     | shows total used and free RAM eg. `free -h` for human readable units                                                                                                                                    |
| `top`      | shows live process information, usually sorted by CPU or RAM - most useful details are PID, CPU, RAM, USER and COMMAND                                                                                  |
| `lsof`     | list open files open files and directories, the processes which currently have them opened, along with the user and PID                                                                                 |
| `vmstat`   | virtual memory stats - shows RAM, CPU, disk I/O etc.                                                                                                                                                    |
| `dstat`    | similar to `vmstat`                                                                                                                                                                                     |
| `lscpu`    | shows number of CPUs, cores etc.                                                                                                                                                                        |
| `nproc`    | the number of CPU cores available to the current process (could be less than the hardware if a limit has been applied to your user or process)                                                          |

#### Networking

| Command         | Description                                                                                                                                                                                                                                                   |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `hostname`      | shows the hostname with domain (FQDN), use `-s` for short name without domain                                                                                                                                                                                 |
| `ifconfig`      | shows or configures network interfaces, usually used to show your IP address                                                                                                                                                                                  |
| `ip`            | similar to `ifconfig`, `ip addr` to show your IP address                                                                                                                                                                                                      |
| `ping`          | sends an ICMP echo request to a device, expects an ICMP echo reply if online. The most basic networking test of connectivity                                                                                                                                  |
| `traceroute`    | print the route packets take to network host, by sending a series of ICMP echo request with increasing TTLs so each router along the path rejects it and exposes its IP                                                                                       |
| `route`         | shows or configures the network routing cables eg. `route -n`                                                                                                                                                                                                 |
| `netstat`       | shows the network connections, connected or listening ports. Commonly called as `netstat -an` or `netstat -lntpu`                                                                                                                                             |
| `host`          | performs DNS lookup for a given hostname or FQDN                                                                                                                                                                                                              |
| `dig`           | similar to `host` but more query options and returns more info                                                                                                                                                                                                |
| `curl`          | get a web page URL via HTTP(S) or send data eg. JSON to a web service in an HTTP(S) request                                                                                                                                                                   |
| `wget`          | similar to curl, downloads web pages to local files by default, use `wget -O - ...` to output to stdout to emulate curl's behaviour on minimalist systems that don't have curl installed but have wget bundled inside the busybox shell, such as Alpine Linux |
| `ssh`           | Secure Shell - connects to a remote server and opens a shell                                                                                                                                                                                                  |
| `scp`           | Secure Copy - copies a file to remote server via SSH                                                                                                                                                                                                          |
| `ssh-keygen`    | generates an SSH public / private key pair for passwordless logins to remote ssh servers (see SSH section further down)                                                                                                                                       |
| `nmap`          | Network Map - scans ports on a target server or range of IPs by sending TCP syn packets to check what ports are open, useful to find services on the network                                                                                                  |
| `netcat` / `nc` | opens sockets to local or remote systems, useful for testing open ports or text-based services eg. HTTP, SMTP etc.                                                                                                                                            |
| `iptables`      | lists or modifies the Linux local IP firewall table eg. `iptable -nL`                                                                                                                                                                                         |

#### Logging & Tracing

| Command      | Description                                                                                        |
|--------------|----------------------------------------------------------------------------------------------------|
| `dmesg`      | shows system kernel logs                                                                           |
| `journalctl` | opens systemd logs                                                                                 |
| `strace`     | traces system calls and signals, eg. file open / read / close, network socket open / send / close  |
| `dtruss`     | similar to `strace` but for Mac                                                                    |

#### Compression

| Command     | Description                                                                                                                                |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `gzip`      | compresses files using the gzip compression algorithm, adds the `.gz` file extension                                                       |
| `gunzip`    | decompresses `.gz` files                                                                                                                   |
| `bzip2`     | compresses files using the bzip2 compression algorithm (more compression but slower)                                                       |
| `bunzip2`   | decompresses `.bz2` files                                                                                                                  |
| `zless`     | shows compressed or plain text files one screen at a time (pipes gzipped files through `gunzip` before opening in `less`)                  |
| `bzless`    | same as `zless` but for `bzip2`                                                                                                            |
| `zip`       | creates zip compression archives                                                                                                           |
| `unzip`     | extracts zip compression archives                                                                                                          |
| `md5sum`    | generates md5 hash of a file's contents, or validates that a saved md5 checksum hash matches the hash computed for a given file's contents |
| `md5`       | same as above, on Mac                                                                                                                      |
| `shasum`    | computes the SHA-1 hash of a file's contents (a hex string that is unique to a given content input)                                        |
| `sha1sum`   | same as above, on Mac                                                                                                                      |
| `sha256sum` | same as above, with longer SHA-256 hash                                                                                                    |
| `sha512sum` | same as above, with longer SHA-512 hash                                                                                                    |

## Networking Basics

| Command                                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| IP address                                 | the unique address of the computer / device on a network. Most computers are still using IPv4 addresses in the format `1.2.3.4`, with the eventual intention of migrating to IPv6                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Subnet mask / netmask                      | an address that when AND'd against the IP address, leaves just the network portion of the IP address                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Network address                            | the IP address range, used by every device to determine if the remote IP is on the local network or a remote network                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Switch                                     | device with multiples ports connecting different computers on the local network                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Router                                     | device which connects 2 or more networks together                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Gateway                                    | a router that is sent traffic to forward on to other networks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Default Gateway                            | the router that you send all your remote traffic to when you don't have a more specific router to send it to e.g. your home broadband router for all traffic going to the internet                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| DNS - Domain Name System                   | software that translates host names and domain names into IP addresses for network connections to initiate. Every computer has a DNS client that queries DNS servers on the internet that is used everytime you put a URL into your web browser. Popular DNS server software includes Bind, Microsoft DNS, DNSmasq, djbdns                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Hostname                                   | the name of your computer on the local network                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Domain Name                                | the address suffix used to group websites and email addresses eg. google.com                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| FQDN - Fully Qualified Domain Name         | the complete host name and domain address eg. www.google.com                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| URL - Uniform Resource Locator             | the full path to a website's webpage eg. https://linkedin.com/in/maya-sekhon                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| TCP - Transmission Control Protocol        | connection-based protocol, retransmits lost packets, delivers in sequence, used underneath many other protocols eg. HTTP, SSH                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| UDP - User Datagram Protocol               | connectionless protocol, less reliable but lower overhead so faster, doesn't detect packet loss or retransmit or guarantee sequence order. Apps have to manage packet loss and retries themselves. DNS is an example of a UDP-based protocol where the DNS client software retries itself. Other examples include NFS, Video streaming, VoIP (Voice over IP)                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| IP - Internet Protocol                     | the standard for addressing internet connected devices and routing packets between them                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| IPv4                                       | the most widely used version of IP with 32-bit addresses usually written in 4 octet format from 0 - 255 eg. 4.2.2.1 or 192.168.1.10. There are ~4.3 billion IPv4 addresses (which are running out)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| IPv6                                       | newer format with more IP addresses available due to 128-bit format written in hexadecimal separated by colons  Used because IPv4 only has 4 billion IP addresses which are running out                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Public vs Private IPs                      | in IPv4, due to limited IPs, three address ranges are reserved for private local network use only. One of these three ranges are used for all home and local office networks. Communicating on the internet requires a public IP<br/>- Private IP address ranges are as follows:<br />- Class A Private IP Range: 10.0.0.0/8 ie. 10.0.0.0 – 10.255.255.255<br />- Class B Private IP Range: 172.168.0.0/12 ie. 172.16.0.0 – 172.31.255.255<br />- Class C Private IP Range: 192.168.0.0/16 ie. 192.168.0.0 – 192.168.255.255                                                                                                                                                                                                                                                                            |
| CIDR - Classless Inter-Domain Routing      | short way of representing a network combining an IP / netmask bits eg. 10.0.0.0 and 255.0.0.0 as 10.0.0.0/8 where the 8 represents an 8-bit netmask which is the same as 255.0.0.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| NAT - Network Address Translation          | local router converts your local devices private IP address to the public IP of the router before sending on to the internet so that servers can reply to the router which forwards the IP packets back to the local device on its private IP                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Static vs Dynamic IPs                      | IP addresses can be configured manually or automatically via DHCP                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| DHCP - Dynamic Host Configuration Protocol | client device broadcasts requesting an IP address using its DHCP client software. DHCP server hears the broadcast and replies with an IP address from its pool of configured IP addresses that the client device can use with a lease duration of typically 24 hours. After 24 hours, if the device is still online, it'll request to renew the lease, otherwise the lease will expire and the IP will be returned to the DHCP pool of available addresses                                                                                                                                                                                                                                                                                                                                              |
| MAC address - Media Access Control address | the physical network address on the network card, hardcoded, can be overridden in software                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| OSI model - Open Systems Interconnection   | seven-layer reference for responsibilities of each component in networking                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Firewall                                   | restricts traffic inbound / outbound to protect computers from untrusted networks. Layer 4 firewalls restrict based on IP + Port number combinations. Layer 7 firewalls filter based on application layer protocol knowledge such as HTTP / paths or protocol abuses                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Web Application Firewall                   | layer 7 firewall that understands HTTP traffic and blocks common attacks and protocol abuses such as SQL injection                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| NAT Firewall                               | layer 4 firewall that permits outbound and matching replies only. Maintains a connection table in RAM of source IP:port and destination IP:port combinations so that only matching replies are permitted back into the network to the requesting source computer                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Port Forwarding                            | opens a port number on a layer 4 firewall to permit outside traffic to flow into a computer in the internal network eg. forward port 80 to a webserver behind the firewall                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Load Balancer                              | accepts traffic on a given port and forwards it to one of several servers, therefore spreading the load of multiple inbound connections between a preconfigured group of servers eg. a web farm. This allows a website to scale to millions of users by allowing many servers to answer HTTP requests. It also allows for high availibility because if any one webserver crashes, it will send traffic to the remaining webservers and not the broken one. It detects if any server in the web farm is broken by using a preconfigured health check, usually a HTTP request with an optional `/path` which it repeats every few seconds to detect if a webserver stops responding properly, in which case it marks it as failed until the webserver starts working properly and the health check passes |

IPv4 Address Format:

![IPv4 address format](https://media.fs.com/images/community/upload/kindEditor/202110/07/ipv4-adress-1633571300-dsz7s7aL9Q.png)

IPv6 Address Format:

![IPv6 address format](https://media.fs.com/images/community/upload/kindEditor/202110/07/ipv6-address-1633571321-vaS1xaeWr9.png)

NAT - Network Address Translation:

![NAT](https://signal.avg.com/hs-fs/hubfs/Blog_Content/Avg/Signal/AVG%20Signal%20Images/Public%20vs.%20local%20IP%20addresses%20(Signal)/Public-vs-local-IP-addresses.png?width=2640&name=Public-vs-local-IP-addresses.png)

Find your public IP address via any of these commands:

```shell
curl ifconfig.co
```

```shell
curl ipinfo.io/ip
```

```shell
curl api.ipify.org
```

```shell
curl 'https://api.ipify.org?format=json'
```

## SSH

SSH stands for Secure Shell. It is the standard for connecting into remote shells on other computers across the network.
The connection is encrypted on port 22 and requires a remote username and password or SSH key.
An SSH server must be running on the remote computer (`sshd`).

```shell
ssh maya@somecomputer.domain.com
```

```shell
ssh maya@192.168.1.2
```

Create an ssh key

```shell
ssh-keygen
```

This generates a public and private key pair under `$HOME/.ssh/`,
by default `id_rsa` for the secret private key and `id_rsa.pub` for the public key.

Copy and paste the public key contents from `$HOME/.ssh/id_rsa.pub` into the `$HOME/.ssh/authorized_keys`
in any computer you want to automatically log into without a password prompt, or any public service like GitHub.

The public key is safe to send to colleagues via emails etc because you cannot derive the secret private key from it due to one-way asymmetric cryptography, so that they can add you into their servers authorised keys.

## Editor / IDE

Get yourself a good IDE (text editor with fancy features like autocomplete, syntax highlighting, version control etc.)

There are many to choose from, if you don't already have a favourite one just go with [Intellij IDEA](https://www.jetbrains.com/idea/) community edition (free).

If you're on Mac and want to be able to open files from the command line using the `idea` command from your shell, you will need to add it to the path:

```shell
export PATH="$PATH:/Applications/IntelliJ IDEA CE.app/Contents/MacOS"
```

## Make / Makefiles

Make is the classic, standard build system that executes the script contents of `Makefile`
in the current directory when you execute the `make` command.

For example, see the [Makefile](https://github.com/Nholuongut/devops-zero-to-hero-tutorial/blob/main/Makefile) in this repo.

If you're using Intellij, remember to add the [Makefile plugin](https://plugins.jetbrains.com/plugin/9333-makefile-language) for syntax support.

## Git

[Git](https://git-scm.com/) is a distributed version control system which saves every version of your software code and configuration files.

This allows you to track all changes made over time made by yourself and your colleagues, and handles most merging
of each other's changes as long as they're not on the same lines.

### Git Commands

| Command         | Description                                                                                                                                                           |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git init`      | creates a new Git repository (creates `.git/` directory storing your file changes and metadata)                                                                       |
| `git clone`     | clones a repo locally from an upstream server, such as GitHub                                                                                                         |
| `git add`       | marks files to be committed                                                                                                                                           |
| `git mv`        | moves or renames files (necessary for Git to track the move or rename, don't just use Unix `mv`)                                                                      |
| `git diff`      | shows you uncommitted changes made to files                                                                                                                           |
| `git commit`    | saves selected changed files in a new version hashref (a unique alphanumeric string representing this set of changes)                                                 |
| `git push`      | pushes your local commits to an upstream shared repository such as GitHub                                                                                             |
| `git pull`      | pulls the latest commits from the upstream shared repository                                                                                                          |
| `git branch`    | show branches / create a new branch                                                                                                                                   |
| `git checkout`  | checks out the files at a given ref (branch / tag / hashref)                                                                                                          |
| `git merge`     | merges a given branch into the current branch                                                                                                                         |
| `git tag`       | creates a tag for the current commit hashref easy to use human name or version number eg. v1.2.3                                                                      |
| `git log`       | shows the git log eg. `git log --all --graph --decorate` to see multi-branch history merges etc. or `git log -p` to see the patch diffs of each commit in the history |
| `git show`      | shows the diff at a specific commit                                                                                                                                   |
| `git config`    | configures settings for the local repo or global user settings eg. `git config --global user.name` or `git cnofig --global user.email`                                |
| `git remote -v` | shows the remote repos and their URLs                                                                                                                                 |

`.gitignore` - file listing paths to ignore, one per line, can be set globally in your home directory or in the root top level directory of the repository

#### Example

```shell
git clone git@github.com:Nholuongut/devops-Zero-to-Hero-Tutorial

# edit file
vim README.md

git diff
git commit -m "updated readme"

git push
```

### GitHub

[GitHub](https://github.com/) is a website which stores your Git repositories and has nice management features as well as CI/CD.

Make sure to enable Two-factor authentication (2FA) in your [security settings](https://github.com/settings/security). Get [Microsoft Authenticator app](https://www.microsoft.com/en-gb/security/mobile-authenticator-app).

Copy and paste the contents of your `$HOME/.ssh/id_rsa.pub` into your profile [keys settings](https://github.com/settings/keys)
(hint: `pbcopy < $HOME/.ssh/id_rsa.pub` on Mac to copy it straight into your clipboard).

Use SSH for your git clone / pull / push because you should be using autogenerated complex passwords that are stored in password managers such as [Chrome](https://www.google.com/intl/en_uk/chrome/)
/ [Lastpass](https://www.lastpass.com/)
/ [1password](https://1password.com/), and have MFA enabled.

If your organisation uses SSO enforced authentication for corporate controls via Azure Active Directory or similar IdP,
then don't forget to authorize your SSH key for your enterprise GitHub organisation using the `Configure SSO` drop down
to the right of the key.

### GitHub alternatives - GitLab, BitBucket, Azure DevOps

These are all just Git repo hosting websites with CI/CD built in.

- [Azure DevOps](https://azure.microsoft.com/en-gb/products/devops) - unlimited free CI/CD build minutes
- [GitLab](https://about.gitlab.com/) - similar feature parity to GitHub, but few free CI/CD build minutes (legacy)
- [BitBucket](https://bitbucket.org/product) - less feature rich and few free CI/CD build minutes (legacy)

GitHub's advantages over these alternatives include:

- most popular and widely used
- feature rich repository management (rivalled only by GitLab)
- huge ecosystem support and integrations
- GitHub can be used for automatic SSO logins to many other 3rd party developer websites
- better CI/CD, see [GitHub Actions section](#github-actions) further down
- Pull Requests with extensive customization:
  - merge control behaviours enforcing peer review approvals
  - CI build / lint checks passed enforcement
  - CI can update / modify / comment on Pull Requests

## CI/CD - Continuous Integration / Continuous Delivery

Continuous Integration means to automatically run any actions upon changes in the repo related to building artifacts, installing dependencies (eg. software libraries or OS packages), testing, linting, code quality checks etc.

Continuous Delivery is the next step where the software is delivered eg. deployed to a server (eg. copied and executed to run a new version of a website or software or config).

CI/CD is done via specialised software that watches your Git repo and automatically runs upon any changes to the files in the repo.

There are many different CI/CD software tools available to fulfill this function. Some prominent ones include:

- Cloud Hosted:
  - [GitHub Actions](https://github.com/features/actions)
  - [CircleCI](https://circleci.com/)
  - [GitLab CI/CD](https://docs.gitlab.com/ee/ci/)
  - [Azure DevOps Pipelines](https://azure.microsoft.com/en-gb/products/devops/pipelines)
  - [BitBucket Pipelines](https://bitbucket.org/product/features/pipelines)
  - [Travis CI](https://www.travis-ci.com/)
  - [AWS CodeBuild](https://aws.amazon.com/codebuild/)
  - [GCP CloudBuild](https://cloud.google.com/build)
- Self Hosted (Install and run on your own server or computer):
  - [Jenkins](https://www.jenkins.io/)
  - [Concourse](https://concourse-ci.org/)
  - [TeamCity](https://www.jetbrains.com/teamcity/)

and many others. For a more comprehensive list of badges of different CI, see [Nholuongut/DevSecOps-CI-CD-Pipeline](https://github.com/Nholuongut/DevSecOps-CI-CD-Pipeline) or https://nholuongut.netlify.app/.

### GitHub Actions

CI/CD built into each GitHub repo, requires just dropping in a yaml file into `.github/workflows`.

- unlimited free build minutes for public projects
- [Marketplace](https://github.com/marketplace?type=actions) of pre-built actions
- widespread support among 3rd party vendors providing ready made actions for their products such as various [SAST](https://en.wikipedia.org/wiki/Static_application_security_testing) tools
- better designed CI/CD than other cloud hosted vendors eg. multi-file workflows, separate repo badges etc.
- community pre-built reusable workflows are ready ro run, such as [Nholuongut/GitHub-Actions](https://github.com/Nholuongut/GitHub-Actions)

For examples, see [.github/workflows](https://github.com/Nholuongut/devops-zero-to-hero-tutorial/tree/main/.github/workflows).

For a master template, see the [Nholuongut/GitHub-Actions](https://github.com/Nholuongut/GitHub-Actions) repo [main.yaml](https://github.com/Nholuongut/GitHub-Actions/blob/master/main.yaml).

### Azure DevOps Pipelines

Azure DevOps Pipelines is the built-in CI/CD available alongside repos. Simply add `azure-pipelines.yml` to the root of your repo and enable in the website.

For a simple example, see the local [azure-pipelines.yml](/azure-pipelines.yml), or for a more real-world example,
see DevOps-Bash-tools [azure-pipelines.yml](https://github.com/Nholuongut/devops-Bash-tools/blob/master/azure-pipelines.yml).

### CircleCI

A well established, polished CI/CD solution with a nice GUI.

For example, see the local [.circlci/config.yml](https://github.com/Nholuongut/devops-zero-to-hero-tutorial/blob/main/.circleci/config.yml)
or the DevOps-Bash-tools [.circleci/config.yml](https://github.com/Nholuongut/devops-Bash-tools/blob/master/.circleci/config.yml)

### Travis CI

The original popular Cloud hosted CI/CD, no longer free for all public projects, considered legacy now.

Configuration template in [Nholuongut/Templates](https://github.com/Nholuongut/Templates) repo [.travis.yml](https://github.com/Nholuongut/Templates/blob/master/.travis.yml)

### Jenkins

The classic, most powerful and flexible CI/CD.

Free open-source server software, written in Java. You must install, run, administer and update it yourself.

Uses a lot of plugins to extend its core functionality.

Ultra powerful but more difficult to manage because you have to
administer the server yourself, including updating all your plugins, compared to Cloud hosted solutions like the above,
which require no administration.

Builds use a `Jenkinsfile` written in a DSL language, similar to code with braces and functions. See this master template [Jenkinsfile](https://github.com/Nholuongut/Jenkins/blob/master/Jenkinsfile) example.

Very powerful and flexible because you can write your own functions in the excellent [Groovy](https://groovy-lang.org/)
programming language. Many such functions can be found in the [Nholuongut/Jenkins](https://github.com/Nholuongut/Jenkins) repo.

Jenkins can have many agents installed on other servers to run pipelines. Jenkins integrates with the fantastic Kubernetes
platform to dynamically spawn agents in autoscaling Kubernetes clusters as needed. To quickly install Jenkins on Kubernetes
with auto-spawning agents, see the [Nholuongut/Kubernetes-configs](https://github.com/Nholuongut/Kubernetes-configs) repo.

A single Jenkins server will eventually hit performance and scalability limits in the server itself if coordinating and
scheduling hundreds of pipelines across agents.

[CloudBees](https://www.cloudbees.com/)
provides commercial software to run and manage multiple Jenkins servers centrally. This is because large enterprises
typically end up with many Jenkins installations for different teams and projects but want centralised control and governance.

For real-world Jenkins architecture and screenshots see the [Nholuongut/Jenkins](https://github.com/Nholuongut/Jenkins) repo.

## Virtualization

Virtualization allows installing multiple virtual machines on one physical machine, using a special piece of software
called a hypervisor that emulates computer hardware. Each virtual machine (VM) believes it's on its own computer and only sees the
virtual hardware presented by the hypervisor, but not any of the adjacent VMs.
Each VM can have different operating systems and versions installed.

The hypervisor allocates a fixed amount of computer resources to each VM eg. CPU, RAM, disk space.

Virtualization is used to utilise large server hardware capacity while maintaining isolation between different applications.
The alternative of trying to install and run many applications on a single bare metal server operating system would be difficult to manage,
with potential clashes of software dependencies, versions and libraries, and insecure because any misbehaving or
hacked application could potentially impact all of the other adjacent applications.
Virtualization solves this by allowing each application to run on its own isolated operating system with resource limits,
to prevent resource starvation by greedy adjacent apps.

Virtualization is also used on desktop computers to able to run software that would otherwise not be able to run on the base operating system
eg. Windows vs Mac vs Linux applications are specific to each operating system.

Benefits of virtual machines include:

- fuller utilisation of hardware capacity
- isolation between apps
- snapshots - can save the computer state at different points in time and can revert to a previous snapshot easily.
  This makes riskier changes and upgrades easy to roll back
- migration - virtual machine disks are stored as files on the computer and can be exported, copied, imported to migrate between computers
- appliances - virtual machine disks can be shared as ready-to-run installed computers with all software pre-installed and configured
- failover - enterprise hypervisors can automatically migrate and restart VMs on other servers if the server
  running the VM dies for any reason.
  The VM disk files are kept on shared network storage, accessible to each server for this.

### Popular Virtualization Software

- Server:
  - [VMware vSphere](https://www.vmware.com/uk/products/vsphere.html) - enterprise-grade mature software suite with centralised vCentre and ESXi server hypervisor, migration, failover etc.
  - [Microsoft Hyper-V](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/) on Windows Server - enterprise features like live VM migration between servers
- Desktop:
  - [Virtualbox](https://www.virtualbox.org/) - widely popular and easy to use, but only for x86-based processors eg. Intel or AMD
  - [VMware Workstation](https://www.vmware.com/uk/products/workstation-pro.html) / [Fusion](https://www.vmware.com/uk/products/fusion.html) -
    desktop virtualization software for Windows / Mac
  - [Microsoft Hyper-V](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/) on Windows - desktop app hypervisor
  - [Qemu](https://www.qemu.org/) - massively versatile but complex and difficult to use, but supports a wider range of processors such as new Apple Silicon (ARM processor)
  - [UTM](https://mac.getutm.app/) - easy to use Mac frontend to Qemu for new Apple Silicon processors

## Data Formats

| Format                                     | Description                                                                                                                                                                                                                                     |
|--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [YAML](https://en.wikipedia.org/wiki/YAML) | Yet Another Markup Language - simple way of representing key value pairs, lists, dictionaries. Usually used for config files eg. [readme-lint.yaml](https://github.com/Nholuongut/devops-zero-to-hero-tutorial/blob/main/.github/workflows/readme-lint.yaml) |
| [JSON](https://en.wikipedia.org/wiki/JSON) | JavaScript Object Notation - text-based data file written like a dictionary in code with braces, key-value pairs, lists, often used for data interchange between web services eg. `{ "name": "Maya", "hobbies": ["coding", "music"] }`          |
| [XML](https://en.wikipedia.org/wiki/XML)   | Extensible Markup Language - text-based data file with a start \<tag\> and end \</tag\> (with a slash) surrounding each field eg. `<name>Maya</name>`, older format used for data interchange in older web services                             |
