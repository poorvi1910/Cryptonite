From the source code we can see that the code is randomly generating 100,000 users and assigning one of them to be admin </br></br>

const users = [...Array(100_000)].map(() => ({ user: `user-${crypto.randomUUID()}`, pass: crypto.randomBytes(8).toString("hex") }));
db.exec(`INSERT INTO users (id, username, password) VALUES ${users.map((u,i) => `(${i}, '${u.user}', '${u.pass}')`).join(", ")}`);</br></br>

I saw the below codelines and thought that sql injection would work so I tried a lot of payloads </br></br>
const query = `SELECT id FROM users WHERE username = '${user}' AND password = '${pass}';`;</br></br>

I tried using sqlmap to bruteforce the login but it didnt work. </br>

 I next saw the below code and checked out the login bypass tricks for pages that use redirects but that too didnt work out.
 
      if (!id) {
            return res.redirect("/?message=Incorrect username or password");
        }

        if (users[id] && isAdmin[user]) {
            return res.redirect("/?flag=" + encodeURIComponent(FLAG));
