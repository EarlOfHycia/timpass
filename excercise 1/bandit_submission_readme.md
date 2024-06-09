# solution document

## **level 0**
 
used the following ssh command to login into the bandit server.

*ssh -p 2220 bandit0@bandit.labs.overthewire.org*

the password is bandit0 as mentioned on the website.

## **level 0->1**

in level0 used the *ls -a* command to display the all the files/directories in the working directory.

on using the command

*cat readme*  

we get the password to access bandit1 directory in the the server.

password for bandit1 is NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

## **level  1->2**

in bandit1, password is within the file '-'. as '-' is a special character used to add optional arguments, we cannot directly access the contents of the file with the 

*cat -* 

command.

so we need to specify that '-' is a file in the working directory.
to do that we use the command 

*cat ./-*

where the '.' means the working directory '/' means to access whatever is mentioned in the path mentioned in the command.

password for bandit2 is rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

## **level 2->3**

in bandit2, password is within a file "spaces in this filename", we cannot get the password by simply using the command *cat spaces in this filename* as cat treats each string separated by a whitespace as a different argument and hence to specify that it is the name of a single file, we put the entire name within quotes.
the command is 

*cat "spaces in this filename"*

password is aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

## **level 3->4**

in bandit3, we use the *cd inhere* command to change the working directory to inhere. as mentioned on the website that password is in a hidden file, we cannot simply use the *ls* command as it only displays the visible files.
to display all files (including hidden), we use the command 

*ls -a*

we observe that there is a hidden file by the name ".hidden".
use the *cat .hidden* command to get the password

password is 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

## **level 4->5**

in bandit4, in the inhere directory, we have many files but as mentione don the website that only one of them is human readaable file, so we use the *file ./** command to get the filetype of all the visible files in the working directory. the '*' is a way to global placeholder for anything. we come to know that '-file07' is human readable as it contains ASCII text. use the *cat ./-file07* command to get the password.

alternate method

use the command,

*find . -readable* 

password is lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

## **level 5->6**

in bandit 5, in the inhere directory we have many directories, which themselves have many files. so it is not possible to manually go through them. so we need to use the find command. also it is mentioned on the site that the password is in a file that is human readable , has a size of 1033 bytes and is not execubtable.

so we us the command,

*find . -readable -size 1033c !-executable*

here -readable options specifies that the file is human readable i.e it contains ASCII text
-size 1033c options mentions that it is 1033 bytes in size ('c' mentions that it is in bytes)
! -executable options specifies that it is not executable.

password is P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

## **level 6->7**

in bandit6, it is mentioned on the website that the file containing the password can be present anywhere on the server, it is possible that the file may not be in the home directory of the user. so we need to search from the 'root' directory. so according to the properties the file of interest has as mentioned on the website,

we use the command,

**find / -size 33c -user bandit7 -group bandit6*

here, '/' means that the search starts from the root directory, -user and -group options specify the user and group owners of the file.

on using the command we get a lot of permission denied prompts, but one of them specifies the path which the current user has access to , file named bandit7.password.

on cat_ing

password is P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

## **level 7->8**

in bandit7, as mentioned on the website that the pass word is in a file called data.txt next to the word millionth,
we use the command,

*grep "millionth" data.txt*

the grep basically searches for patterns/text in a file.

passwoed is TESKZC0XvTetK0S9xNwm25STk5iWrBvP

## **level 8->9**

in bandit 9, as mentioned in the website the the password is in a file named data.txt and is the line of text that occurs only once in the file

we can dfind the this line using the uniq command but, it only works when the data is sorted as it comapares a line of text and the one next to it.

so we us the command,

*sort data.txt | uniq -c*

here the '|', "tube/pipe operator" pipes the output of the sort command into the input of the uniq command. '|' is powerful tool chain commands in command/shell prompts. -c option of the uniq command mentions the amount of times the line has been encountered in the sorted data.

password is EN632PlfYiZbn3PhVK3XOGSlNInNE00t

## **level 9->10**

in bandit9, as mentioned on the website the password is in the file data.txt and is one of the few human readable lines preceded by a bunch '=' chahracters. we first use the command,

*grep "==" data.txt*

but we get a binary file matches prompt.

so to get the ASCII text matches, we use the command,

*strings data.txt | grep "=="*

password is G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

## **level 10->11**

in bandit10,as mentioned in the website, the password is in a base64 encoded file data.txt, so we use the command.

*base64 -d data.txt*

base64 command is used to deal with data encoded in base64 and the -d option specifies to decode the data.

password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

## **level 11->12**

in bandit11, as mentioned in the website the password is in a file named data.txt but the data has been encrypted using a substitution cipher or Caeser cipher of 13 shifts to be specific.

so we use the tr command to get the password. the command is 

*cat data.txt | tr ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm*

the tr command translates the text piped in by cat command according to the substitution mentoined in the options of the tr command

password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

## **level 12->13**

in bandit12, as mentioned in the website that the password is in a hexdump of a repeatedly compressed file called data.txt

also due to no write permissions in the home directory,we make a temporary working directory in /tmp directory to carry out decompression.the commands are,

*cd /tmp*

*mkdir eoh123*

*cd*

*cp data.txt /tmp/eoh213*

*xxd -r data.txt data2.txt*

xxd command with -r option creates a reverse dump and stores it in the data2.txt file

now we repeatedly check the file type using the *file* command, modify the filenames accordingly for the decryption using the *mv* command and use the *gunzip* , *bunzip2* and *tar -xf* commands as per requirement.

following are some screenshots of my terminal while doing the exercise...(i am too lazy to explain all of it in text)

![screenshot1](https://drive.google.com/file/d/1zLz6BKkdOPteDtDeoR0yaCM9kSKcWdeX/view?usp=share_link)

![screenshot2](https://drive.google.com/file/d/1zSa4VEuaG6GZQwSLD84a8wdEPKbtwrZP/view?usp=share_link)

![screenshot3](https://drive.google.com/file/d/1zUTH0nXRO3erXoIgcGnyIKhEywQWX_dL/view?usp=share_link)

![screenshot4](https://drive.google.com/file/d/1za2GSbTra-F7nnrHjiEFuZxzk_6cpnFU/view?usp=share_link)

password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

## **level 13->14**






 
g