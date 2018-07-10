# Introduction
In this branch i'll include some commands really importants in Linux, SSH, Vi or Vim and Github.

## Linux
Linux is an operating system. An operating system is software that manages all of the hardware resources associated with your desktop or laptop. To put it simply – the operating system manages the communication between your software and your hardware. 

#### Important commands:

- `pwd`, shows the folder as you stay. E. g. `/home/user/Desktop`




## SSH
The SSH (Secure Shell) is a network protocol that provides administrators with a secure way to access a remote computer. SSH also refers to the suite of utilities that implement the protocol. Secure Shell provides strong authentication and secure encrypted data communications between two computers connecting over an insecure network such as the Internet. SSH is widely used by network administrators for managing systems and applications remotely, allowing them to log in to another computer over a network, execute commands and move files from one computer to another.

To access the SPRACE Cluster use:

`ssh -XY user@access.sprace.org.br`

To access the LXplus use:

`ssh -XY user@lxplus.cern.ch`

The `-XY` enables the graphical interface (X11 forwarding).


## Vi or Vim
Vi or Vim is a screen-oriented text editor originally created for the Unix operating system.

#### Difference between Vi and Vim:

- Vim has been ported to a much wider range of OS's than vi;
- Vim includes support (syntax highlighting, code folding, etc) for several popular programming languages (C/C++, Python, Perl, shell, etc);
- Vim can be used to edit files using network protocols like SSH and HTTP;
- Vim allows the screen to be split for editing multiple files;
- Vim can edit files inside a compressed archive (gzip, zip, tar, etc);
- Vim includes a built in diff for comparing files (vimdiff);
- Vim includes support for plugins, and finer control over config and startup files;
- Vim can be scripted with vimscript, or with an external scripting language (e.g. python, perl, shell);

#### Important commands:

- `vi filename` edit filename;
- `vi -r filename` recover filename that was being edited when system crashed;
- `:x or :wq` save & quit;
- `:q` quit vi;
- `:q!`quit vi without save (force quit);
- `:w` save file;
- `u` undo whatever you did;

More informations and other commands [here](https://www.cs.colostate.edu/helpdocs/vi.html)

## GitHub
