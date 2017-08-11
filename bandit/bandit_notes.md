This is for overthewire.org. 



Bandit 

Need to ssh into different levels@bandit.labs.overthewire.org

Level 0 - >>>ssh bandit0@bandit.labs.overthewire.org -p 2220 
>>>password: bandit0

level 1 - ssh badit1@same as level 0 
pass: boJ9jbbUNNfktd78OOpsqOltutMc3MY1

to exit an ssh, type exit. But if that doesn't work, try ctrl ~. or ctrl d. 
level 2 - so for this one, the passwd is in a file named -. doing cat - is for input. So, to read it, need to do cat ./- 

Flag - CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9 this'll get you into level 2.

level 2: So the file is named "spaces in the filename" ....Hm. 

Well, i just did cat spaces\t and it filled it in for me. It came up as: cat spaces\ in\ this\ filename
Flag - UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

Level 3: Apparently the next file is stored in a secret file in the _inhere_ directory (underscores is MD for italics. Wait, why am I not doing this on my github or in md?)
It came up as: cat spaces\ in\ this\ filename 
Flag: UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

Level 3 -> level 4: Alright, for this one, had to ssh into level 3. Then, cd into inhere. After that, ls -a for all the files. Can see there is a hidden file. so do
    cat .hidden 
And that should be the flag. 

Yep. pIwrPrtPN36QITSp3EQaw936yaFoFgAB

Level 4 -> Level 5: ssh'd in, wth. It's a bunch of files named -file00 up to -file09. But that is not the weird part, the weird part is if I do 
    cat ./-file00 
then it goes to this: 4bandit4@bandit:~/inhere$. Alright, weird. It is a bunch of question blocks on my terminal, maybe I can include a screenshot later. Okay, this is the content of -file01: ;gvW
bandit4@bandit:~/inhere$. The rest are similar up to -file07, which looks like the flag. Its output is: koReBOKuIDDepwhWk7jZC0RTdopnAYKh 

Can not be this easy, right? Let me look into what the file, du, and find commands do/how to use them. 

Okay, so file <filename> tests what kind of file it is. All of them are data except for -file07 which is ASCII text. 
du <filename> gives the size of the file. Can also do the file of a directory like du /home. Can also add the -h flag for human_readable format. du -a <directory> gives the usage of all the files. du -s <directory> for grand total disk usage size. du -ch <directory> gives total at last line. du -ah --exclude="*.txt" <directory> will exclude filetypes of .txt in the calculation. 
Syntax of the find command: find <startingpoint> <options> <search term>. startingpoint is the folder, for whole drive do find / <option> <search term>. Folder currently in: find . <options> <search term>. by name: find / -name my_file.txt
Start from home: find ~ -name game or whatever. Lots of flags, look them up later. Probably the reason people use find but whatever. How to find all exec/readable files: find / -exec/-read. Find and exectute a command against a file: find /-name filename -exec nano '{}' \; 
Look up what this does later. Also, file ./-* does the file of everything. Dang, use the * more often. 

Level 5 -> Level 6: ls -la lists all the files, even the hidden ones, and some stats. ls -a just lists the file names, including hidden ones. Alright, the hints to find it are that it is:
* human-readable 
* 1033 bytes in size - use du for this.  
* not executable. - tried doing find / -exec * for this and it says I am missing argument to -exec? 
did du -ah maybehere* to search all the directories, and looked for files that fit the 1033 byte description. K, can not really find one. 

MKAY SO find / -perm /u=r finds all the read only files, change / to directory or else it is root, or find inhere -perm /a=x for all the executables. 

