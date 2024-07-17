---
category: Technical
date: 2024-06-14
layout: post
title: Linux commands for Reference
updated: 2024-07-05
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
- [To sort out a given list of string or numbers - sort](#to-sort-out-a-given-list-of-strings-or-numbers---sort)
- [To filter out duplicate lines and get only unique entries - uniq](#to-filter-out-duplicate-lines-and-get-only-unique-entries---uniq)
- [To find a file - find](#to-find-a-file---find)
- [To view last few lines of the file or follow the log in live - tail](#to-view-last-few-lines-of-the-file-or-follow-the-log-in-live---tail)
- [To view first few lines of the file - head](#to-view-first-few-lines-of-the-file---head)
- [To extract section of text from the line - cut](#to-extract-section-of-text-from-the-line---cut)
- [To list process that are running - ps](#to-list-process-that-are-running---ps)
- [To view the system stats and list of processes in real time - top](#to-view-the-system-stats-and-list-of-processes-in-real-time---top)
- [To kill a process that is running - kill](#to-kill-a-process-that-is-running---kill)

## Commands
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


### [To count the number of lines or words or characters - wc](to-count-the-number-of-lines-or-words-or-characters---wc)
Sometimes we would like to get the count of lines or words in a given text file. We can use `wc` example - `wc file.txt`

```shell
➜  harsha-kadekar.github.io git:(master) wc /etc/passwd
  58  112 3578 /etc/passwd
```

To just know the number of lines use `-l` flag

```shell
➜  harsha-kadekar.github.io git:(master) wc -l /etc/passwd
58 /etc/passwd
```

To just know the number of words use `-w` flag

```shell
➜  harsha-kadekar.github.io git:(master) wc -w /etc/passwd
112 /etc/passwd
```

To just know the number of bytes use `-c` flag

```shell
➜  harsha-kadekar.github.io git:(master) wc -c /etc/passwd
3578 /etc/passwd
```


### [To sort out a given list of string or numbers - sort](to-sort-out-a-given-list-of-strings-or-numbers---sort)

If we have a list of words in a file and we want to sort them out, we can use `sort` command - `sort myfile`
```shell
➜  dir1 cat samplefile.txt
cat
bat
mat
pet
bat
eat
cat
top
bat
and
dot
➜  dir1 sort samplefile.txt
and
bat
bat
bat
cat
cat
dot
eat
mat
pet
top
```

If we want to sort in the descending order, we can use `-r` flag.

```shell
➜  dir1 sort -r samplefile.txt
top
pet
mat
eat
dot
cat
cat
bat
bat
bat
and
➜  dir1
```

This uses alphabetic order for sorting. If we have a list of numbers, we might want to sort them as numbers, instead of alphabetic order. We need to use `-n`

```shell
➜  dir1 cat samplefileNumber.txt
1
56
5
7
20
3
7
89
0
5
2
44
6
18
➜  dir1 sort -n samplefileNumber.txt
0
1
2
3
5
5
6
7
7
18
20
44
56
89
➜  dir1
```
### [To filter out duplicate lines and get only unique entries - uniq](to-filter-out-duplicate-lines-and-get-only-unique-entries---uniq)
In the sorted list, we want to use only the unique elements, in such a case, we can use `uniq` command on the `sort` output.

```shell
➜  dir1 sort samplefile.txt
and
bat
bat
bat
cat
cat
dot
eat
mat
pet
top
➜  dir1 sort samplefile.txt | uniq
and
bat
cat
dot
eat
mat
pet
top
```

If we want to know the number of occurrence of the words then use `-c` flag
```shell
➜  dir1 sort samplefile.txt | uniq -c
      1 and
      3 bat
      2 cat
      1 dot
      1 eat
      1 mat
      1 pet
      1 top
```

If we want to only display the repeated words then we can use `-d` flag
```shell
➜  dir1 sort samplefile.txt | uniq -d
bat
cat
```
The opposite case of display only those which are unique and not repeated, can be achieved via `-u` flag

```shell
➜  dir1 sort samplefile.txt | uniq -u
and
dot
eat
mat
pet
top
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

We can also use `size` attribute to search files based on file size.

```shell
➜  ~ find Downloads -type f -size +100M | wc -l
49
➜  ~ find Downloads -type f -size +200M | wc -l
38
```

We also have following useful parameter
- `-empty` - match only empty files and directories
- `-name pattern` - match files and directory with specified pattern
- `-user name` - match files and directories belonging the given user
- `-newer file` - match only files which are newer that the given file

Once we find the files, we can ask find to act on it like - 
- `-delete` - this will delete the matching files
- `quit` - quit find immediately after first match
- `-ls` - do a `ls` on the found file/folder

We can use `-exec command '{}' ';'`  to execute custom commands on the matched files/folders. Example `find ~ -type f -name 'testfile*' ls -l '{}' ';' `. We can make the command interactive with `-ok` attribute - `find ~ -type f -name 'testfile*' -ok ls -l '{}' ';'`

### [To view last few lines of the file or follow the log in live - tail](to-view-last-few-lines-of-the-file-or-follow-the-log-in-live---tail)
`tail` can be used to view the last 10 lines of the file `tail myfile`. We can modify the number of lines to display with `-n` flag.

```shell
➜  dir1 cat tempfile1.txt
This is a text in tempfile1
This is an unique line in tempfile1
This is a common line
➜  dir1 tail -n 2 tempfile1.txt
This is an unique line in tempfile1
This is a common line
➜  dir1
```

Sometimes we would want to view the content of the file live as in as it gets added by another process, we need to use `-f` flag. It will keep following the file until `Ctrl+C` is pressed.

```shell
➜  dir1 tail -f tempfile1.txt
```

### [To view first few lines of the file - head](to-view-first-few-lines-of-the-file---head)
Similar to `tail` command, this command helps to view the first few lines of the file. By default it will show first 10 lines. With `-n` flag, we can control the number of lines we want to display.

```Shell
➜  dir1 cat tempfile1.txt
This is a text in tempfile1
This is an unique line in tempfile1
This is a common line
this is a new line added in live
➜  dir1 head -n 2 tempfile1.txt
This is a text in tempfile1
This is an unique line in tempfile1
➜  dir1
```

### [To extract section of text from the line - cut](to-extract-section-of-text-from-the-line---cut)
We can use `cut` to extract particular fields or certain range of characters from the given line. To extract based on the field we can use flag `-f`. By default cut divides the line based on the `tab`/`space`. 

```Shell
➜  dir1 cat datafile.txt
Harsha  ABC     2024-07-12      45red89
Anu     MNO     2024-11-01      67sea90
Smriti  JKL     2024-01-23      90blr45
➜  dir1 cut -f 3 datafile.txt
2024-07-12
2024-11-01
2024-01-23
```

If we want to use some other delimiter than `tab`/`space` then use `-d` flag with the delimiter mentioned. 

```Shell
➜  dir1 cut -f 3 datafile.txt | cut -d '-' -f 2
07
11
01
```

If we want to cut specific position of characters, we can use `-c` flag

```Shell
➜  dir1 cut -f 4 datafile.txt | cut -c 3-5
red
sea
blr
```

### [To list process that are running - ps](to-list-process-that-are-running---ps)

`ps` command helps to list all processes which are running in the system. The default `ps` will only display the current process associated with the current terminal.
```Shell
➜  Playground ps
    PID TTY          TIME CMD
  36329 pts/3    00:00:00 zsh
  36698 pts/3    00:00:00 ps
➜  Playground
```

- `PID` is the process ID
- `TTY` is the terminal id to which these processes are associated
- `TIME` is the amount of time process spent in CPU
- `CMD` is actual command that started this process

In order to list all the process belonging the current user across all terminals, we need to use `x`. This will also give more details about the process

```Shell
➜  Playground ps x
    PID TTY      STAT   TIME COMMAND
   2290 ?        Ss     0:01 /lib/systemd/systemd --user
   2291 ?        S      0:00 (sd-pam)
   2297 ?        S<sl   0:00 /usr/bin/pipewire
   2298 ?        Ssl    0:11 /usr/bin/pipewire-media-session
   2299 ?        S<sl  14:24 /usr/bin/pulseaudio --daemonize=no --log-target=journal
   4692 ?        Sl     0:00 /opt/vivaldi/chrome_crashpad_handler --monitor-self --monitor-self-annotation=ptype=crashpad-handler --database=/home/harsha/.config/vivaldi/Crash Reports --url=https://crash
   4694 ?        Sl     0:00 /opt/vivaldi/chrome_crashpad_handler --no-periodic-tasks --no-rate-limit --monitor-self-annotation=ptype=crashpad-handler --database=/home/harsha/.config/vivaldi/Crash Report
   4700 ?        S      0:00 /opt/vivaldi/vivaldi-bin --type=zygote --no-zygote-sandbox --crashpad-handler-pid=4692 --enable-crash-reporter=,stable --change-stack-guard-on-fork=enable
   4984 ?        Sl     0:01 update-notifier
   6362 ?        Sl     1:00 /snap/obsidian/34/obsidian --no-sandbox
   10790 ?        Z      0:00 [sd_espeak-ng-mb] <defunct>
    36800 pts/3    R+     0:00 ps x
```
- If a `TTY` is `?` that means, no terminal is associated to the process. 
- `STAT` - state of the process. Example `S` means process is sleeping and waiting for an interrupt to wake up. `R` means running. `Z` means a zombie process which is terminated and parent has not yet cleaned up. `<` means higher priority process and `L` means low priority process

To get a detailed process across all terminals and users, we need to use `aux`

```Shell
➜  Playground ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0 167548 11956 ?        Ss   07:35   0:03 /sbin/init splash
root           2  0.0  0.0      0     0 ?        S    07:35   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   07:35   0:00 [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   07:35   0:00 [rcu_par_gp]
root           5  0.0  0.0      0     0 ?        I<   07:35   0:00 [slub_flushwq]
root           6  0.0  0.0      0     0 ?        I<   07:35   0:00 [netns]
root        1202  0.0  0.0      0     0 ?        I<   07:35   0:00 [ext4-rsv-conver]
systemd+    1241  0.1  0.0  14836  6784 ?        Ss   07:35   1:39 /lib/systemd/systemd-oomd
systemd+    1242  0.0  0.0  26200 13932 ?        Ss   07:35   0:25 /lib/systemd/systemd-resolved
syslog      1371  0.0  0.0 222456  5888 ?        Ssl  07:35   0:00 /usr/sbin/rsyslogd -n -iNONE
lp          2255  0.0  0.0  16288  6528 ?        S    07:35   0:00 /usr/lib/cups/notifier/dbus dbus://
harsha      2290  0.0  0.0  18560 11136 ?        Ss   07:35   0:01 /lib/systemd/systemd --user
harsha      2291  0.0  0.0 105220  6576 ?        S    07:35   0:00 (sd-pam)
harsha      2297  0.0  0.0  40696  6400 ?        S<sl 07:35   0:00 /usr/bin/pipewire
harsha      2298  0.0  0.0  24332  6528 ?        Ssl  07:35   0:11 /usr/bin/pipewire-media-session
harsha     33810  0.5  0.2 1374176 90444 ?       Rl   21:33   0:14 /snap/alacritty/130/bin/alacritty
```
- `USER` - this gives the user which owns/created this process
- `%CPU` - Total percentage of CPU utilised by the process until now
- `%MEM` - Total percentage of memory utilised by the process until now
- `VSZ` - Total virtual size of the RAM utilised by the process
- `RSS` - This is the physical RAM size utilised by the process
- `START` - This is the time of the day when the process was started.

### [To view the system stats and list of processes in real time - top](to-view-the-system-stats-and-list-of-processes-in-real-time---top)
Unlike `ps`, top gives the real time view of all the process running with sorted based on the CPU utilisation. `top` refreshes every 3 seconds

```Shell
➜  ~ top

top - 23:33:55 up 16:01,  1 user,  load average: 1.07, 0.74, 0.72
Tasks: 383 total,   1 running, 381 sleeping,   0 stopped,   1 zombie
%Cpu(s):  0.7 us,  0.4 sy,  0.0 ni, 98.2 id,  0.6 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :  31945.3 total,  19023.3 free,   5263.4 used,   7658.7 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.  24934.8 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   2540 harsha    20   0 5997132 354500 159296 S   5.3   1.1  36:31.31 gnome-shell
  25449 harsha    20   0 1349972  88344  61508 S   1.3   0.3   0:00.74 alacritty
   6201 harsha    20   0 1140.3g 367220 129584 S   1.0   1.1  10:00.25 obsidian
  24538 harsha    20   0 1133.8g 332880 142924 S   1.0   1.0   1:25.30 vivaldi-bin
   1270 root      20   0 2133856  35164  19584 S   0.7   0.1   0:15.26 snapd
   4628 harsha    20   0   32.8g 533412 254964 S   0.7   1.6  11:26.93 vivaldi-bin
   4682 harsha    20   0   32.4g 148796 106708 S   0.7   0.5   5:42.27 vivaldi-bin
   6176 harsha    20   0   32.7g 145412  98048 S   0.7   0.4  11:15.50 obsidian
   6818 harsha    20   0 9851.2m 315956 180404 S   0.7   1.0   8:44.26 spotify
    678 root     -51   0       0      0      0 S   0.3   0.0   0:15.02 irq/144-iwlwifi:default_queue
    869 root      20   0       0      0      0 S   0.3   0.0   5:22.79 nv_queue
   2873 harsha    20   0  719316  68876  41968 S   0.3   0.2   0:47.72 ulauncher
   2926 harsha    20   0  708212 111444  73856 S   0.3   0.3   8:24.45 Xwayland
   3092 harsha    20   0   36.7g 136260 104176 S   0.3   0.4   1:54.10 breaktimer
   4768 harsha    20   0 1132.0g 391660 137444 S   0.3   1.2   7:27.01 vivaldi-bin
   4791 harsha    20   0 7967144 332528  49792 S   0.3   1.0   2:33.62 jetbrains-toolb
   5908 harsha    20   0 1132.0g 261640 129736 S   0.3   0.8   6:40.10 vivaldi-bin
   7033 harsha    20   0   50.3g 280020 107984 S   0.3   0.9  53:06.65 spotify
  11532 harsha    20   0 1133.9g 358624 171444 S   0.3   1.1   5:40.96 vivaldi-bin
  11570 harsha    20   0   32.4g 113316  59164 S   0.3   0.3   1:41.08 vivaldi-bin
  24729 root      20   0       0      0      0 I   0.3   0.0   0:00.09 kworker/2:1-mm_percpu_wq
  25619 harsha    20   0 1678412  74392  17184 S   0.3   0.2   0:00.90 zellij
  25690 harsha    20   0   14600   4224   3200 R   0.3   0.0   0:00.70 top
      1 root      20   0  168976  13436   8060 S   0.0   0.0   0:05.43 systemd
```

The top row is showing 
- `23:33:55` - the current time of the day
- `up 16:01` - System is up for 16 hours
- `1 user` - 1 user is logged in
- `load average: 1.07, 0.74, 0.72` - Number of processes waiting to run 5 second, 5 mins and 15 mins
- `Tasks` - Number of processes and categorised based on the state of the process
- `%Cpu(s)` - How the CPU is being used - `u` for user processes, `s` for system/kernel process, `ni` for nice/lower priority processes, `id` for idle, `wa` for waiting for IO, `hi` for managing hardware interrupts, `si` for managing software interrupts, `st` for getting hold of physical CPU/ time stolen by the hypervisor.
- `MiB Mem` and `MiB Swap` - memory and swap usage information
- `VIRT` is virtual memory, `RES` is the physical memory and `SHR` is shared memory
### [To kill a process that is running - kill](to-kill-a-process-that-is-running---kill)

Sometimes the process has reached a bad state or just in a zombie state without doing anything. In such cases, we can use `kill` to terminate the process. Example - `kill 1234` where `1234` was the process id. `kill` command performs this action by sending signals. It can send multiple types of signals.
- `TERM` - `15` - Send terminate signal to the program.  This is the default signal of `kill` command. Usage `kill -TERM PID` or `kill -15 PID`
- `INT` - `2` - Send interrupt signal to the program. `Ctrl - C` generates this signal. Usage `kill -INT PID` or `kill -2 PID`
- `KILL` - `9` - Send this signal to kernel to kill a particular program. So, program will not receive this signal, hence not able to clean up properly. Use it rarely. Usage `kill -STOP PID` or `kill -9 PID`
- `STOP` - `19` - Send this signal to kernel to stop a particular program without actually terminating it. Usage `kill -STOP PID` or `kill -19 PID`
- `TSTP` - `20`  - Send this signal for a terminal linked process to stop without killing it. We can use `ctrl z` to achieve this as well. Usage `kill -TSTP PID` or `kill -20 PID`

We can use `killall` command to kill all the processes matching a user or a program name. Usage `killall -u kadekar` or `killall vivaldi`

### Still To Come
- uname, ln, tr, chown, chsh, sudo, chgrp, chmod, su, ping, ip, ssh, scp, traceroute, netstat,curl, wget, tar, zip, gzip, bzip2