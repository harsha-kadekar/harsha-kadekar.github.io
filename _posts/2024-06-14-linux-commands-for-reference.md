---
category: Technical
date: 2024-06-14
layout: post
title: Linux commands for Reference
updated: 2024-06-18
---

In this post, I want to capture the most used linux commands by me as well as some rare ones I did use, so that I can refer these commands whenever I need it.

- [To know which directory we are in](#To know which directory we are in)
- [To go inside a directory](#To go inside a directory)
- [To Print the contents of file to StdOut](#To Print the contents of file to StdOut)
- [To Print the details of the file and folder](#To Print the details of the file and folder)
- [To Copy Files and Folders](#To Copy Files and Folders)
- [To move files and folders](#To move files and folders)
- [To create an empty file](#To create an empty file)
- [To create a directory](#To create a directory)
- [To delete files and folders](#To delete files and folders)
- [To print messages to stdout](#To_print_messages_to_stdout)

### To know which directory we are in

`pwd` - To know current working directory

```shell
➜  ObsidianToGithubPages git:(main) pwd
/home/harsha/workspace/ObsidianToGithubPages
```

### To go inside a directory
`cd` - Usually when you log in, you will be in the home directory. From there you can use `cd` i.e. change directory to go to different directory

```shell
➜  workspace cd ObsidianToGithubPages
➜  ObsidianToGithubPages git:(main)

➜  ~ cd /home/harsha/workspace/ObsidianToGithubPages
➜  ObsidianToGithubPages git:(main)
```

There are special characters which are shorthand to indicate a directory
- To go to parent directory - `cd ..`
- To go to home directory - `cd ~` or `cd` or `cd ~harsha`


### To Print the contents of file to StdOut
`cat file1` - This is used to print the contents of file to stdout. It is actually used to concatenate 2 or more files. Example `cat file1, file2, file3`

```shell
➜ ~ cat testfile.txt
this is atest
new file
```

In-order to print it in reverse order use `tac file1`. Example `tac file1, file2, file3`

```shell
➜  ~ tac testfile.txt
new file
this is atest
```

### To Print the details of the file and folder

`ls` is the command to list the details of a file or a folder

```shell
➜  ObsidianToGithubPages git:(main) ls
LICENSE  README.md  converter_config.yaml  obsidian_to_githubpages.py

➜  ObsidianToGithubPages git:(main) ls obsidian_to_githubpages.py
obsidian_to_githubpages.py
```

We can use `ls` with various attributes
- `l` - for long listing giving more information
- `a` - include hidden files and folders
- `h` - the file size details making more human readable instead of just numbers

```shell
➜  ObsidianToGithubPages git:(main) ls -lah
total 32K
drwxrwxr-x  3 harsha harsha 4.0K Feb 11 10:02 .
drwxrwxr-x 19 harsha harsha 4.0K Mar  6 21:21 ..
drwxrwxr-x  8 harsha harsha 4.0K Feb 11 10:06 .git
-rw-rw-r--  1 harsha harsha   22 Feb 10 15:29 .gitignore
-rw-rw-r--  1 harsha harsha 1.2K Feb 10 15:29 LICENSE
-rw-rw-r--  1 harsha harsha  971 Feb 10 15:38 README.md
-rw-rw-r--  1 harsha harsha  398 Jun 14 21:02 converter_config.yaml
-rwxrwxr-x  1 harsha harsha 2.7K Feb 11 10:02 obsidian_to_githubpages.py

➜  ObsidianToGithubPages git:(main) ls -lah obsidian_to_githubpages.py
-rwxrwxr-x 1 harsha harsha 2.7K Feb 11 10:02 obsidian_to_githubpages.py

➜  workspace ls -lah ObsidianToGithubPages
total 32K
drwxrwxr-x  3 harsha harsha 4.0K Feb 11 10:02 .
drwxrwxr-x 19 harsha harsha 4.0K Mar  6 21:21 ..
drwxrwxr-x  8 harsha harsha 4.0K Feb 11 10:06 .git
-rw-rw-r--  1 harsha harsha   22 Feb 10 15:29 .gitignore
-rw-rw-r--  1 harsha harsha 1.2K Feb 10 15:29 LICENSE
-rw-rw-r--  1 harsha harsha  971 Feb 10 15:38 README.md
-rw-rw-r--  1 harsha harsha  398 Jun 14 21:02 converter_config.yaml
-rwxrwxr-x  1 harsha harsha 2.7K Feb 11 10:02 obsidian_to_githubpages.py
```

### To Copy Files and Folders
To copy file1 to file2 use `cp file1 file2`

```shell
➜  dir1 ls
testfile.txt
➜  dir1 cat testfile.txt
This is a test file
➜  dir1 cp testfile.txt testcopiedfile.txt
➜  dir1 ls
testcopiedfile.txt  testfile.txt
➜  dir1 cat testcopiedfile.txt
This is a test file
```

To copy multiple files to a folder - `cp file1 file2 file3 dir`

```shell
➜  dir1 ls
testcopiedfile.txt  testfile.txt  testfiledir
➜  dir1 ls testfiledir
➜  dir1 cp testfile.txt testcopiedfile.txt testfiledir
➜  dir1 ls testfiledir
testcopiedfile.txt  testfile.txt
➜  dir1
```

To copy directory1 to directory2 we need to use `-r` attribute `cp -r dir1 dir2`

```shell
➜  Playground ls
dir1  dir2
➜  Playground ls dir1
testcopiedfile.txt  testfile.txt  testfiledir
➜  Playground ls dir2
➜  Playground cp -r dir1 dir2
➜  Playground ls dir2
dir1
➜  Playground ls dir2/dir1
testcopiedfile.txt  testfile.txt  testfiledir
```

To copy the contents of directory1 to directory2 instead of directory1 itself use `cp -r dir1/* dir2`

```shell
➜  Playground ls
dir1  dir2
➜  Playground ls dir2
➜  Playground ls dir1
testcopiedfile.txt  testfile.txt  testfiledir
➜  Playground cp -r dir1/* dir2
➜  Playground ls dir2
testcopiedfile.txt  testfile.txt  testfiledir
➜  Playground
```

### To move files and folders
Instead of copy, we need to move the file from one location to another, we can use `mv`  command. Example `mv file1 file2`. In its simple term it is renaming the file1 to file2

```shell
➜  dir1 ls
testfile.txt
➜  dir1 mv testfile.txt newpathtestfile.txt
➜  dir1 ls
newpathtestfile.txt
➜  dir1
```

To move the files from one directory to another - `mv file1 file2 targetdirectory`

```shell
➜  dir1 ls
testdirectory  testfile1.txt  testfile2.txt
➜  dir1 mv testfile1.txt testfile2.txt testdirectory
➜  dir1 ls
testdirectory
➜  dir1 ls testdirectory
testfile1.txt  testfile2.txt
➜  dir1
```

We can also move a directory into another directory

```shell
➜  dir1 ls
anothertestdir  testdirectory
➜  dir1 ls anothertestdir
➜  dir1 ls testdirectory
testfile1.txt  testfile2.txt
➜  dir1 mv testdirectory anothertestdir
➜  dir1 ls
anothertestdir
➜  dir1 ls anothertestdir
testdirectory
➜  dir1 ls anothertestdir/testdirectory
testfile1.txt  testfile2.txt
➜  dir1
```

### To create an empty file
We can use `touch` to create an empty file. If the file already exists, it will just update the last modification time of the file.

```shell
➜  testdirectory ls
testfile1.txt  testfile2.txt
➜  testdirectory touch anotherfile.txt
➜  testdirectory ls
anotherfile.txt  testfile1.txt  testfile2.txt
➜  testdirectory ls -lah
total 16K
drwxrwxr-x 2 harsha harsha 4.0K Jun 18 17:58 .
drwxrwxr-x 3 harsha harsha 4.0K Jun 18 17:56 ..
-rw-rw-r-- 1 harsha harsha    0 Jun 18 17:58 anotherfile.txt
-rw-rw-r-- 1 harsha harsha   20 Jun 17 22:42 testfile1.txt
-rw-rw-r-- 1 harsha harsha   20 Jun 17 22:58 testfile2.txt
➜  testdirectory touch testfile1.txt
➜  testdirectory ls -lah
total 16K
drwxrwxr-x 2 harsha harsha 4.0K Jun 18 17:58 .
drwxrwxr-x 3 harsha harsha 4.0K Jun 18 17:56 ..
-rw-rw-r-- 1 harsha harsha    0 Jun 18 17:58 anotherfile.txt
-rw-rw-r-- 1 harsha harsha   20 Jun 18 17:59 testfile1.txt
-rw-rw-r-- 1 harsha harsha   20 Jun 17 22:58 testfile2.txt
➜  testdirectory
```

### To create a directory

use `mkdir` to create the directory

```shell
➜  dir1 ls
➜  dir1 mkdir testdirectory
➜  dir1 ls -lah
total 12K
drwxrwxr-x 3 harsha harsha 4.0K Jun 18 20:17 .
drwxrwxr-x 4 harsha harsha 4.0K Jun 17 22:48 ..
drwxrwxr-x 2 harsha harsha 4.0K Jun 18 20:17 testdirectory
➜  dir1
```

### To delete files and folders
To delete files use `rm` command. Example `rm file1 file2 file3`

```shell
➜  testdirectory ls
anotherfile.txt  testfile1.txt  testfile2.txt
➜  testdirectory rm anotherfile.txt testfile1.txt testfile2.txt
➜  testdirectory ls
➜  testdirectory
```

If we want confirmation of the file delete before it is done, we can use `-i` attribute

```shell
➜  testdirectory ls
testfile1.txt  testfile2.txt  testfile3.txt
➜  testdirectory rm -i testfile1.txt testfile2.txt testfile3.txt
rm: remove regular empty file 'testfile1.txt'? y
rm: remove regular empty file 'testfile2.txt'? y
rm: remove regular empty file 'testfile3.txt'? n
➜  testdirectory ls
testfile3.txt
```

If we want to delete a directory then we need to use `-r` attribute

```shell
➜  anothertestdir ls -lah
total 12K
drwxrwxr-x 3 harsha harsha 4.0K Jun 18 18:04 .
drwxrwxr-x 3 harsha harsha 4.0K Jun 18 17:56 ..
drwxrwxr-x 2 harsha harsha 4.0K Jun 18 18:05 testdirectory
➜  anothertestdir rm testdirectory
rm: cannot remove 'testdirectory': Is a directory
➜  anothertestdir rm -r testdirectory
➜  anothertestdir ls
➜  anothertestdir
```

Sometimes, we need to remove the files and directories which are large in number or via a script and we do not want any interactive questions while deleting. To force delete everything in a file or folder use `-f` flag.

```shell
➜  anothertestdir ls
testdirectory
➜  anothertestdir rm -rf testdirectory
➜  anothertestdir ls
➜  anothertestdir
```

### To_print_messages_to_stdout
To print messages to the screen use `echo`

```shell
➜  dir1 echo "How are you?"
How are you?
➜  dir1 echo How are you
How are you
➜  dir1
```