So it is not an executable, so it cannot be: 
inhere
inhere/maybehere15
inhere/maybehere15/spaces file3
inhere/maybehere15/spaces file1
inhere/maybehere15/.file1
inhere/maybehere15/-file3
inhere/maybehere15/.file3
inhere/maybehere15/-file1
inhere/maybehere07
inhere/maybehere07/spaces file3
inhere/maybehere07/spaces file1
inhere/maybehere07/.file1
inhere/maybehere07/-file3
inhere/maybehere07/.file3
inhere/maybehere07/-file1
inhere/maybehere08
inhere/maybehere08/spaces file3
inhere/maybehere08/spaces file1
inhere/maybehere08/.file1
inhere/maybehere08/-file3
inhere/maybehere08/.file3
inhere/maybehere08/-file1
inhere/maybehere13
inhere/maybehere13/spaces file3
inhere/maybehere13/spaces file1
inhere/maybehere13/.file1
inhere/maybehere13/-file3
inhere/maybehere13/.file3
inhere/maybehere13/-file1
inhere/maybehere11
inhere/maybehere11/spaces file3
inhere/maybehere11/spaces file1
inhere/maybehere11/.file1
inhere/maybehere11/-file3
inhere/maybehere11/.file3
inhere/maybehere11/-file1
inhere/maybehere16
inhere/maybehere16/spaces file3
inhere/maybehere16/spaces file1
inhere/maybehere16/.file1
inhere/maybehere16/-file3
inhere/maybehere16/.file3
inhere/maybehere16/-file1
inhere/maybehere10
inhere/maybehere10/spaces file3
inhere/maybehere10/spaces file1
inhere/maybehere10/.file1
inhere/maybehere10/-file3
inhere/maybehere10/.file3
inhere/maybehere10/-file1
inhere/maybehere05
inhere/maybehere05/spaces file3
inhere/maybehere05/spaces file1
inhere/maybehere05/.file1
inhere/maybehere05/-file3
inhere/maybehere05/.file3
inhere/maybehere05/-file1
inhere/maybehere17
inhere/maybehere17/spaces file3
inhere/maybehere17/spaces file1
inhere/maybehere17/.file1
inhere/maybehere17/-file3
inhere/maybehere17/.file3
inhere/maybehere17/-file1
inhere/maybehere04
inhere/maybehere04/spaces file3
inhere/maybehere04/spaces file1
inhere/maybehere04/.file1
inhere/maybehere04/-file3
inhere/maybehere04/.file3
inhere/maybehere04/-file1
inhere/maybehere06
inhere/maybehere06/spaces file3
inhere/maybehere06/spaces file1
inhere/maybehere06/.file1
inhere/maybehere06/-file3
inhere/maybehere06/.file3
inhere/maybehere06/-file1
inhere/maybehere00
inhere/maybehere00/spaces file3
inhere/maybehere00/spaces file1
inhere/maybehere00/.file1
inhere/maybehere00/-file3
inhere/maybehere00/.file3
inhere/maybehere00/-file1
inhere/maybehere18
inhere/maybehere18/spaces file3
inhere/maybehere18/spaces file1
inhere/maybehere18/.file1
inhere/maybehere18/-file3
inhere/maybehere18/.file3
inhere/maybehere18/-file1
inhere/maybehere01
inhere/maybehere01/spaces file3
inhere/maybehere01/spaces file1
inhere/maybehere01/.file1
inhere/maybehere01/-file3
inhere/maybehere01/.file3
inhere/maybehere01/-file1
inhere/maybehere02
inhere/maybehere02/spaces file3
inhere/maybehere02/spaces file1
inhere/maybehere02/.file1
inhere/maybehere02/-file3
inhere/maybehere02/.file3
inhere/maybehere02/-file1
inhere/maybehere19
inhere/maybehere19/spaces file3
inhere/maybehere19/spaces file1
inhere/maybehere19/.file1
inhere/maybehere19/-file3
inhere/maybehere19/.file3
inhere/maybehere19/-file1
inhere/maybehere14
inhere/maybehere14/spaces file3
inhere/maybehere14/spaces file1
inhere/maybehere14/.file1
inhere/maybehere14/-file3
inhere/maybehere14/.file3
inhere/maybehere14/-file1
inhere/maybehere09
inhere/maybehere09/spaces file3
inhere/maybehere09/spaces file1
inhere/maybehere09/.file1
inhere/maybehere09/-file3
inhere/maybehere09/.file3
inhere/maybehere09/-file1
inhere/maybehere03
inhere/maybehere03/spaces file3
inhere/maybehere03/spaces file1
inhere/maybehere03/.file1
inhere/maybehere03/-file3
inhere/maybehere03/.file3
inhere/maybehere03/-file1
inhere/maybehere12
inhere/maybehere12/spaces file3
inhere/maybehere12/spaces file1
inhere/maybehere12/.file1
inhere/maybehere12/-file3
inhere/maybehere12/.file3
inhere/maybehere12/-file1

Good to know. Can I fit all the find criteria into one find command? maybe 
    find inhere -size 1033c 
Googled it and found: 
    find . -type f -size 1033c -name "[[:print:]]*" ! -executable 
But that seems to be for the same reason lol. At least I know the ! operator works now. 
I did: 
    find inhere -size 1033 c ! -executable 
and it came out with inhere/maybehere07/.file2 
After doing cat ./.file2 I got: DXjZPULLxYr17uwoI01bNLQbtFemEgo7
Sweet. reset also resets the terminal. 

Level 6 -> Level 7: passwd on the server is stored somewhere and is owned by user bandit7, owned by group bandit6 \n and is 33 bytes in size. Look up how to find based on groups. It also suggests to use grep, so I will learn how to use that. Log in with: 
    bandit6@bandit.labs.overthewire.org -p 2220
Okay, so grep is used to search text or searches given file for lines containing a match to the given strings or words. Displays matching lines by default. Can use it to search for many regExs, and outputs only matching lines, one of the most useful commands. 
Syntax: grep 'word' filename OR grep 'word' file1 file2 file3 file* OR grep 'string1 string2' filename OR cat somefile | grep 'something' or command option1 | grep 'something' OR grep --color 'data' fileName OR command option1 | grep 'data'

