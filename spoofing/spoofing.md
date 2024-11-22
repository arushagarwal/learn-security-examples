# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?
Yes

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 
When the user is not logged out, we see : { message: 'Operation successful' }
When the user is logged out, we see : { message: 'Unauthorized Access' }


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.
Ans : Cookies are being sent to the server with every request so that server remembers its the same user because it has the same token, but the cookie can be read programmatically by any malicious attacker
2. Briefly explain different ways in which vulnerability can be exploited.
And : Suppose, there is a fishing link, which is opened in the same browser, in which the cookie is set, and that link has a script attached to it which can read the all cookies saved in the browser. Now, since the attacker has the cookie, they just need the link or url of the server and can send the request with the cookie as token and the server will take it as a authenticated user, there by causing spoofing.
3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
Ans : Here, the cookie is protected because of which attacker cant access cookie. So the way we are configuring cookie in secure.ts is that httpOnly is true, which means that no one can read the cookie progrmmatically, and sameSite is true, which means that when a request gets sent, this cookie will only be sent if domain of the client and server are a match, and wont be sent if some other client or site is trying to access the server. We prevent cookie stealing and CSRF with these ways.