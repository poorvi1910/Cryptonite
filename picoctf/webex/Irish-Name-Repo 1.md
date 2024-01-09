When we look at the Support page however, we see some inquiries, one of which states: I tried adding my favorite Irish person, Conan O'Brien. But I keep getting something called a SQL Error
This hints that we can use SQL injection. Using the 'OR 1==1-- payload can help
The SQL query to access the database is probably something like this:
SELECT username, password FROM users WHERE username='$username' AND password='$password';

Hence if i the admin field we use the above mentioned payload:
SELECT username, password FROM users WHERE username='admin' OR 1=1-- AND password='$password';

In this the 1==1 makes the condition true always and the -- at the end makes anything coming after it a comment hence eliminating the password field too. This gives us access to the site and the flag is printed
