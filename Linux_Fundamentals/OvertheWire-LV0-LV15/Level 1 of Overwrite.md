# Overthewire 0 > 15
## 
Congratulations on your first steps into the bandit game!!
## Level 0 >  1
Needed to exit intial SSH connection and badit1@host name instead and use password from first level 

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If[[ of Overwire]


## Level 1  >  2

### Goal

The password for the next level is stored in a file called - located in the home directory

Password - 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

T - Task

I had to open a file that was just named -. When I tried to open it normally, it didn't work. The computer just sat there waiting for me to do something else because it didn't realize I was talking about a file.
E - Evidence

I tried typing cat - but nothing happened. In Linux, when you type a dash, the computer thinks you want to type the information into the terminal yourself. It "ignores" the actual file named dash because it thinks the symbol is a special instruction.

D - Detail

To fix this, I had to be very specific about where the file was. I had to tell the computer, "Look right here in this folder for a file named dash."

    The Easy Fix: cat ./-

        The . means "Right here."

        The / is just a divider.

        The - is the file name.

    The Long Fix: cat /home/bandit1/- (This is just the full address of the file).


## Level 2 > 3

### Goal 
The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

Password - MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

T - Task

I had to read a password inside a file named --spaces in this filename--. Usually, when you put a space in a command, Linux thinks you are finished with the first word and moving on to the next.
E - Evidence

If I just typed cat --spaces in this filename--, the computer would give me an error saying it couldn't find a file called spaces, then it couldn't find a file called in, and so on. It "breaks" the name apart at every space.
D - Detail

To fix this, I had to "shield" the filename so the computer sees it as one single piece of text. There are two ways I did this:

    The Quote Method (The Shield): cat "--spaces in this filename--"

        Putting quotes around the name tells the computer: "Everything inside these marks is ONE file name."

    The Backslash Method (The Escape): cat \ \spaces\ in\ this\ filename--

        (The computer does this automatically if you hit the TAB key). The backslash tells Linux: "Ignore the special meaning of the next space."

## Level 3 > 4

password - 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ 

### Goal 

The password for the next level is stored in a hidden file in the inhere directory.

Had to use la command to find hidden files and use relative path to get to inherit directory. 



flags used - la find hidden files 

cat - concatenate file and prints to screen 

## Level 4 > 5

Password - 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

## The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

files stared with -- which means  had to use relative path again and then put file you want to open using cat at end of of path 

Alternative method

Used file to search directory and found file command tells you which file is human readable or otherwise. ASCII text is humand readable and stands for **ASCII** stands for **American Standard Code for Information Interchange**. 

I did this by using an astrix  at the end of the file path like this file /home/bandit4/inhere/ ./*



## Level 5 > 6

### The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

    human-readable
    1033 bytes in size
    not executable


Password - morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

Found I had to use the find command using specific flags to ensure I narrow down the search.  had to use user flag and size flag

Also has to ensure that files found with permissions denied were funneleld during search so it would be easier to find password file.

Also when using find feature search from root which is / 

When searching and permission to read certian files is denied this is due to the find feature searching everything and it put them into two catergories. by using this code this deletes the one which we do not have access to  '2>/dev/null'



## Level 7 > 8

 ## The password for the next level is stored in the file data.txt next to the word millionth

Password - dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

Used strings and piped it to  grep to find line containing millionth 



## Level 8 > 9

## The password for the next level is stored in the file data.txt and is the only line of text that occurs only once


Had to use sort which is sorting Alphabetical as standard.  

Used -n flag to sort numerically instead which worked in this situation. on the data.txt file and used the pipe to uniq which is lazy so only checks the line below it and doubled it up with -u flag to ensure it would look beyond just the line below

sort data.txt -n | uniq -u



You have the **Logic Chain** almost perfectly mapped out, but there is one small technical correction needed regarding how `uniq -u` works. Understanding this distinction is key to your "Autistic Logic" requirement of knowing exactly _why_ the machine does what it does.

### 1. What you got 100% Right

- **The Necessity of `sort`**: You correctly identified that `uniq` is "lazy." It only compares Line A to Line B. If the duplicates are spread out (Line 1 and Line 50), `uniq` will miss them. `sort` forces them to touch.
    
- **The Pipe (`|`)**: You are correctly using the "Conveyor Belt" to move data between tools.
    
- **The Result**: Your command `sort data.txt -n | uniq -u` will successfully isolate a single, non-repeated line.
    

---

### 2. The Correction: How `-u` actually works

You mentioned that you "doubled it up with the `-u` flag to ensure it would look **beyond just the line below**."

**This is a common misconception.** The `-u` flag does **not** make `uniq` look further down the file. `uniq` stays "lazy" no matter what flags you give it.

- **The `uniq` rule:** It _always_ only compares the current line to the next line.
    
- **The `-u` role:** This flag changes the **Filter**.
    
    - **Standard `uniq`**: "If I see three 'Apples', I will output **one** 'Apple'."
        
    - **`uniq -u`**: "If I see three 'Apples', I will output **nothing**. I only output lines that have no identical neighbor."
        

The reason it works is not because the flag made `uniq` smarter; it's because the `sort` command did the "heavy lifting" by grouping all identical lines together. Once they are grouped, `uniq`'s "lazy" one-line-at-a-time check is all that's needed to find the duplicates.

## Level 9 > 10


### The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

Password - 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
 
This level reuired me to use strings and grep commands to filter out the result reuiqred and used pipe method to get the result. 

I did this by firstly using the stringd command referencing the data.txt file and piped it to grep and referenced the string '=' which gave me the answer for this level.

## Level 10 > 11

## The password for the next level is stored in the file data.txt, which contains base64 encoded data

password - dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

Used the Base64 command and used the -d flag to encode the file and get the password  

## Level 11 > 12

### The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

Password - dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr 

Answer - cat data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'

I had to use the cat and tr commands together with a pipe to get the answer. cat simple opens the file and tr allows me to swap any charcater fro the first set with the second. As ROT13 rotates the alphabet by 13 places firstly state the alphabet in its typical format. 

Once thats been done you reference the second group which translates if you see an a chnage it to 13 letters after it and so on for each charcter until you get the result of the password. 


## Level 12 > 13

Password - 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

T - We had to use the cat command to open up the file and use a | 'pipe' to put the output into the tr command which uses the options and set1 and set 2 syntax to decifer the ROT13 password. ROT13 means the code has been scrambled by 13 characters alphabetically.  

E - The first set is replaced buy the second set which you use to change characters  based on the arguments which in this case is set1 and set2. 


D -  so for example if i you wanted to decipher it you would use the code cat data.txt | tr 'A-Za-z'(set 1) "N-ZA-Mn-za-m" and get the output of the password file. 

## Level 12 > 13 


Password - FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

**T (Task):** I had to use various decompression methods, as well as renaming files at each stage, while assigning each file to a designated name (such as "layer1").

**E (Evidence):** I achieved this by researching the syntax for **Gzip**, **Bzip2**, and **tar**. I used the foundations I built with the `file` command, which identified the file type and informed me which decompression tool was required for the next step.

**D (Detail):** This process required several levels of decompressing and repeating the steps above. Eventually, I reached `data8.bin`, which the system identified as **ASCII** (user-readable text).

## Level 13 > 14 

Password - MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

Task - The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level.


-T I Researched into SCP and found this allows you to transfer files from local login to another user using SSH.  Once in the system I then had to learn about **chmod** and user prioreties  and permissions. 


-D so logged in using the password from the last level and found a SSH.Private key file. Found this was RSA from the file command and logged out. 

Once out i used scp  which was scp -P 2220  scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private . 


Now that im logged in i used the chmod to change the file permission so only the owner could read write and execute and no one else. 


I then logged out and logged in using the -i flag whcih indicated i have the private key and changed my user to bandit 14 which allowed me to access this 

ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220


## Level 14 > 15 

### The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

-T I needed to utilise netcat command whlist inside the bandit 14

-E once connected to the local host i inputted the password and it gave me the correct password back for the next level 


-D Answer was nc localhost 30000 

