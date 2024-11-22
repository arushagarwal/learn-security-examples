# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?
Yes

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.
Here, the attacker exploits a vulnerability to crash the server by sending a script at place of id which leads to denial of service at server leading it to crash
2. Briefly explain how a malicious attacker can exploit them.
the mongoose query is expecting an id which has a particular format and this id is coming from the http request which the client provides, and the malicious attacker sends a script at its place which causes mongoose to crash, and since the developer didnt handle it, it caused the server to crash.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
used try catch or handle the errors and stop the server from crash
used rate limiter to check the rate limit appropriate, for every IP, every IP can send 1 request every 5 seconds.