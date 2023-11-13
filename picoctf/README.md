REVERSE ENGINEERING

Keygenme-py          30
We have been given  python code which basically is a menu driven program that works as an arcane calculator and theres a key you need to input to get access to the full version. We are checking the input key against the predefined key character by character.We have been give the static part of the key that is "picoCTF{1n_7h3_|<3y_of_" and the third part “}”. To find dynamic part:

hashlib.sha256(username_trial).hexdigest():
hashlib.sha256 is a function from the hashlib module in Python that applies the SHA-256 hashing algorithm to the provided input.
username_trial is a string representing the username.
.hexdigest() converts the hash object to a hexadecimal representation.

The result of the hash is a string of characters (hexadecimal).
[4] is used to access the character at index 4 of the hexadecimal string. This is a specific character of the hash.

Hence the line is checking whether the i-th character of the key string is not equal to the character at index 4 of the hexadecimal representation of the SHA-256 hash of the username.
	
	So to get the key we can just print what the hashlib function does 




Combing all the key parts we get the flag:
picoCTF{1n_7h3_|<3y_of_e584b363}

GDB Baby Step 1       100


ARMssembly 0           40





BINARY EXPLOITATION

Stonks                20


babygame01             100


buffer overflow 0        100






WEB EXPLOITATION

caas                               150
When we click on the website link we get the following:

Displaying the javascript file, we can see the below code:

The code is a simple Node.js application using the Express framework. This application serves static files from the "public" directory and has a single route that allows you to trigger the "cowsay" command with a message and return the output as plain text.

Here's a breakdown of the code:

1. First, it imports the necessary modules: `express` for creating a web server, and `child_process` to run shell commands.

2. An Express application is created using `express()` and stored in the `app` variable.

3. The `express.static` middleware is used to serve static files from the "public" directory. This means that any files in the "public" directory will be accessible via the web server.

4. The `app.get` method defines a route for handling GET requests to "/cowsay/:message". It uses a parameter ":message" to capture the message you want to pass to the "cowsay" command. When a request is made to this route, it uses the `exec` function to run the "cowsay" command with the provided message. The `{timeout: 5000}` option specifies a timeout of 5 seconds for the command execution. If an error occurs during command execution, it responds with a 500 status code. If the command executes successfully, it sets the response content type to plain text and sends the output from the "cowsay" command as the response.

5. Finally, the Express application listens on port 3000, and a message is logged to the console when the server starts.

To use this application, you can navigate to http://localhost:3000/cowsay/YourMessage in your web browser, replacing "YourMessage" with the message you want the cow to say. The "cowsay" command is executed with your message, and the cow's response is displayed in plain text in your browser.

Using curl command(curl is a command-line tool to transfer data to or from a server, using any of the supported protocols (HTTP, FTP, IMAP, POP3, SCP, SFTP, SMTP, TFTP, TELNET, LDAP, or FILE):


Curl is a command-line tool that can send and receive HTTP requests and responses
Since curl is specifically developed for HTTP requests it already uses the appropriate line-endings when making HTTP requests. However, netcat is a more general purpose program.

We now need to perform OS command injection to obtain the files we need

OS command injection is also known as shell injection. It allows an attacker to execute operating system (OS) commands on the server that is running an application, and typically fully compromise the application and its data.

The file ‘falg.txt’ looks like our desired file. So we can cat it out and check
Initially i put the injected command ‘cat flag.txt’ but it the following error:

This is because URLs cannot contain spaces. URL encoding normally replaces a space with a plus (+) sign or with %20.Doing that:


We get the flag:
picoCTF{moooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo0o}

What is OS command injection:
https://portswigger.net/web-security/os-command-injection


Forbidden paths           200

When we go to the website, type in file.txt and read, we get an expected error of ‘File does not exist’.

The description mentioned that we are now located at /usr/share/nginx/html/, and flag is stored in  /flag.txt. So we can use path traversal. Path traversal is also known as directory traversal. These vulnerabilities enable an attacker to read arbitrary files on the server that is running an application. To achieve this, we use   ../ to travel to the upper layer.
We need to go back 4 layers to travel back to the home directory, so we need to modify the filename section to ../../../../flag.txt


When we click on read now, we get the flag:
picoCTF{7h3_p47h_70_5ucc355_e5a6fcbc}

What is path traversal:
https://portswigger.net/web-security/file-path-traversal


Local Authority             100
Hint tells us to look at how the password input is being taken
Viewing page source of the website we get the following:

Clicking on style.css we get the following code

We get nothing useful here. So we go back to the website and enter any random username and password and as expected the login fails.But if we view the source of the log in failed page we get the following: 

We can see a javascript file ‘secure.js’ here. Clicking on it we get the below code:

Hence we now have our login username and password.Entering these in the website, we get the following flag:
picoCTF{j5_15_7r4n5p4r3n7_05df90c8}



FORENSICS

tunn3l v1s10n             40
Putting the image in a hex editor, we get file signature as 42 4D which corresponds to a BMP file. Adding a ‘.bmp’ extension to the file and opening it in an online editor like Photopea, we get the following image

The image does not look like it is displaying completely, so we can go to hex editor and change the height to equal the width(as width is more)

Original header:

Changed header(4 bytes starting from offset 16):

On doing so we get the following image

On further changing dimensions we can get more and more of the image but we can stop since we have gotten our flag.

We have hence gotten our flag which is:
picoCTF{qut3_a_v13w_2020}

How hex offsets work:
https://stackoverflow.com/questions/141262/can-someone-explain-hex-offsets-to-me



Trivial FTP                   90


Opening instructions.txt we get the following cipher:
GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA

Using ROT13 on the cipher and adding space between words:
TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER.FIGURE OUT A WAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN

Doing the same for plan.txt :
I USED THE PROGRAM AND HID IT WITH-DUE DILIGENCE.CHECK OUT THE PHOTOS

On running the program.deb file, it opens up a package installer for steghide

Steghide is steganography program which hides bits of a data file in some of the least significant bits of another file in such a way that the existence of the data file is not visible and cannot be proven.
Steghide is designed to be portable and configurable and features hiding data in bmp, jpeg, wav and au files, blowfish encryption, MD5 hashing of passphrases to blowfish keys, and pseudo-random distribution of hidden bits in the container data.

Installing the package and running the command on the three images using ‘DUEDILIGENCE’, we get no output for first 2 images 

But the third image:


Using cat command on the flag.txt file, we get the flag:
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}


