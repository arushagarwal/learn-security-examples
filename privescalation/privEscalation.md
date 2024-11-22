# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
Lack of Proper Authentication: The server does not verify if the user making the request is authenticated, allowing any user to attempt to change roles.
Direct Access to User Data: The server allows direct access to user data without validating the user's identity or role, making it easy for attackers to manipulate user roles.
2. Briefly explain how a malicious attacker can exploit them.
A malicious attacker can exploit these vulnerabilities by:
Bypassing Authentication: Accessing the system without proper authentication to perform unauthorized actions.
Manipulating User Roles: Changing their own or others' roles to gain higher privileges.
Direct Object Manipulation: Accessing and modifying user data directly to escalate privileges without proper validation.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
Authentication: Ensuring that users are properly authenticated before allowing access to sensitive operations.
Authorization Checks: Verifying that the authenticated user has the necessary permissions to perform specific actions.
Input Validation and Sanitization: Validating and sanitizing user inputs to prevent injection attacks and unauthorized data manipulation.