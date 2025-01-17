# Shell and Terminals

# Some Basic Commands

Expr

```bash
expr 123456 + 7890 # Results in 131346
```

Variables

```bash
bankname = "WorldBanc" # Creates a variable called bankname
echo $bankname # Prints out the value stored in the bankname variable
```

History

```bash
history # Prints out the last 10 commands send to the terminal
```

# Terminal Alternatives

- **Editor/IDE built-in terminals -** Most text editors for developers have a built-in terminal. VS Code is a popular text editor that also has a built-in terminal
- **iTerm2** - [iTerm2](https://iterm2.com/) is a popular terminal for Mac OS. It's a bit more powerful than the default terminal, and it has some nice features like split panes
- **Alacritty -** [Alacritty](https://github.com/alacritty/alacritty) is a popular terminal for Linux with a focus on flexibility and extensive configuration. GPU-accelerated, it's great if you're doing a lot of heavy lifting in the terminal
- **Windows Terminal -** Microsoft's substitute for the Linux terminal. Use the "cmd.exe" program settings to change the default terminal. Be sure to start WSL whenever you open a new terminal window.

# Basic File Reading

```bash
# Print the contents of a file to the terminal
cat file1.txt
```

```bash
head -n 10 file1.txt # Shows the top 10 lines of a file
tail -n 10 file1.txt # Shows the bottom 10 lines of a file
```

```bash

less file1.csv # less is more (the less command, replaces the more command)
less -N file1.csv # includes line numbers
```

Notice that when you execute less, you are now in an interactive mode and you've lost your shell prompt! That's because `less` has taken over your terminal window.

- Press “enter” a few times to scroll down line by line
- Press q to quit
- Press “spacebar” to scroll page by page
- Press “b” to go back

# Basic File Creation

The [touch command](https://man7.org/linux/man-pages/man1/touch.1.html) is designed to update the access and modification timestamps of a file. By default, if the specified file does not exist, `touch` will create an empty file with the given filename. Because of this, you’ll often see this command used to quickly create new files.

```bash
touch new_file.txt # Creates a single file
touch some_file.txt some_other_file.txt # Creates multiple files at same time
```

# Grep

The [grep command](https://www.digitalocean.com/community/tutorials/grep-command-in-linux-unix) allows you to search for text in files. It has a *ton* of capability, and you’ll usually only be scratching the surface of its true power.

```bash
grep "hello" hello.txt # Searches the hello.txt file for any lines with the word "hello"
grep "hello" hello.txt hello2.txt # Searches two files

grep -r "hello" <directory> # Search an entire directory including all sub-directories

grep -r "CRITICAL" . # The . is a special alias for the current directory
```

# Permissions

The permissions of an individual file or directory are visually represented as a 10-character string:

```bash
drwxrwxrwx
```

The first character just tells you whether you're looking at a file or a directory:

- `-`: Regular file (e.g. `-rwxrwxrwx`)
- `d`: Directory (e.g. `drwxrwxrwx`)#

The next 9 characters are broken up into 3 sets of `rwx` and represent the permissions themselves for the "owner", "group", and "others", in order. Each group of 3 represents the permissions for reading, writing, and executing, in order. So, for example:

- **Owner -** The first 3 characters are "owner" permissions. The "owner" is usually just the user who created the file or directory, but it can be manually changed.
    - `rwx`: All permissions
    - `rw-`: Read and write, but not execute
    - `r-x`: Read and execute, but not write
- **Group -** The next 3 characters are "group" permissions. Unix-like systems support groups of users and a file or directory can be assigned to a single group.
    - `rwx`: All permissions
    - `rw-`: Read and write, but not execute
    - `r-x`: Read and execute, but not write
- **Other -** The last 3 characters are "others" permissions. This is everyone else
    - `rwx`: All permissions
    - `rw-`: Read and write, but not execute
    - `r-x`: Read and execute, but not write

# Chmod

Lets you change the permissions of a file or directory. It's short for "change mode" 

```bash
chmod -R u=rwx,g=,o= DIRECTORY
```

In the command above, `u` means "user" (aka "owner"), `g` means "group", and `o` means "others". The `=` means "set the permissions to the following", and the `rwx` means "read, write and execute". The `g=` and `o=` mean "set group and other permissions to nothing". The `-R` means "recursively", which means "do this to all of the contents of the directory as well".

```bash
chmod -x genids.sh
chmod +x FILENAME
```

The `chmod` command has a convenient `-x` flag that will simply remove the executable permission from the file.

# Root User

The "root" user is a superuser. It has access to everything on the system and can do anything. When you use the `sudo` command, you're running as the root user

The `sudo` keyword is convenient because it quickly gives you elevated permissions to run a single command.

# Chown

The `chown` command, which stands for "change owner", allows you to change the owner of a file or directory, and it requires root privileges.

```bash
sudo chown -R root contacts
```

- `sudo` - Run as the root user
- `chown` - Command to change the owner
- `R` - "Recursive", meaning also apply the changes to everything inside the directory
- `root` - The name of the new owner
- `contacts` - The directory to change the owner of

# Compiled vs Interpreted

There are two type of program:

- Compiled programs
- Interpreted programs

## Compiled

A compiled program is a program that has been converted from human-readable source code into machine code (binary). [Machine code](https://en.wikipedia.org/wiki/Machine_code) is a set of instructions that a computer can execute directly: your computer's CPU is hardware that's been designed to execute machine code.

Programming languages like Go, C, and Rust are compiled languages that produce compiled programs.

## Interpreted

An interpreted program is a program that is executed by *another* program. The program that executes the interpreted program is called an [interpreter](https://en.wikipedia.org/wiki/Interpreter_%28computing%29). The interpreter reads the source code of the interpreted program and executes it.

Programming languages like Python, Ruby, and JavaScript, are interpreted languages. Your computer needs to have an interpreter installed to run programs written in those languages.

# Shebang

A ["shebang"](https://en.wikipedia.org/wiki/Shebang_(Unix)) is a special line at the top of a script that tells your shell which program to use to execute the file.

The format of a shebang is:

```bash
#! interpreter [optional-arg]
```

For example, if your script is a Python script and you want to use Python 3, your shebang might look like this:

```python
#!/usr/bin/python3
```

This tells the system to use Python 3 located at `/usr/bin/python3` to run the script.

# **Bourne Shell**

For your main shell REPL, as we talked about before:

- If you're using Ubuntu on WSL, you're probably running a [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) shell.
- If you're using macOS, you're probably running a [Zsh](https://en.wikipedia.org/wiki/Z_shell) shell.
- If you're running a raw Linux installation, I pray you already know what you're using.

To get hand-wavy about it, I want to explain the difference between the 3 shells you're likely to encounter:

- `sh` - The Bourne shell. This is the original Unix shell and is [POSIX-compliant](https://en.wikipedia.org/wiki/POSIX). It's very basic and doesn't have many quality-of-life features.
- `bash` - The Bourne Again shell. This is the most popular shell on Linux. It builds on `sh`, but also has a lot of extra features.
- `zsh` - The Z shell. This is the most popular shell on macOS. Like `bash`, it does what `sh` can do, but also has a lot of extra features.

Both `zsh` and `bash` are "sh-compatible" shells, meaning they can run `.sh` scripts, but they also have extra features that generally make them more pleasant to use. 

# **Shell Configuration**

Bash and Zsh both have [configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files) that run automatically each time you start a new shell session. These files are used to set up your shell environment. They can be used to set up aliases, functions, and environment variables.

These files are located in your home directory (`~`) and are hidden by default. The `ls` command has a `-a` flag that will show hidden files:

```python
ls -a ~
```

- If you're using Bash, `.bashrc` is probably the file you want to edit.
- If you're using Zsh, `.zshrc` is probably the file you want to edit or create if it doesn't yet exist.

# **Environment Variables**

There is another type of variable called [environment variables](https://en.wikipedia.org/wiki/Environment_variable). They are available to *all* programs that you run in your shell.

You can view all of the environment variables that are currently set in your shell with the command `env`.

If you want to set a variable in your shell, you can use the `export` command:

# PATH

There are environment variables that are sort of "built-in" to your shell. By "built-in" I just mean that different programs and parts of your system know about them and use them. The `PATH` variable is one of those.

If it weren't for the `PATH`, you'd have to remember the filesystem path of every executable you wanted to run. Instead of just running `ls`, you'd have to run `/bin/ls` (or whatever the location of the `ls` executable is on your system). That's not very convenient.

The `PATH` variable is a list of directories that your shell will look into when you try to run a command. If you type `ls`, your shell will look in each directory listed in your `PATH` variable for an executable called `ls`. If it finds one, it will just run it. If it doesn't, it will give you an error like: "command not found".

Take a look at your current `PATH` variable:

```bash
echo $PATH
```

You should see a giant list of directories separated by colons (`:`). Each of those directories is a place where your shell will look for executables. For example, with a `PATH` like this:

```bash
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

Your shell will look for executables in the following directories:

- `/usr/local/bin`
- `/usr/bin`
- `/bin`
- `/usr/sbin`
- `/sbin`

To add a directory to your `PATH` without overwriting all of the existing directories, use the `export` command and reference the existing `PATH` variable:

```bash
export PATH="$PATH:/path/to/new"
```

To change the PATH variable completed, the most common way to do this is to add the same `export` command (above) to your shell's configuration file.

# Command Flags

The `ls` command can take a `-l` flag to show a "long" listing of files:

```bash
ls -l
```

The `ls` command can also take a `-a` flag to show "all" files, including hidden files:

```bash
ls -a
```

You can combine flags:

```bash
ls -al
```

Whether or not a command takes flags, and what those flags are, is up to the developer of the command. That said there are some common conventions:

- Single-character flags are prefixed with a single dash (.e.g `a`)
- Multi-character flags are prefixed with two dashes (e.g. `-help`)
- Sometimes the same flag can be used with a single dash or two dashes (e.g. `-h` or  `--help`)

# Piping

One of the most beautiful things about the shell is that you can [pipe](https://en.wikipedia.org/wiki/Pipeline_%28Unix%29) the output of one program into the input of another program. With this one simple concept, you can run incredibly powerful automation tasks.

The pipe operator is `|`. It's the character that looks like a vertical line. It's usually on the same key as the backslash (`\`) above the enter key. The pipe operator takes the stdout of the program on the left and "pipes" it into the stdin of the program on the right.

```bash
echo "Have you heard the tragedy of Darth Plagueis the Wise?" | wc -w
# 10
```

In the example above, the `echo` command sends "Have you heard the tragedy of Darth Plagueis the Wise?" to stdout.

However, instead of that text being sent to your terminal, the pipe operator pipes it into the `wc` (word count) command. The `wc` command counts the number of words in the input it receives. The `-w` flag tells `wc` to only count words.

This only works because the `wc` command, like most shell commands, can optionally read from stdin instead of a filepath.

# Interrupt and Kill

ometimes a program will get stuck and you'll want to stop it. Common reasons for this are:

- You made a typo in the command and it's not doing what you want
- It's trying to access the internet but you're not connected
- It's processing too much data and you don't want to wait for it to finish
- There is a bug in the program causing it to hang

In these cases, you can stop the program by pressing `ctrl + c`. This sends a "SIGINT" signal to the program, which tells it to stop.

Sometimes a program is in such a bad state (or is so malicious) that it doesn't respond to the `SIGINT`, in which case the best option is to use another shell session (new terminal window) to manually [kill](https://www.ibm.com/docs/en/aix/7.3?topic=k-kill-command) the program.

```bash
kill PID
```

`PID` stands for "process ID". Every process that's running on your machine has a unique ID. The [ps](https://www.ibm.com/docs/en/zos/3.1.0?topic=jobs-using-ps-command), "process status" command can be used to list the processes running on your machine, and their IDs:

```bash
ps aux
```

The "aux" options just mean "show all processes, including those owned by other users, and show extra information about each process".

# Unix Philosophy

The [Unix Philosophy](https://en.wikipedia.org/wiki/Unix_philosophy) is a simple set of principles that have guided the development of Unix-like operating systems for decades. It can be summarized as:

1. Write programs that do one thing and do it well.
2. Write programs to work together.
3. Write programs to handle text streams, because that is a universal interface.

# Package Managers

A package manager is a software tool that helps you install other software. Its primary functions include:

- Downloading software from official sources
- Installing software
- Updating software
- Removing software
- Managing dependencies

As a developer, you'll frequently use package managers to get access to the software you need to get your work done.

## APT (Ubuntu)

APT, or "Advanced Package Tool", is the primary package manager for Ubuntu. To be fair, you can use other package managers on Ubuntu, but APT is the default and most common.

If you're on WSL and Ubuntu, you'll be using APT. If you're on another Linux setup, I pray you already know what package manager you're using. If you're on WSL or Ubuntu, check to make sure you have APT installed by running the following command:

```bash
apt --version
```

## Brew (Mac OS)

There isn't a "default" package manager for Mac OS. The most popular (but unofficial) package manager is [Homebrew](https://brew.sh/).

If you're on Mac OS, and you don't have Homebrew installed, you can install it by running the following command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

When you type a command like `apt install neovim`, the package manager will:

1. Check to see if the package is already installed.
2. If it's not installed, it will download the package from a repository.
3. It will install the package on your computer.
4. It will install any dependencies that the package needs to run.
5. It will (hopefully) add the package to your PATH if it should be there.

Good package managers keep track of what packages you have installed, and what versions of those packages you have installed. They keep your filesystem nice and tidy, making sure you haven't installed 10 different instances of the same package or application.

For your edification, take a look at where your package manager installed `nvim` on your filesystem. The `which` command will help:

```bash
which nvim
```

## Webi

There is one more package manager (actually more of an anti-package manager) I want to introduce you to: [Webi](https://webinstall.dev/). Also known as webinstall.dev.

Webi lets you install command line tools directly from the web, with no need for a local command line tool like `apt` or `brew`. You don't need to install webi itself at all, instead, you just run a shell command that downloads and runs the tool's official installer script.