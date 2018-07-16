[CADES](http://support.cades.ornl.gov/) → [User Documentation](../README.md) → [Linux](linux-intro.md) → [Managing Files](managing-files.md)

# Managing Files

<!-- TOC depthFrom:2 depthTo:2 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Part 1: Working with the Contents of Files](#part-1-working-with-the-contents-of-files)
- [Part 2: Data Manipulation](#part-2-data-manipulation)
- [Part 3: Working with a Collection of Files](#part-3-working-with-a-collection-of-files)
- [Part 4: Comparing Differences Between the Contents of Files](#part-4-comparing-differences-between-the-contents-of-files)
- [Part 5: Compressing and Extracting Files](#part-5-compressing-and-extracting-files)

<!-- /TOC -->

## Part 1: Working with the Contents of Files

Let's consider the content of file `/tmp/matrix.c`. You may paste the contents of the file into `/tmp/matrix.c` using your favorite text editor.

```c
#include <stdio.h>

#include "mpi.h"

#define N               4        /* number of rows and columns in matrix */

MPI_Status status;

double a[N][N],b[N][N],c[N][N];

main(int argc, char **argv)

{

  int numtasks,taskid,numworkers,source,dest,rows,offset,i,j,k;

  struct timeval start, stop;

  MPI_Init(&argc, &argv);

  MPI_Comm_rank(MPI_COMM_WORLD, &taskid);

  MPI_Comm_size(MPI_COMM_WORLD, &numtasks);

  numworkers = numtasks-1;
```

- #### head: read the first few lines of the given text as an input

  ```bash
  head -n 3 /tmp/matrix.c > /tmp/matrix_head.txt
  ```

  _The initial three lines of content will be directed into a new file named '/tmp/matrix_head.txt'._

  If you use only `head /tmp/matrix.c`, the first ten lines are displayed.

- #### tail: read the final few lines of any text given to it as an input

  ```bash
  tail -n 6 /tmp/matrix.c > /tmp/matrix_tail.txt
  ```

  _The last six lines of the file `/tmp/matrix.c` will be shown in `/tmp/matrix_tail.txt`._

- #### more: lets you view text files or other output in a scrollable manner. It displays the text one screenful at a time. Press `<Space>` to advance the screen.

  ```bash
  more /tmp/matrix.c
  ```

  _All of the lines of the file `/tmp/matrix.c` will be displayed._

- #### less: is a program similar to more, but allows backward movement in the file as well as forward movement. Additionally, you may search for patterns using **less**.

  ```bash
  less /tmp/matrix.c
  ```

  _The content of the file `/tmp/matrix.c` will be displayed on the terminal and you can navigate by pressing the up and down arrows._

- #### wc: word count

  ```bash
  wc /tmp/matrix.c
     21      64      367  /tmp/matrix.c
  ```

  _Here, 21 is shown in the first column which represents the 21 lines, 64 words and 367 characters of the file `/tmp/matrix.c`._

  It is possible to provide the output for multiple files by listing the name of each separated by a space. For example: `wc file1 file2 file3`.

  In case you need to know the size of an image file in the current directory as well as the total for all of them, you can use the `-c` option like: `wc -c *.jpg`.

## Part 2: Data Manipulation

Let's apply commands to filter, sort, group, match, and replace data in the file `/tmp/data.txt`. You may paste the contents of the file into `/tmp/data.txt` using your favorite text editor.

NAME    | START LOCATION | END LOCATION |  cM   | SNPs |            Comments
------- | :------------: | :----------: | :---: | :--: | ------------------:
Wendi   |     72017      |   5827331    | 12.43 | 1686 |        Match to Mom
Sheila  |    6514775     |   1500362    | 6.65  | 1089 |        Match to Mom
Michael |    3793615     |   12596858   | 17.25 | 2785 | Match to Dad or IBS
Robert  |    4090545     |   5115145    | 2.68  | 500  |      Mom but not me
Sheila  |    2514775     |   5600362    | 8.65  | 1189 |        Match to Mom

- #### sed: a special editor for modifying files, mostly used for substitutions

  ```bash
  sed 's/Sheila/Linda/'/tmp/data.txt > /tmp/data.txt.bak
  ```

  _This replaces all occurrences of `Sheila` with `Linda` in the file `/tmp/data.txt`, and sends the output to `data.txt.bak`._

  It is crucial to redirect the desired changes into another file in case you will need to review or compare to the original file.

- #### grep: search the input file(s) for _lines_ containing a match to a given pattern. This utilizes [regular expression](https://en.wikipedia.org/wiki/Regular_expression) patterns.

  ```bash
  grep 'Match to Mom' /tmp/data.txt > /tmp/data.txt.2
  ```

  _The content of the file `/tmp/data.txt.2` will include the lines that contain "Match to Mom", taking the file `/tmp/data.txt` as an input._

- #### awk: to parse and manipulate tabular data. It operates on a line-by-line basis and iterates through the entire file.

  ```bash
  awk '{print $1,$6;}' /tmp/data.txt > /tmp/data_tab.txt
  ```

  _It will display in columns: **NAME** (column 1) and **Comments** (column 6) in the `/tmp/data_tab.txt` file._

  You may need to list only the rows that contain a **value of cM greater than 10**, then you run `awk '$4 >10' /tmp/data.txt`

  If you want to know the rows that contain "Match to Mom", then type `awk '$4 ~/Match to Mom/'`

- #### sort: is used to sort a file, arranging records in a particular order. By default, the `sort` command sorts file using ASCII.

  ```bash
  sort -k 5n /tmp/data.txt
  ```

  _In this case, the data is going to be sorted according to **SNPs** because the option `5k` (5th column) is set. It was set also `n` because they are numbers._

  If you need to sort data in descending order, you will need to use the option `-r`, which means **reverse**, like this:`sort -k 5n -r /tmp/data.txt`.

  In case you want to sort and remove duplicates, then use the option `-u`, like this: `sort -u /tmp/data.txt`.

  If you want to sort a list to ordered by month name, then use the option `-M`, like this: `sort -M /your/file`.

## Part 3: Working with a Collection of Files

Let's work with the files that are located inside `/tmp/test_files`. [Here are the instructions](scripts/loop_for1.md) to create them.

```bash
user:test_files x0y$ ls -l
total 0
-rw-r--r--  1 x0y  user  0 Apr 10 09:37 test0.txt
-rw-r--r--  1 x0y  user  0 Apr 10 09:37 test1.txt
-rw-r--r--  1 x0y  user  0 Apr 10 09:37 test2.txt
-rw-r--r--  1 x0y  user  0 Apr 10 09:37 test3.txt
-rw-r--r--  1 x0y  user  0 Apr 10 09:37 test4.txt
-rw-r--r--  1 x0y  user  0 Apr 10 09:37 test5.txt
-rw-r--r--  1 x0y  user  0 Apr 10 09:37 test6.txt
-rw-r--r--  1 x0y  user  0 Apr 10 09:37 test66.txt
```

- #### find: to search for files based on various search criteria like permissions, user ownership, modification of date/time, size, etc.:

  ```bash
  find . -name "*6*" -user x0y
  ```

  _In this case, the search happens in the current path (`.`) and is looking for those files that have the number 6 in their name, and were created by the user **x0y**._

  If you want to search for a file(s) in which the filename has the characters "conf" and modified 7 days ago, then type: `find / -name "*conf" -mtime 7`.

  If you want to find a file without searching over the entire network or mounted filesystems on your system, you would run: `find / -name foo.bar -print -xdev`.

## Part 4: Comparing Differences Between the Contents of Files

For this section, we will use the files `/tmp/test_file/test6.txt` and `/tmp/test_file/test66.txt`. You may paste the contents of the two files into `/tmp/test_file/` using your favorite text editor.

```bash
$ cat test6.txt
Weld I.D.    Material Grade        Segment Tested        Accepted
========================================================================
004          CS AH38               100%                  No
009          CS AH30                50%                  No
099          CS AH40                50%                  No
100          CS AH67               100%                  Yes

$ cat test66.txt
Weld I.D.    Material Grade        Segment Tested        Accepted
========================================================================
004          CS AH38               100%                  No
009          CS AH30                50%                  No
099          CS AH40                50%                  No
200          CS AH44                75%                  No
100          CS AH67               100%                  Yes
```

- #### diff: show the differences between two files' contents

  ```bash
  diff test6.txt test66.txt
    5a6
    > 200        CS AH44            75%            No
  ```

  _In this case, the differences between the two files `test6.txt` and `test66.txt` are located in lines 5 and 6._

  If you want to restrict the number of columns, you can run: `diff --width=5 test6.txt test66.txt`.

  If you want to know if the files are different without interest in which lines are different, please run `diff -q test6.txt test66.txt`.

## Part 5: Compressing and Extracting Files

To create files with extensions such as `.tar`, `tar.gz`, `.tgz`, `.gz`, or `.bz2` use the commands `tar` (also useful to extract files), `gzip`, or `bzip2`.

- #### gzip: compresses the size of the given files. Whenever possible, each file is replaced by one with the extension `.gz`.:

  ```bash
  gzip test66.txt
  ```

  _It will compress **test66.txt** file using the "gzip" command it will have as an output `test66.gz`_.

- #### bzip2: bzip2 creates smaller archives than gzip but has a slower decompression time and higher memory use

  ```bash
  bzip2 -k test66.txt
  ```

  _It will compress the file test66.txt. It will keep the uncompressed version and create the new file: `test66.txt` and `test66.txt.bz2`._

  To decompress the file and remove the `bz2` extension, please run `bzip2 -d test66.txt.bz2`.

- #### zip: compress the size of the given files. Whenever possible, each file is replaced by one with the extension `.gz`.

  ```bash
  zip test.zip test66.txt test6.txt
  ```

  _It will compress `test66.txt` and `test6.txt` files into a directory called test.zip_.

  To compress a directory, please run `zip -r squash.zip dir1`. This will zip the whole directory `dir1` into `squash.dir`.

  To decompress, use `unzip squash.zip`; this unzips it in your current working directory.

- #### tar: bundle many files together into a single file on a single tape or disk. If you have more than 2 files then it is recommended to use tar instead of gzip or bzip2.

  ```bash
  tar -cvf output.tar /dirname
  ```

  _It will compress the `/dirname` directory and create a file called a "tar ball" named `output.tar`._

  To install `tar`, please run `yum install tar` or `apt-get install tar`, to extract the content of `output.tar`, please run `tar -xvf output.tar`.
