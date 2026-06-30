Three is a very easy Linux machine featuring a website using a misconfigured AWS S3 bucket as its cloud-storage device. The machine explores web application enumeration and subdomain fuzzing to detect the hidden domain corresponding to the S3 bucket. Then it showcases using the AWS command line interface to access the vulnerable S3 bucket as well as how to exploit it by uploading and triggering a reverse shell.


Task 1

How many TCP ports are open?

Answer - 2

As shown below i performed an Nmap Scan to see the open ports. 

Flags 

-sC Runs the defalt scrips against the target including Automated scanning for commond vulnerablities and extra information on this.

-sV Tells you what version or type of software running on the opens ports found. 

-Pn Skips pining request usually carried out 

-oA - The -oA flag handles your output and documentation, which is vital for keeping a clean record. This flag requires you to provide a filename directly after it, and Nmap will automatically generate three different files containing your results. One is a normal text file that looks just like your terminal output, one is an XML file that can be easily imported into other security tools, and the third is a "grepable" format, which makes it incredibly easy to search through using command-line filters if you are dealing with a massive amount of data.

Task 2

What is the domain of the email address provided in the "Contact" section of the website?