Macrohard Weakedge     60
We have been given a pptm file over here. 
Checking file details there is nothing useful found:

Hence we can convert the file to a zip instead by changing extension to ‘.zip’ instead of ‘.pptm’ and sorting through the files, we come across a file named ‘hidden’

Opening the hidden file we get the cipher below:
Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q

Since there are uppercase, lowercase AND digits in the license, it might be base64 encoded
Decoding through base64 we get:

flag: picoCTF{D1d_u_kn0w_ppts_r_z1p5}



CRYPTOGRAPHY

new caesar             60


miniRSA                  300


mod1 
The text file contains the following:
350 63 353 198 114 369 346 184 202 322 94 235 114 110 185 188 225 212 366 374 261 213 

Applying mod 37 on each number: [remainder when number is divided by 37]
17 26 20 13 3 36 13 36 17 26 20 13 3 36 0 3 3 27 33 4 2 28
		
Given, alphabets are coded 0-25 and numbers are as follows:
0    1   2   3   4   5   6   7   8   9   _
26 27 28 29 30 31 32 33 34 35 36

Using the above we get the flag:
r0und_n_r0und_add17ec2


mod2          
The text file contains the following:
104 372 110 436 262 173 354 393 351 297 241 86 262 359 256 441 124 154 165 165 219 288 42


Applying mod 41 on each number: [remainder when number is divided by 41]
22 3 28 26 16 9 26 24 23 10 36 4 16 31 10 31 1 31 1 1 14 1 1
  
Finding modular inverse of above numbers:[using any online tool]
28 14 22 30 18 32 30 12 25 37 8 31 18 4 37 4 1 4 1 1 3 1 1

Given, alphabets are coded 1-26 and numbers are as follows:
27 28 29 30 31 32 33 34 35 36 37
 0   1   2   3   4   5   6   7   8   9   _

Using the above we get the flag:
1nv3r53ly_h4rd_dadaacaa


PRACTICE

Information (forensics)
exiftool is a tool used to display all details about a jpg file and since the hint mentions that we might need to do this, hence we can run this command on the image

Since there are uppercase, lowercase AND digits in the license, it might be base64 encoded
Decoding through base64 we get:
picoCTF{the_m3tadata_1s_modified}

Insp3ct0r (Webex)
Viewing source code of the website:

We have one part of the flag
Clicking on the mycss.css and myjs.js links:



We have part 2 and 3 of the flag also:
flag: picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?2e7b23e3}

advanced-potion-making (forensics)
We have been given a file here called advanced-potion-making. When we try to open the file it gives unknown file type error. Hence we can put the file in a hex editor to check the file header to see what type of file it is. 

On searching the wikipedia page of file signatures starting with 89 50:

What is interesting is only 2 bytes of the signature do not match the expected format. Hence we can change the header

Now saving the file and running it gives an error of invalid IHDR length
https://en.wikipedia.org/wiki/PNG
Using this wikipedia page and understanding the IHDR format helped a lot

This mentions that IHDR needs to be 13 bytes in size and the header size makes up the first 4 bytes that is 00 00 00 0D
Howeve r when we look at our file we can see that the header size part shows 
00 12 13 14. This is why we were getting invalid header size error. Changing the values:

Now we can save this file(along with .png extension) we can see that we now have an uncorrupted png file that shows solid red colour rectangle
This hints to using a steganography tool which can filter colours to extract our flag




It is used to analyze images in different planes by taking off bits of the image.

To install:
$ wget http://www.caesum.com/handbook/Stegsolve.jar -O stegsolve.jar
$ chmod +x stegsolve.jar
$ mkdir bin
$ mv stegsolve.jar bin/

Running the stegsolve.jar file using:
$ java -jar stegsolve.jar

We get a popup application which allows us to upload a file and view it through different fileters. While going through the filters, the red plane 0 finally works and display our flag

picoCTF{w1z4rdry}

https://book.hacktricks.xyz/crypto-and-stego/stego-tricks


