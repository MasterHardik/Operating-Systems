# Bash Bang Command

Ever find yourself forgetting to use `sudo`, battling typos, or wishing for shortcuts to repeat commands? If this sounds familiar, Bash bang (`!`) commands are your new best friend. They offer powerful shortcuts for repeating commands, fixing errors, and more. Let’s dive into these handy tricks!

## Command Repeat Basics

Bash keeps a history of your commands, which is stored in the `~/.bash_history` file. By default, it holds the last 500 commands. The `!` (bang) commands let you access this history to quickly repeat or modify past commands.

### Examples of Bash Bang Commands

#### Repeat the Last Command Matching a String

Use `!<string>` to repeat the most recent command starting with `<string>`:

```bash
$ ls

dir  dir1  dir2  file  file1  file2  hello.txt

$ !l
ls 
dir  dir1  dir2  file  file1  file2  hello.txt

$ !ls
ls 
dir  dir1  dir2  file  file1  file2  hello.txt
```

**Repeat the Last Command Matching Anywhere in the String**
Use `!?<string>` to repeat the most recent command containing `<string>`:

```bash
$ cat hello.txt 
Hello world ..!

$ !?hello.txt
cat hello.txt 
Hello world ..!
```

**Repeat the nth Command from Your History**

To repeat a command from the history by its position, use `!<number>`:

```bash
!10
```

**Repeat the nth Command from the End**
To repeat a command from the end of the history, use `!-<number>`:

```bash
!-10
```

**Repeat the Last Command**
`!!` repeats the last command. It's especially useful when you need to prefix a command with `sudo` or pipe its output:

```bash
$ yum update
Loaded plugins: priorities, update-motd, upgrade-helper
You need to be root to perform this command.

$ sudo !!
sudo yum update
Loaded plugins: priorities, update-motd, upgrade-helper

$ ls
dir  dir1  dir2  file  file1  file2  hello.txt

$ !! | grep file
ls | grep file
file
file1
file2
```
**Repeat and Substitute a String**

To fix typos or adjust long commands without retyping, use `!!:s^<old>^<new>`:

```bash
$ ls /etc/httpd/conf.d
autoindex.conf  notrace.conf  php.conf  php-conf.7.2  README  userdir.conf  welcome.conf

$ !!:s^conf.d^conf
ls /etc/httpd/conf
httpd.conf  magic
```

Alternatively, use `!<string>:s^<old>^<new>` for non-recent commands:

```bash
$ !l:s^conf^conf.d
ls /etc/httpd/conf.d
autoindex.conf  notrace.conf  php.conf  php-conf.7.2  README  userdir.conf  welcome.conf
```
**Repeat Command Arguments**
Reuse arguments from the previous command with `!:n` or `!!:$`:

```bash
~/project $ ls -a -l 
# ... list output ...

~/project $ ls !:1
ls -a
# ... list output ...

~/project $ mkdir dir3
~/project $ cd !$
cd dir3
```
You can also apply this to commands that are not the most recent:

```bash
$ mkdir -p hello/test1/test2
$ ls !mkdir:$
ls hello/test1/test2
```
**Print Commands Without Executing**
To display a command from history without running it, use !:p:

```bash
~/project $ !:p
cat hello.txt 

$ !mkdir:p
mkdir -p hello/test1/test2

$ !su:p
sudo yum check-update
```

**Recall Commands with Reverse-i-Search**
For a more interactive search, use reverse-i-search with `CTRL+R`:

```plaintext
(reverse-i-search)`<search string>`: <output>
(reverse-i-search)`yu': sudo yum check-update
(reverse-i-search)`cd': cd /etc
```

## Conclusion
Mastering Bash bang commands can significantly streamline your workflow and help you quickly correct mistakes. For more details, explore Bash’s man page using $ `man bash`.