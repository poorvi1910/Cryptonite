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
