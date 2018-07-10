# Introduction
In this branch i included some commands importants in Linux, SSH, Vi or Vim and Github.

## Linux
Linux is an operating system. An operating system is software that manages all of the hardware resources associated with your desktop or laptop. To put it simply – the operating system manages the communication between your software and your hardware. 

#### Important commands:
- `ẁhoami`, show the user name;
- `pwd`, shows the folder as you stay. E. g. `/home/user/Desktop`;
- `clear or CTRL+L`, clear the terminal;
- `exit or CTRL+D`, quit the terminal;
- `cd`, change directory;
- `ls`, list the contents;
- `mkdir`, create a folder;
- `rm`, delete a file;
- `rm -r or rmdir`, delete a folder;
- `cat`,  displaying the contents of a file;
- `find -iname "file"`, search the file in the computer;
- `grep`, searches files for a given character string;
- `apt-get`, install linux packages/programs;
- `df -h`, displays information about the total disk space;
- `du -hs`, show the size of the file;
- `free`,  displays information about RAM and swap space usage;
- `diff`, compares the contents of any two files;
- `chmod`, changes the access permissions;
- `fs quota`, show quota in the machine;

More informations and other commands click [here](https://www-uxsup.csx.cam.ac.uk/pub/doc/suse/suse9.0/userguide-9.0/ch24s04.html) or [here-2](https://searchdatacenter.techtarget.com/tutorial/77-Linux-commands-and-utilities-youll-actually-use).

## SSH
The SSH (Secure Shell) is a network protocol that provides administrators with a secure way to access a remote computer. SSH also refers to the suite of utilities that implement the protocol. Secure Shell provides strong authentication and secure encrypted data communications between two computers connecting over an insecure network such as the Internet. SSH is widely used by network administrators for managing systems and applications remotely, allowing them to log in to another computer over a network, execute commands and move files from one computer to another.

To access the SPRACE Cluster use:

`ssh -XY user@access.sprace.org.br`

To access the LXplus use:

`ssh -XY user@lxplus.cern.ch`

The `-XY` enables the graphical interface (X11 forwarding).

If you like to work in your own computer you can download files or folders using `scp`. E. g. 
##### Send files to SPRACE Machine
`scp file.txt user@access.sprace.org.br:/home/user/`
##### Send folders to SPRACE Machine
`scp -r folder/ user@access.sprace.org.br:/home/user/`
##### Copy files from SPRACE Machine
`scp user@access.sprace.org.br:/home/user/file.txt .`
##### Copy folders from SPRACE Machine
`scp -r user@access.sprace.org.br:/home/user/folder/ .`

Sometimes we need to copy files for the grid structure, to do that we need to use srm (to use that the certificate is requested).
##### Show the list of files
`srmls srm://...`

##### Copy files
`srmcp srm://...`




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
- `i` insert text;
- `dd` delete the current line;
- `dNd` delete N lines above (N is a number);
- `/text` search for text in the file;
- `n` move to next occurrence of search text;


More informations and other commands click [here](https://www.cs.colostate.edu/helpdocs/vi.html).

## GitHub
GitHub is Git’s cloud-based publishing tool and hosting platform. It also has a desktop application for locally storing projects. Git is used by programmers, developers, and designers to store projects and keep track of changes to their files.

#### Set up your .gitconfig
`git config --global user.name [Name]`

`git config --global user.email [Email]`

`git config --global user.github [Account]`

`cat ~/.gitconfig`

#### Collaboration on GitHub

Clone the github folder

`git clone https://github.com/denerslemos/Standard-Model.git`

`cd Standard-Model`

`ls -a`

`ls .git`

`git branch -a`

#### Adding remotes and synchronizing

Look at your remote(s): 

`git remote`

`git remote -v`

The "origin" remote is set by default when you use `git clone`. Because your repository is a fork, you also want to have a remote that points to the original repo, traditionally called "upstream". 

`git remote add upstream https://github.com/denerslemos/Standard-Model.git`

`git remote -v`

Check for changes in upstream

`git pull upstream master`

Push your local master branch back to your remote fork: 

`git pull origin master`

`git remote`

#### Making edits and committing 

-> Ex. 1) Edit the table SM.md to add a new particle. The new particle is called a Giton, with symbol G, spin 2, charge 0, and mass 750 GeV.

-> Ex. 2) Create a file quarks.md with the name of the 6 quarks.

When collaborating with other developers on GitHub, it is best to make a separate topic branch to store any changes you want to submit to the main repo. This way, you can keep the default branch in your fork synchronized with upstream, and then make another topic branch when you want to make more changes.

Make a topic branch: 

`git checkout -b MyBranch`

Once you have made changes in your working area, you have to stage the changes and then commit them. First, you can inspect the status of your working area.

Try the following commands:

`git status`

`git status -s`

`git diff`

Now stage your change, and check the status:

`git add SM.md`

`git add quarks.md`

`git status -s`

Commit your change:

`git commit -m "add Giton to standard model"`

Push your topic branch, which now includes the new commit you just made, to origin: 

`git push origin MyBranch`

#### Making a pull request 

Now that you have made your change, you can submit it for inclusion in the central repository.

When you open the page to send a pull request on GitHub, you will notice that you can send a pull request to any fork of the repo (and any branch). 

![Screenshot](https://github.com/denerslemos/CMSSW_SPRACE_2018/tree/Linux_SSH_Git/0.png)
