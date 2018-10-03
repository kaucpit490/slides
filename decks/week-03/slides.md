### The UNIX/Linux Philosophy

> Do One Thing and Do It Well


> "This is the Unix philosophy: Write programs that do one thing and do it well. Write programs to work together. Write programs to handle text streams, because that is a universal interface."

Doug McIlroy


### Shell Types
- A shell is a user interface for accessing the operating system.
- Shells are either command-line interface (CLI) or graphical user interface (GUI).
- Text (CLI) shell types:
  - __sh__ the basic shell in UNIX-related environments.
  - __bash__ or Bourne Again shell: the standard shell for common users.
  - __zsh__ An extended Bourne shell with signifcant improvements.


### Common shell programs
- _ls_: lists the content of a directory
- _grep_: searches text
- _wc_: counts lines, words, and characters
- _sort_: sorts lines
- _uniq_: prints unique lines
- _head_: reads the beginning of a file
- _tail_: reads the end of a file


### Communication Channels
- Every process has at least three communication channels:
  - Standard Input (stdin)
  - Standard Output (stdout)
  - Standard Error (stderr)
- In most interactive text shells, stdin reads from keyboard, stdout and stderr writes outputs to the screen.
- These communication channels can be redirected into a file or piped into the stdin of another program or command.


### Redirection (I)
- Communication channels can be redirected into a file
- The symbols `<`, `>`, and `>>` are used to redirect a program's input or output to or from a file. 
  - _>_ Redirects stdout. It creates a file or replaces its content if it exists.
  - _>>_ Redirects stdout. It appends to the existing file's content.

```bash
$ ls /home > users.txt ## stdout to a file (create or replace)
$ ls /home >> users.txt ## stdout to a file (create or append)
```


### Redirection (II)
<!-- .slide: style="text-align: left;"> --> 
- The symbol _2>_ is used to redirect stderr into a file.

```bash
$ find /etc -name network 2> error.log
```

- Redirect stdout and stderr into two different files.

```bash
$ find /etc -name network > out.txt 2> error.log
```
  
  - _>_ sends stdout to a file named out.txt
  - _2>_ sends stderr to a file named error.log


### Pipes
- Pipes are used to connect the stdout of one command into the stdin of another command.
- Pipes use the pipe symbol _|_ 
  - piping into _wc_ tool, which counts how many lines, words, and characters.

  ```bash
$ ls /etc | wc -l
  ```
  - Counting how many bash users by using the search tool _grep_ and piping into _wc_.

  ```bash
$ grep bash /etc/passwd | wc -l
  ```


### Scripting and Automation
- It's important for a sysadmin to incorporate automation into your daily work.
- Automation is done through writing scripts.
- Whenever you encounter a repetitive task, automate it in a script.
- Examples:
  - Storing backups in two different data centers.
  - Checking if an application or a process has crashed accidently.
  - Creating, configuring, and deploying a cloud service in one command.


### From commands to script
- A typical shell script contains a list of commands
- These commands are exactly the same commands you run in a bash shell
- The script may also include control flow statements, loops, and functions.



### Bash Script Examples (I)
<!-- .slide: style="text-align: left;"> --> 

1) Hello World Example

_script.sh_
```bash
#!/bin/bash
foo="HELLO WORLD!!!"
echo $foo
```
_Running/Execution:_

```bash
# make it executable
chmod u+x script.sh
# run it
./script.sh 
# or
bash ./script.sh
```


### Bash Script Examples (II)
<!-- .slide: style="text-align: left;"> --> 
2) Creating an archive (i.e., compressing a directory)
```bash
#!/bin/bash
target="/home/khalid/backup/archive.tar"
tar -cvf $target /home/khalid
```

3) Passing arguments to the bash script

_archive-maker.sh_
```bash
#!/bin/bash
echo "creating an archive file using tar -cvf $0 $1"
tar -cvf $0 $1
```
_Run it:_
```bash
bash ./archive-maker.sh output.tar /path/to/dir
```


### Reading Input
```bash
$ echo -n "Proceed? [y/n]: "
$ read ans
$ echo $ans

```


### Loops
- The _for ..in_ construct is used to perform loops/iteration.
- Example: copy shell script files (*.sh files) into a directory called _bin_.

```bash
srcDir=/home/khalid
targetDir=/home/khalid/bin
mkdir $targetDir
for scriptFile in $srcDir/*.sh; do
  echo "Moving $scriptFile into $targetDir"
  mv $scriptFile $targetDir
done
```


### Exercise (in-class activity)
- Modify the previous bash script to accept command line arguments instead of hard coded source and target path name values. Example:

```bash
$ bash move-sh-files.sh ~/ ~/bin
```


### Control Flow Statements

```bash
x=5
if [ $x -eq 5 ]
  then
  echo "$x equals 5"
elif [ $x -lt 5 ]
  then
  echo "$x is less than 5"
elif [ $x -gt 5 ]
  then
  echo "$x is greater than 5"
fi
```


### Functions (I)

- Declaring and calling bash functions

```bash
#!/bin/bash 
quit() {
  exit
}
hello() {
  echo Hello!
}
hello
quit
echo "End!"
```


### Functions (II)
- Passing parameters to a Bash function

```bash
#!/bin/bash 
my_function() {
  echo "In my_function"
  echo $1 $2 $3
  echo "End!"
}
my_function "Learn" "Bash" "Functions"
```


### Environment Variables (I)
- Bash uses certain global variables or environment variables. 
- Examples:
  - $PATH
    - Contains a colon-separated list of directories in which the shell looks for commands.
  - $HOME
    - Contains the path of the current user's home directory.


### Environment Variables (II)
- When you type a command you installed recently by its name and get an error message that says: "X: command not found", that means it's not available in your $PATH variable.
- You need to add it to your _$PATH_ environment variable.


### Environment Variables (III)
- To add a command to your $PATH variable, you need to edit the `~/.bash_profile` file.
  - Append the path of your tool into the PATH variable
```bash
PATH=$PATH:$HOME/.local/bin:$HOME/bin:/path/to/mytool
export $PATH
```
- Save the file and login again or run the command: 
```bash
source ~/.bash_profile
```


### Other Scripting Languages
- There're many general-purpose scripting languages that offer easy to read syntax and have an extensive set of standard libraries.
- Examples include, Perl, Python, and Ruby.
- Python is a widely used scripting language for system adminstration scripting.
- In addition to Bash scripting, it's expected for a system administrator to be familiar with a language like Python.
