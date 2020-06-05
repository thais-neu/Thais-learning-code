# Notes taken while learning code from multiple sources

## Practical Computing for Biologists (Haddock and Dunn) book, Part I

**Chapter 1 - Text files.**
- using BBEdit 

**Chapter 2 - Regular expressions. A language for search and replace.**

- useful table: Table 2. Some common wildcards (search term and meaning)
 
 > \w a word character including letters, numbers and the underscore
 
 > \t a tab character
 
 > \s a white space including space, tabs and end of line
 
 > \r \n end of line marker, depending on the program you're using (R uses \n)
 
 > \d a digit from 0 to 9
 
 > . any letter number or symbol except end of line characters
 
 *note: the slash \ is used to tell the search engine that the following command is not literal, i.e., using w and not \w will search for the letter w.*
 
**Chapter 3 - practicing reg expressions**


## Shell commands (compilation notes from: PCFB book (chapters 7 and 16), Software Carpentry, Open Classrooms - Command Line in Terminal course, Ubuntu Tutorials - The Linux command Line for beginners).

Terminal is in Applications > Utilities

Terminal > Preferences - to change color and other layout options

Ctrl-alt-d opens the terminal

Ctrl-d logout

## **Some commands**

pwd where are you now

ls list contents of a folder, default is your current folder

cd moves you "down" a level from the folder you're in

cd .. moves you "up" a level from the folder you're in

cd - brings you back (up or down) where you were

command K clears the terminal (think 'klean')

command C halts an operation that was done in error, or taking too long, etc. (think 'cancel')

Control a takes you to the beginning of a line

Control e takes you to end of a line

Option cursor position takes you to where the cursor is pointing

Control u wipes out the whole command line


## **Mkdir**

Mkdir creates one or more folders in the directory you're in.

Tips to naming a folder - don't use spaces; if you do use spaces or any other special character, either (1) wrap the whole name in quotations or (2) escape the special character or (3) do both quotations and escape

> **usage: mkdir myfolder or mkdir "my folder" or mkdir my\ folder or mkdir "my\ folder"**

Mkdir can be used to make more than one folder at the same time inside the directory you're in - list more than one name separated by spaces, without quotations so the terminal understands it's more than one folder. This is creating folders inside the working directory, not inside each other (myfolder2 is not created inside myfolder1).

> **usage: mkdir myfolder1 myfolder2 myfolder3**

Mkdir can create a folder with new folders inside it (a nested directory) in the directory you're in when the flag -p and / are used in combination

> **usage: mkdir myfolder1willcontain/myfolder2whichwillcontain/myfolder3**



## **Open, copy, move**

open - opens a file, usage: open myfile.txt


cp - copies a file in another location, usage: cp myfile.ext ../foldertocopyinto

*A file that is copied will exist in both the original and the new location.*


Use an -R flag option to rename a folder or to move a folder to another location

> **cp -R usage: cp -R folder1 folder2**

> **cp -R usage: cp ~/Desktop/folder1 ~/Documents/folder1**



mv moves a file (from where it is) to a location, 

> **usage: mv file_you_want_tomove.ext folder_tomove_itto**

*A file that is moved this way disappears in the original location after you moved it.*

Mv renames a file if two file names are provided instead of a folder name, 

> **usage: mv file_youwant_torename.ext new_filename.ext**

Mv -i will confirm yes or no to minimize accidentally overwriting a file with the same name.


## **Absolute vs relative paths**

Absolute paths is the full address of a file or folder; 

Relative path is the short address, always relative to the working directory (where you are now).


for instance, you're in your working directory and want to create (mkdir) a file inside some other directory, you can used the absolute path:

mkdir biology_data.csv ~/Documents/BiologyProject/Datafolder/

Which will create the file biology_data.csv inside Datafolder when you are NOT inside the folder Datafolder


Or the relative path:

