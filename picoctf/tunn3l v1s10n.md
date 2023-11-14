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
