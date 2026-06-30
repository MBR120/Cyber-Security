Task 1 

What Nmap scanning switch employs the use off default scripts during a scan ? 

Answer - sC 

Upon scanning the network I find there is most notably port 21 is open which is TCP and could indicate this is a websiite. 


Task 2 

What service is found to running on port 21 ? 

Answer - vsftpd 3.0.3 

As shown in the image below it shopws the active service and version running on port 21 

![Nmap scan Results](/home/user/Fundamentals/Reference_Images/Screenshots/Screenshot_20260507_150209.png)

Task 3

What FTP code is returned to us for the "Anonymous FTP login allowed" message?

Answer - 230 

As Shown below when loggin in Anonymously as was indiacated in the inital scan it shows 230 which indicates loging in was succesful 

Task 4

After connecting to the FTP server using the ftp client, what username do we provide when prompted to log in anonymously?

Answer - Anonymous 

![Shows 230 Login code](/home/user/Fundamentals/Reference_Images/Screenshots/Screenshot_20260507_191934.png)

Task 5

After connecting to the FTP server anonymously, what command can we use to download the files we find on the FTP server?

Answer - get 

As shown below once inside the ftp server i used the get method for the files shown in the image which had user names and passwords in them, 

![get method ](/home/user/Fundamentals/Reference_Images/Screenshots/Screenshot_20260507_192550.png)

Task 6

What is one of the higher-privilege sounding usernames in 'allowed.userlist' that we download from the FTP server?

Answer - Admin

![usernames](/home/user/Fundamentals/Reference_Images/Screenshots/Screenshot_20260507_192845.png)

Task 7

What version of Apache HTTP Server is running on the target host?


Answer - Apache httpd 2.4.41 

As shown from intial scan from first task. 

Task 8

What switch can we use with Gobuster to specify we are looking for specific filetypes?

Answer - x 

Task 9

Which PHP file can we identify with directory brute force that will provide the opportunity to authenticate to the web service?

Answer - login.php

As shown below this flag helps filter the specific files relevant to the enumaration we have been doing as shown below it specifies a login.php file which is very useful for the next steps

![Gobuster findings](/home/user/Fundamentals/Reference_Images/Screenshots/Screenshot_20260507_203632.png)
 
 
 Step 10 (extra step)
 
 To automate logins for the website i had to find a the format compatible with hydra to automatethe logins by using curl.

 curl -s http://[IP]/login.php

 This then showed the internal names for the input boxes for the login 

 <input name="Username" ...>

<input name="Password" ...>

<button name="Submit" value="Login" ...>

If the HTML says name="User", your Hydra command must use User=^USER^. If it says name="email", you must use email=^USER^. Web servers are extremely picky; if you use lowercase username when the code says Username, the server will ignore your request entirely.
 
 Step 2: Mapping the Hydra Syntax

The Hydra http-post-form module follows a very specific "three-part" structure separated by colons.

"/path/to/page:form_data:failure_or_success_condition"
Part A: The Path

This is simply the URL location, like /login.php or /admin/index.php.
Part B: The Form Data (The "Payload")

This is where we bridge the gap between your files and the website.

    We take the names we found in Step 1: Username, Password, and Submit.

    We use the Hydra placeholders ^USER^ and ^PASS^ (always uppercase).

    We join them with ampersands (&).

    Result: Username=^USER^&Password=^PASS^&Submit=Login

Part C: The Condition (The "Stop Sign")

This tells Hydra how to know if it got the password right.

    F= (Failure): Look for a message that only appears when you fail (like "Incorrect Password").

    S= (Success): Look for a message or a status that only appears when you win (like "Welcome" or "Dashboard").

The Lesson: Using S= (Success) is usually more reliable because it is easier to identify the "Victory" page than to guess exactly what the "Error" message says.
Step 3: Putting it all together

By combining these observations, your final command became a precise reflection of the website's own code:

hydra -L users.txt -P pass.txt [IP] http-post-form "/login.php:Username=^USER^&Password=^PASS^&Submit=Login:S=Dashboard"
Key Takeaways for Future Targets

    Case Sensitivity: Always match the name="Value" from the HTML exactly (Capitals matter!).

    Don't Forget the Button: If there is a name="Submit" in the HTML, include it in your Hydra string.

    Verify with curl: Never start a brute-force attack without seeing the source code first. It saves hours of troubleshooting.Step 2: Mapping the Hydra Syntax

The Hydra http-post-form module follows a very specific "three-part" structure separated by colons.

"/path/to/page:form_data:failure_or_success_condition"
Part A: The Path

This is simply the URL location, like /login.php or /admin/index.php.
Part B: The Form Data (The "Payload")

This is where we bridge the gap between your files and the website.

    We take the names we found in Step 1: Username, Password, and Submit.

    We use the Hydra placeholders ^USER^ and ^PASS^ (always uppercase).

    We join them with ampersands (&).

    Result: Username=^USER^&Password=^PASS^&Submit=Login

Part C: The Condition (The "Stop Sign")

This tells Hydra how to know if it got the password right.

    F= (Failure): Look for a message that only appears when you fail (like "Incorrect Password").

    S= (Success): Look for a message or a status that only appears when you win (like "Welcome" or "Dashboard").

The Lesson: Using S= (Success) is usually more reliable because it is easier to identify the "Victory" page than to guess exactly what the "Error" message says.
Step 3: Putting it all together

By combining these observations, your final command became a precise reflection of the website's own code:

hydra -L users.txt -P pass.txt [IP] http-post-form "/login.php:Username=^USER^&Password=^PASS^&Submit=Login:S=Dashboard"
Key Takeaways for Future Targets

    Case Sensitivity: Always match the name="Value" from the HTML exactly (Capitals matter!).

    Don't Forget the Button: If there is a name="Submit" in the HTML, include it in your Hydra string.

    Verify with curl: Never start a brute-force attack without seeing the source code first. It saves hours of troubleshooting.
![Hydra brute force](/home/user/Fundamentals/Reference_Images/Screenshots/Screenshot_20260508_171749.png)
 

 
 Submit flag 

Answer - 

![shows login to website and flag is on homepage](/home/user/Fundamentals/Reference_Images/Screenshots/Screenshot_20260508_170608.png)
 