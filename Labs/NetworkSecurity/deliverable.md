Lab 8 Deliverable:<br><br>
Vulnerability 1, Cross-Site Request Forgery (CSRF):<br>
Issue found(and description): <br>A client user does not have to actually sign in or sign up(and so on) at the Bananama Page, for example,
they can just make a post request via different ways to pretend to be the user(I believe one of the ways is using `curl`
command in terminal) to complete these tasks.<br>
To fix it:<br> Include an unpredictable token with such HTTP requests.<br><br>
Vulnerability 2, Client Side Validation:<br>
Issue found(and description): <br>While signing up, it allows the user to omit the enter of Beta sign up code after they failed the sign up once.<br>
(i.e., the validation of beta code only functions at the first time a user is attempting to sign up.)By looking
at the code at app.js,the function that handles the post request which is `'/signup'`, it just take three input
fields(username, password, password confirmation) and creates an user if not duplicated. It does not validate the
beta code at server side at the time when making such post request. It is only checked at client side instead.
This is bad since client can directly modify DOM to get themselves easily approved while server side's validation
would not allow client to accomplish this so easy.<br>
To fix it:<br>Validate the beta code at server side instead of at client side. Alternative is to enable two-way validation.<br><br>
Vulnerability 3, XSS:<br>
Issue found(and description): <br>Also called cross-site scripting. There are many input 'fields' at Bananama page, especially the one that asks<br>
user to upload comment. The admin does not know if the comment a user uploaded is untrusted data. Thus, some 
injected malware scripts will be permanently stored in server database and every time a user browses
Bananama page, they will retrieve the database to get the comment, and such injected malware scripts will 
get other users reflected. Thus, at server side, it should have a implementation of escaping all untrusted 
data, which potentially come from user 'comments'.<br>
To fix it:<br>Validate the comments before storing it in database at server side and escape all untrusted data. Limit the lengths of input fields like username and password to avoid potential script injection as well. <br><br>
Vulnerability 4, SQL Injection:<br>
Issue found(and description):<br>There is no encryption at the client side while submitting the userpasswd to the server. Also,I think the encryption generated by `.hashSync` at server side does not make the password difficult to decrypted. It is not a hard algorithm and once the attacker knows about it, they can easily get the password of a user.To interpret the SQL injection, a user may 'submit' a SQL query without detection and prohibition to get the information of other 
users.The attacker can figure out the SQL schema and make up a SQL query to get and change the information of 
another user.This is what SQL injection mainly means.<br>
To fix it: <br>Allow useful and credible encryption and decryption algorithms both at server and client side, to use parameterized queries, validate input and never trust raw input etc.