(You are inside the Datafolder but want to create biology_data.csv inside the parent directory BiologyProject; here the .. means "go up a level = out of DataFolder and into Biology project in this cases), and create biology_data.csv there)

Mv biology_data.csv ../BiologyProject



## **Create data files**

touch creates an empty file

> **usage: touch myfile.ext (replace ext with any file extension, such as myfile.txt)**


\> or >> create an output data file - the output or results of a command can be redirected to a file by using > output.txt. This creates a file named output and dumps the content of your command into it, all in one line. The output of any command can be save into a file. (Example: the list of contents of a directory can be sent to a file name output_list)

> **usage (example): ls > output_list.txt**


## **Ways to see the contents of a file:**

open filename.txt will open the file in another window (if you edit anything it will save without confirming); 

> **usage: Open filename.txt**

nano is an editor, it opens an existing file (or creates one if none exists with that name in the folder you're in) in a separate window of an editor called nano - use key strokes listed on bottom of screed to modify, save, scroll and exit the editor. If no changes are made to an existing file, it won't ask you if you want to save. If you make any changes, it will confirm if you want to save them. For that reason, it is preferred over the Open command. 

> **usage: nano filename.txt**

cat dumps the entire content of a file on to the screen; it's good for very short files (if the file is blank, cat will print a ls of the folder instead). Cat is actually not a file reader but a concatenation, that is used to merge files (see below); but when cat is followed by one file, it spits out its contents, so in that sense, it is a 'way to see the contents of a file'.

> **usage: cat myfile.txt**

less is a file reader; dumps parts (one screen =page at the time) of the content of a file right at the command line (not a new window); you need to scroll through to see the next page of content; 

> **usage: less filename.txt**

head dumps the first 10 lines of content on to the screen or as many as specified by the number following the flag -n

> **usage: Head myfile.txt or head -n 32 myfile.txt**

tail is same as head but shows the last lines of a file instead of the first.

*Head and tail accept more than one file, list them sequentially*; ***usage: tail myfile1.txt myfile2.txt***

Grep finds a keyword in a given file and dumps the lines containing that keyword on to the screen right at the command line, 

> **usage: grep guacamole hopper.txt**

Echo is the same as print; combined with a redirecting command > will save the text that you typed into a file 

> **usage: echo "this is an example" > example.txt** if you open example.txt inside nano, you will see the text this is an example.

## **General tips**

Up and down arrows show your latest commands

Tab will auto-fill parts of your command, helps to minimize spelling mistakes and save time

Commands and their options are case-sensitive themselves and to file/folder names.

## Wildcards

Wildcards that apply at the command line:

\? means any single character

\* means zero or more characters

\. Means the current directory

\.. means the parent (one level up) directory

The interpretation of wildcards by the shell is what makes it a bad idea to use special characters in file names.

Example of using wildcards and cat:

> Cat test_?.txt Will print the contents of any .txt file that has a single character (whatever character) following test_ in its name

> Cat test_*.txt will print the contents of any .txt file that has zero or more characters (whatever character) following test_ in its name


Example of using wildcards and head or tail

> Head test_*.txt

Will list the first 10 lines of every .txt file whose name starts with test_


Example of using wildcards and cat and >

> Cat test_*.txt > combinedtest.txt

Will merge the contents of all .txt files in the current directory whose filenames start with test_ and save the merged content into 'combined test.txt'

*If you send another output to 'combinedtest.txt' the content will be overwritten. To avoid that you want to use >> instead of > which will append more content to an existing file instead of replacing the content. So it's safer to always use >> instead of > unless you are sure you want to replace contents of a file.*


## **Deleting things** 

the following commands will delete files and folders permanently - not send them to the trash bin or any other location 

rm delete files

rmdir delete empty folders

rmdir -p delete parent directory

rmdir -R delete a folder and its contents 

rm -i is the interactive option that will ask you to confirm you want to delete something (y=yes, n=no, ctrl c=cancel)


## **Other commands**

ls -l will show the permissions for each file in a folder

wc counts; 

> usage wc - l (will spit out the number of lines in a file)

man a manual for commands;

> usage: man mkdir (then use q to quit and return to command line)

Su is a command to switch user 

Sudo (means "run as administrator") - is a command to request the super user power on a per-command basis (will require a password); might be needed to install new software.

Sudo su - goes to the root of the system, don't use.

**Hint: if you try access a file and get the message "...permission denied", try again using sudo.**

Hidden files have a filename starting with .

If you want to save file as hidden, do mv combined.txt .combine.txt

If you want to ls all files, including hidden files, do ls -a 


## **Pipe**
Pipes pipe the output of the command on the left directly as an input argument of the command on the right

> usage (example): ls . | wc -l 

In this example, the command will list (ls) the contents of the current directory (.) and the output will have its lines counted (wc -l). Spaces here are optional.  

More than one pipe at the same time for more complex commands such as:

Cat file1 file2 | grep chlorophyll | wc -l

In example above, the cat command will merge file1 and file2; grep will look for the word chlorophyll in the combined file; and wc -l will count the lines containing chlorophyll in the combined file.


 
## **For loop**

A built in command; start by defining for which files the loop will cycle through; type for, hit run (it won't execute because the shell knows that there's more to come, it will instead show the next prompt, >) then type "do" (hit run) type you're command whatever you want to do (hit run) then type "done". This means - for these files, do this and then be done. (Do and done indicate beginning and end of the commands built in the for loop.

## **History**

Shows a numbered list of the last several hundred commands; to rerun any command, type !number of command desired.

## Other commands
!$

!$ retrieves the last word of the last command

Ctrl R will let you search a command based on a keyword.

## **Ways to join commands together**

Pipe | output is used as next input

grep followed by $(); usage(example): grep 'chlorophyll' $(find . -name "*.dat")

the line above will search for and list (grep) filenames (-name) containing the word 'chlorophyll' from a list of .dat files ("*.dat") found (find) in the current directory (.); grep could be replaced by wc and the command will instead count and spit out the number of adjacent the filenames containing the word 'chlorophyll' instead of listing them. To count them all (not only the adjacent ones), do 
wc -l $(find . -name "*.dat") | sort -n

## Extract table columns

cut will isolate/extract (not eliminate or cut off) columns of interest from the rest of the table; if columns are delimited by special characters other than tab, you need to specify the delimiter; you also need to specify the column(s) you are interested in extracting;

> **usage: cut -d "," -f 2,3,4**

the line above will extract (cut) columns 2, 3 and 4 (-f 2,3,4) which are delimited by a comma (-d ",")

## Sort lines in a table

By default, sort will sort alphabetically starting with the first character of the first column - to do it based on another column use the flag -k

Can also sort based on unique entries, with the flag -u

## Uniq and sort

uniq will find unique entries - only the ones that are listed adjacently

sort will sort entries alphabetically by default or numerically with the flag -n (smallest to largest)

Sort and uniq can be piped to get unique entries in a file even if duplicate entries are not adjacent, using pipe and grep:

sort | uniq | wc 

Sort and uniq are often used together because uniq only selects duplicated values that are listed consecutively (uniq should read as "remove the repeated"); if you want to extract all unique entries regardless of their location, sort first (this will get all repetitions grouped together) and then use uniq to extract one of each.


## **Aliases**

Are temporary names or shortcuts for any long, complicated and often used set of commands; they are only valid for as long as the terminal window is open; to make them permanent, they need to be saved in .bash_profile; aliases are defined as:

Alias "myshortcut" command command command

Then to quickly run command command command, type "myshortcut"



## **Functions**

Are shortcuts for multiline commands; scripts are too, but they are saved in a file outside of the terminal while functions are defined within the terminal; so scripts need the shebang #! to remind the shell that they are programs while functions don't because they are already made in the shell; 

Are temporary and only valid for as long as the session is open; to make them permanent, they need to be saved in .bash_profile; functions are defined as:

> Myfunction () { insert commands here }

The curly brackets here are equivalent to 'do' and 'done' in the for loop built in function; similarly, once you type myfunction() { the shell understands there's more to come and you can hit return to get the continuing prompt rather than to run the function; this continues until you type the closing curling bracket, which is the same as 'done' and tells the shell you are done defining your function and can now run it.

Hint: echo within a function means 'print'


## **The $ character**

$ followed by () means "the variable inside ()"

> Example: echo $HOME will print the user home path /users/thaisbittar (the meaning of the variable HOME) in this case, while echo HOME will print the word HOME.

$1 means the first variable listed in the command line, $2 the second, $3 the third and so on. 

$@ means all the variables (used if you don't know how many variables you have)

> Examples (for loop):

> For item in $1 $2 $3 do...done, then in your command line, the first argument listed will replace $1, the second will replace $2 and the third will replace $3.

> For item in $@ do...done, then in your command line, list as many items as you want or use a wildcard (e.g., "\*.txt") and the for loop will cycle through all listed arguments (the advantage of $@ is that you don't need to know how many arguments you have ahead of time).



 
