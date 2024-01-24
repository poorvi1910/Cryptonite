When we click on the link provided we are shown a webpage with an image that leads us to another website. Viewing the source code also does not yield anything helpful. 

So i tried using robots.txt. A robots.txt file tells search engine crawlers which URLs the crawler can access on your site. This is used mainly to avoid overloading your site with requests and not a mechanism for keeping a web page out of Google.


Going to the site http://66.228.53.87:5000/robots.txt we can see the message:
Disallow : /l3v1_4ck3rm4n.html

Now that we have gotten an html page, we can visit it. Going to http://66.228.53.87:5000/l3v1_4ck3rm4n.html, we get the flag

Flag: KCTF{1m_d01n6_17_b3c4u53_1_h4v3_70}