The command: 
    grep boo /etc/passwd
searches /etc/passwd file for boo, can add -i to try and output boo, Boo, BOO, etc. 
The command: 
    grep -r "ADSF" /etc/ searches each file under each directory for "ASDF". Capital -R works too. 
- can use the -h or -hR command to omit filenames. 
- to match the whole word, do -w b/c without it, the boo thing up there will find boo123, etc. 
Can use: 
    egrep -w 'word1|word2' /path/to/file 
to search for 2 whole words. 
Use: 
    grep -c 'word' /path/file 
in order to count the number of times it's matched, use the -n opttion to precede each line of output with the number of the line in the text file from which it's obtained. 
    grep -v bar /path/to/file
Matches all the lines that DO NOT contain the word bar. grep -l 'main' *.c lists all files with a main() in it. 
    grep --color vivek /etc/passwd 
colors the word given. 
GREP with REGEX!
    grep -E -i -w 'vivek|Raj' /etc/passwd will search raj or vivek in any case. 
Can basically use regex patterns instead of words.
    grep 'foo$' filename 
finds files that only end in foo, but ^ in front of foo without $ to find files only starting with foo, put both to find filenames with just those. Grep RegEx shortcuts: 
[:alnum:] - Alphanumeric characters.
[:alpha:] - Alphabetic characters
[:blank:] - Blank characters: space and tab.
[:digit:] - Digits: 0 1 2 3 4 5 6 7 8 9.
[:lower:] - Lower-case letters: a b c d e f g h i j k l m n o p q r s t u v w x y z.
[:space:] - Space characters: tab, newline, vertical tab, form feed, carriage return, and space.
[:upper:] - Upper-case letters: A B C D E F G H I J K L M N O P Q R S T U V W X Y Z.

Use {1,3} for greater than 1 or no more than 3 times, then use \. to put actual dots instead of anything metacharacter. egrep is the same as grep -E. It interprets PATTERN as an extended regEx. 

Can use
    find 
in order to list current directory and sub-directory. Same as find . or find . -print
    find ./test
lists all files in current directory. Can also do -not -name "*.txt" to get rid of .txt files. -o is the or operator. Can also do 
    find ./test -name 'abc*' ! -name '*.php' 
combines search criteria. 
    find ~ -type f -name ".*"
lists all idden files. Can also type: 
    find . -type f -perm 0664 OR find . -type f ! -perm 0777 
to find files of a certain permission or NOT of a certain permission. 
    find /etc -maxdepth 1 -perm /u=r
finds all the readonly files. 
    find . -user bob 
finds all the files by bob, or 
    find . -user bob -name '*.php' 
to find criteria. 
For files belonging to a different group: 
    find /var/www -group developer. 
Size: 
    find / -size 50M 
for all files 50MB 
    find / -size +50M -size -100M 
For all files greater than 50 MB but smaller than 100 MB. 

Okay time to actually do the challenge lol 
    find . -user bandit7 -group bandit6 -size 33c
Crap, been trying this one in different places. Didn't reach any conclusions. However, I never bothered to cd .. so now i'm in root. Let us try this command in different places. Alright, getting a lot of permission denied. How to get rid of them...  

Okay found it, it's the third one, but there's a better way to do this. Apparently find puts stuff in stdout and in order to put errors like permission denied away, can either grep them away or add 2>/dev/null because dev/null is where we put stuff we do not like. 

final command: 
    find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
Then doing: 
    cat /var/lib/dpkg/info/bandit7.password
yields: 
    HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
Great. That is the password to get into bandit7@bandit.labs.overthewire.org -p 2220 
That took way longer than I thought it would. I learned about grep and the 2>/dev/null thing. 

Level 7 -> Level 8: 

Okay so there is a file named data.txt, cat'd it, and there's a bunch of words with flags next to them. Hint is that the flag is sotred next to the word millionth. Should just be a simple: 
    grep millionth data.txt 
I hope. Yep. Yields: cvX2JJa4CFALtqS87jk27qwqGhBM9plV to ssh bandit8@bandit.labs.overthewire.org -p 2220

They suggesting using uniq, base64, tr, tar, gzip, bzip2, and xxd though. So ima have to read them and figure out what they do. 

Level 8 -> Level 9: 
Hint is it's the only line of text that occurs only once...so a unique line in the file? Alos says helpful reading materials are pipes and redirects. Gonna have to read those too. 

lol cat'ing it yields a ton of flags. Apparently this will sort stuff based on number of appearences, with piping, thanks stack overflow, got to this page when searching "uniq linux command". 
    sort FILE | uniq -c | sort -n
Look at the reading here: http://www.westwind.com/reference/os-x/commandline/pipes.html
running the Stackoverflow command yields: wow. Apparently the flag appears once and everyhing else appears ten times. 
Flag for ssh bandit9@bandit.labs.overthewire.org -p 2220 is UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
Got to do these readings! 

Level 9 -> Level 10: 

