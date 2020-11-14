# 	Command Line

The below is using GitBash

## Commands

- `pwd` outputs the name of the current working directory.
- `ls` lists all files and directories in the working directory.
- `cd` switches you into the directory you specify.
- `mkdir` creates a new directory in the working directory.
- `touch` creates a new file inside the working directory.
- The `cp` command copies files or directories. 
- The `mv` command moves files.
- The `rm` command deletes files and directories.

## Options

The '-a' is known as an option. These can be used like so `ls -a`. Here are some options below:

- `-a` - lists all contents, including hidden files and directories
- `-l` - lists all contents of a directory in long format
- `-t` - order files and directories by the time they were last modified.

The `-l` option lists files and directories as a table. Here there are four rows, with seven columns separated by spaces. Here’s what each column means:

1. Access rights. These are actions that are permitted on a file or directory.
2. Number of hard links. This number counts the number of child directories and files. This number includes the parent directory link (`..`) and current directory link (`.`).
3. The username of the file’s owner. Here the username is `cc`.
4. The name of the group that owns the file. Here the group name is `eng`.
5. The size of the file in bytes.
6. The date & time that the file was last modified.
7. The name of the file or directory.

The `-r` is an option that modifies the behavior of the `rm` command. The `-r` stands for “recursive,” and it’s used to delete a directory and all of its child directories.

## Copy + Move

To copy we use the command `cp`. This can be used to copy multiple files or individual files. This is more of a duplication than a "copy" as we know it today.

In addition to using filenames as arguments, we can use special characters like `*` to select groups of files. These special characters are called *wildcards*. The `*` selects all files in the working directory.

If you wanted to select all the files that start with m and ending in .txt for instance would look like `m*.txt`.

To Move files it is done similarly with the command `mv`.

Using these commands look like this `mv(OR cp) file.txt destination/`. This can be done to multiple files at one time.

To rename a file, use `mv` with the old file as the first argument and the new file as the second argument.



## Shorthand

- Options modify the behavior of commands:
  - `ls -a` lists all contents of a directory, including hidden files and directories
  - `ls -l` lists all contents in long format
  - `ls -t` orders files and directories by the time they were last modified
  - Multiple options can be used together, like `ls -alt`
- From the command line, you can also copy, move, and remove files and directories:
  - `cp` copies files
  - `mv` moves and renames files
  - `rm` removes files
  - `rm -r` removes directories
- Wildcards are useful for selecting groups of files and directories