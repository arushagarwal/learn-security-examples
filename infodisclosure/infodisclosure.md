# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?username[$ne]=
    ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?
Yes

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
We are searching database based on the username we are getting from the http request and if that username comes to be a script or nosql query script and ends up executing the mongoose query in the way server did not expect it to execute, and this is called nosql injection attack.
2. Briefly explain how a malicious attacker can exploit them.
When the user sends a specially crafted query at the place of username which says to give all usernames and the server returns the first document from the database, and the attacker gets the sensitive data from the database without actually having username to get the data. Its a potential security vulnerability. Again we are not sanitizing the input we are getting from the request.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?
When we get the http request from the client, we are sanitizing the input and firstly checking that its a string or not, to make sure, we are not sending any script to the database query. Then, we are removing non-alphanumeric characters to prevent NoSQL injection to block all semicolons, brackets etc.