---
category: Technical
date: 2024-06-14
layout: post
title: Linux commands for Reference
updated: 2024-06-22
---

In this post, I want to capture the most used linux commands by me as well as some rare ones I did use, so that I can refer these commands whenever I need it.

The two books that has helped in learning these commands apart from linux itself are - 
- [The Linux Command Line](https://www.amazon.com/Linux-Command-Line-Complete-Introduction/dp/1593273894)
- [How Linux Works](https://www.amazon.com/How-Linux-Works-Brian-Ward/dp/1718500408)

## Table of Content
- [To know which directory we are in - pwd](#to-know-which-directory-we-are-in---pwd)
- [To go inside a directory - cd](#to-go-inside-a-directory---cd)
- [To Print the contents of file to stdout - cat](#to-print-the-contents-of-file-to-stdout---cat)
- [To Print the details of the file and folder - ls](#to-print-the-details-of-the-file-and-folder---ls)
- [To Copy Files and Folders - cp](#to-copy-files-and-folders---cp)
- [To move files and folders - mv](#to-move-files-and-folders---mv)
- [To create an empty file - touch](#to-create-an-empty-file---touch)
- [To create a directory - mkdir](#to-create-a-directory---mkdir)
- [To delete files and folders - rm](#to-delete-files-and-folders---rm)
- [To print messages to stdout - echo](#to-print-messages-to-stdout---echo)
- [To read a text file - less](#to-read-a-text-file---less)
- [To search for text in files - grep](#to-search-for-text-in-files---grep)
- [To know the difference between files - diff](#to-know the difference-between-files---diff)
- [To find a file - find](#to-find-a-file---find)


### [To know which directory we are in - pwd](to-know-which-directory-we-are-in---pwd)

`pwd` - To know current working directory

```shell
➜  ObsidianToGithubPages git:(main) pwd
/home/harsha/workspace/ObsidianToGithubPages
```

### [To go inside a directory - cd](to-go-inside-a-directory---cd)
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


### [To Print the contents of file to stdout - cat](to-print-the-contents-of-file-to-stdout---cat)
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

### [To Print the details of the file and folder - ls](to-print-the-details-of-the-file-and-folder---ls)

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

### [To Copy Files and Folders - cp](to-copy-files-and-folders---cp)
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

### [To move files and folders - mv](to-move-files-and-folders---mv)
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

### [To create an empty file - touch](to-create-an-empty-file---touch)
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

### [To create a directory - mkdir](to-create-a-directory---mkdir)

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

### [To delete files and folders - rm](to-delete-files-and-folders---rm)
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

### [To print messages to stdout - echo](to-print-messages-to-stdout---echo)
To print messages to the screen use `echo`

```shell
➜  dir1 echo "How are you?"
How are you?
➜  dir1 echo How are you
How are you
➜  dir1
```

### [To read a text file - less](to-read-a-test-file---less)
Use `less` to read the files in the form of pages -  `less file.log`.  Use `spacebar`/`f` to move to next page in forward direction. Use `b` to go to page backwards. In order to search a text in the following pages use `/word`. In order to search a text in the previous pages use `?word`. Once searched use `n` to search next occurrence in forward direction and use `N` to search occurrence in the reverse direction.  To go to the starting point of file use `g`. Similarly to go to the last line use `G`.  Use `F` to tail the file, as the input comes, it will show the input and scroll to next line. Use `&word` to display only those lines which match a pattern. If you are reading a code file which uses brackets like `{}`, `()`, `[]` then you can type `{`, `}`, `(`, `)`, `[`, `]` to find the corresponding opening or closing brackets - make sure those opening brackets are the first line in the screen.

### [To search for text in files - grep](to-search-for-text-in-files---grep)

`grep` is the tool to search for text in files. 

In its simple form, find all the lines in the file that has a particular word in it -  `grep myword file.log`

We can pass a regular expression for the file to search in multiple files - `grep myword *.log`

In order to search for case insensitive word in the file, use `-i` flag - `grep -i myWord *.log`

```shell
➜  testdirectory grep Purpose testnextfile.txt
Purpose is to use AI.
➜  testdirectory grep -i Purpose testnextfile.txt
My purpose is to provide intelligent and multilingual responses to queries.
what is our purpose?
Purpose is to use AI.
➜  testdirectory
```

If we want to search for all those lines which do not match the word then use `-v` flag - `grep -v myWord *.log`

```shell
➜  testdirectory grep test testnextfile3.txt
This is a test line with word - TEST
This is another test with word - TEST
➜  testdirectory grep -v test testnextfile3.txt
This is a line without the key word
➜  testdirectory
```

If we want to display only the file names which have the matching word/pattern then use `-l` flag - `grep -l myword *.log`. Similarly, in-order to list all the files which do not have the matching word/pattern then use `-L` - `grep -L myword *.log`
```shell
➜  testdirectory grep -l the test*
testnextfile.txt
testnextfile1.txt
➜  testdirectory grep -L the test*
testnextanotherdirectory.txt
testnextfile2.txt
➜  testdirectory
```

If we want to display the line number along with the line where the match was found use `-n` flag - `grep -n myword *.log`.

```shell
➜  testdirectory grep -n the test*
testnextfile.txt:5:I strive to offer accurate and insightful answers tailored to the needs of each user.
testnextfile1.txt:3:With a population of over 1.3 billion people, India is the second most populous country in the world.
testnextfile1.txt:5:India is famous for its historical landmarks like the Taj Mahal and vibrant festivals like Diwali and Holi.
testnextfile1.txt:9:India's economy is one of the fastest-growing in the world, with sectors like IT, agriculture, and pharmaceuticals playing a crucial role.
```

To print the name of the file along with the matched lines, use flag `-H` - `grep -H myword *.log`

If we want to stop the search after max number of matched lines, use flag `-m` - `grep -m 2 myword *.log`
```shell
➜  testdirectory grep the test*
testnextfile.txt:I strive to offer accurate and insightful answers tailored to the needs of each user.
testnextfile1.txt:With a population of over 1.3 billion people, India is the second most populous country in the world.
testnextfile1.txt:India is famous for its historical landmarks like the Taj Mahal and vibrant festivals like Diwali and Holi.
testnextfile1.txt:India's economy is one of the fastest-growing in the world, with sectors like IT, agriculture, and pharmaceuticals playing a crucial role.

➜  testdirectory grep -m 2 the test*
testnextfile.txt:I strive to offer accurate and insightful answers tailored to the needs of each user.
testnextfile1.txt:With a population of over 1.3 billion people, India is the second most populous country in the world.
testnextfile1.txt:India is famous for its historical landmarks like the Taj Mahal and vibrant festivals like Diwali and Holi.
```

To get only the count of the matched lines use flag `-c` - `grep -c myword *.log`

```shell
➜  testdirectory grep -c the test*
testnextanotherdirectory.txt:0
testnextfile.txt:1
testnextfile1.txt:3
testnextfile2.txt:0
```

When you use regular expression to provide target files, the list of files might include the folder as well , grep will not work for directories and it will throw an error. Sometimes it cannot search a file due to permissions issue. In such cases it will print an error message. When searching large number of files, you would like to suppress these error/warnings. Use `-s` flag - `grep -s myword *est`

```shell
➜  dir1 grep "123-1234-1234" test*
testanotherfile.txt:123-1234-1234 this is a test.
grep: testdirectory: Is a directory
testfile.txt:My capabilities include language translation, information 123-1234-1234 retrieval, and problem-solving.
testfile1.txt:The country has made significant advancements in technology, 123-1234-1234 space exploration, and various industries.

➜  dir1 grep -s  "123-1234-1234" test*
testanotherfile.txt:123-1234-1234 this is a test.
testfile.txt:My capabilities include language translation, information 123-1234-1234 retrieval, and problem-solving.
testfile1.txt:The country has made significant advancements in technology, 123-1234-1234 space exploration, and various industries.
```

Grep do not search if the target location is a folder. If we want to search in all the files under that directory then use `-r` flag. Example `grep -r myword targetdirectory`

```shell
➜  dir1 grep "123-1234-1234" test*
testanotherfile.txt:123-1234-1234 this is a test.
grep: testdirectory: Is a directory
testfile.txt:My capabilities include language translation, information 123-1234-1234 retrieval, and problem-solving.
testfile1.txt:The country has made significant advancements in technology, 123-1234-1234 space exploration, and various industries.

➜  dir1 grep -r  "123-1234-1234" test*
testanotherfile.txt:123-1234-1234 this is a test.
testdirectory/testnextfile.txt:My capabilities include language translation, information 123-1234-1234 retrieval, and problem-solving.
testdirectory/testnextfile1.txt:The country has made significant advancements in technology, 123-1234-1234 space exploration, and various industries.
testdirectory/testnextanotherdirectory.txt:123-1234-1234 this is a test.
testfile.txt:My capabilities include language translation, information 123-1234-1234 retrieval, and problem-solving.
testfile1.txt:The country has made significant advancements in technology, 123-1234-1234 space exploration, and various industries.
```

Sometimes we would like to get the context around the matched line. We would like to display along with the matched line few lines before that matched line. In such cases use `-B` - `grep -B 2 myword myfile` . Similarly, sometimes we would like to see few lines after the matched line. In such cases use `-A` example - `grep -A 2 myword myfile`.

```Shell
➜  testdirectory grep Hindi testnextfile1.txt
The country's official language is Hindi, but it has 22 recognized languages.
➜  testdirectory grep -B 2 Hindi testnextfile1.txt
It shares borders with Pakistan, China, Nepal, Bhutan, Bangladesh, and Myanmar.
With a population of over 1.3 billion people, India is the second most populous country in the world.
The country's official language is Hindi, but it has 22 recognized languages.
➜  testdirectory grep -A 2 Hindi testnextfile1.txt
The country's official language is Hindi, but it has 22 recognized languages.
India is famous for its historical landmarks like the Taj Mahal and vibrant festivals like Diwali and Holi.
It is a secular republic with a parliamentary system of government.
➜  testdirectory
```


To specify the to be matched word, we can specify regular expressions. To use regular expression for matching word, use flag `-e`. Example to match all the 3 letter words which are ending with letter t 

```Shell
➜  testdirectory grep -e "[a-z][a-z]t" testnextfile4.txt
This is cat
there is mat
then there is hat
why not pot
why not ant
hey there is bat
oh there is dot
➜  testdirectory
```

If we just want to list the matched word instead of complete line use `-o` flag - 

```Shell
➜  testdirectory grep -oe "[a-z][a-z]t" testnextfile4.txt
cat
mat
hat
not
pot
not
ant
bat
dot
➜  testdirectory
```

Some of the special characters honoured in the regular expressions are - 

- `*` - it can match any character  0 or more times
- `+` - any character but atleast 1 occurrence should be there. 
- `.` - any single character
- `?` - 0 or 1 occurrence of any character
- `^` - search the preceding characters at the beginning of the line
- `$` - search the preceding characters at the end of the line
- `[]` - Used to specify a group of possible character for a single position. Example - `[A-Z]`, `[0-9]`, `[a-z0-9]`, `[amn]`. If used with `^` it can be treated as negation - `[^mto]` excluding m,t,o rest of the characters is okay
- `|` - to chose either one of the patter. Example - `ABC|XYZ` - either `ABC` or `XYZ` are matched.
- `{}` - to match preceding elements based on the number of occurrence.
	- `{n}` - if it occurs exactly n times
	- `{n,m}` - if it occurs atleast n times but not more than m times
	- `{n,}` - if it occurs atleast n times.
	- `{,m}` - if it occurs not more than m times

### [To know the difference between files - diff](to-know the difference-between-files---diff)
If we have 2 text files and want to compare then & find differences in them use `diff` - Example `diff file1 file2`

```shell
➜  dir1 diff tempfile1.txt tempfile2.txt
1,2c1,2
< This is a text in tempfile1
< This is an unique line in tempfile1
---
> This is a text in tempfile2
> Here is something very different in tempfile2
➜  dir1

➜  dir1 cp tempfile1.txt tempfile3.txt
➜  dir1 diff tempfile1.txt tempfile3.txt
➜  dir1
```

For a better format use `-u` - `diff -u file1 file2`
```shell
➜  dir1 diff -u tempfile1.txt tempfile2.txt
--- tempfile1.txt       2024-06-24 22:46:17.259536361 -0700
+++ tempfile2.txt       2024-06-24 22:47:10.270392162 -0700
@@ -1,3 +1,3 @@
-This is a text in tempfile1
-This is an unique line in tempfile1
+This is a text in tempfile2
+Here is something very different in tempfile2
 This is a common line
➜  dir1
```

### [To find a file - find](to-find-a-file---find)
Sometimes we do not know the location of the file. We can use `find` to locate that file in the given directory tree - `find dir -name file -print`

```shell
➜  ~ ls ~/workspace/Playground/dir1/testdirectory
tempfile3.txt  testnextanotherdirectory.txt  testnextfile1.txt  testnextfile3.txt
tempfile4.txt  testnextfile.txt              testnextfile2.txt  testnextfile4.txt
➜  ~ find workspace -name tempfile4.txt -print
workspace/Playground/dir1/testdirectory/tempfile4.txt
➜  ~
➜  ~ find workspace -name tempfile3.txt -print
workspace/Playground/dir1/testdirectory/tempfile3.txt
workspace/Playground/dir1/tempfile3.txt
➜  ~
```

`find` can do multiple things on finding the file like print contents or exec. Example to know all the files and folder in a folder we can use `find directorypath` 

```shell
➜  ~ find ~ | wc -l
731986
➜  ~
```

We can use `-type` argument to restrict the search to particular type of file - file, directory, symbolic link

```shell
➜  ~ find workspace -name commonfilefolder -print
workspace/Playground/dir2/testfiledir/commonfilefolder
workspace/Playground/dir2/commonfilefolder
➜  ~ find workspace -type d -name commonfilefolder -print
workspace/Playground/dir2/testfiledir/commonfilefolder
➜  ~ find workspace -type f -name commonfilefolder -print
workspace/Playground/dir2/commonfilefolder
➜  ~
```

We can also use `size` attribute to search files based on file size (to be continued)

### Still To Come
- wc, head, tail, uniq, sort, ln, ps, kill, chown, chsh, sudo, chgrp, chmod, su, ping, ip, ssh, scp, traceroute, netstat,curl, wget, tar, zip, gzip, bzip2