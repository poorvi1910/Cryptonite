Hint tells us to look at how the password input is being taken
Viewing page source of the website we get the following:

Clicking on style.css we get the following code

We get nothing useful here. So we go back to the website and enter any random username and password and as expected the login fails.But if we view the source of the log in failed page we get the following: 

We can see a javascript file ‘secure.js’ here. Clicking on it we get the below code:

Hence we now have our login username and password.Entering these in the website, we get the following flag:
picoCTF{j5_15_7r4n5p4r3n7_05df90c8}
