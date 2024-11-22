# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
Not checking the input, so the user can inject a script in the input which can be link to malicious application. So the input form we are accepting inputs which are supposed to be plain string but we are also allowing code injections, which goes into the server and gets redirected as a hyperlink.
2. Briefly explain how a malicious attacker can exploit them.
User can add code at the place of string in the form which will run in server at place of string. This is a violation of integrity as server should not run any code which is not written by it. It should not accept any code as input which it has accepted. We are taking input from the user which happens to come from the request, request can come from any client and without checking the input, we are running the string that the server received

3. Briefly explain why **secure.ts** does not have the same vulnerabilties?
We are sanitizing the input that we are receicing using the function escapeHTML where we convert it to format we expect it to be.Replacing every code looking keyword into a string thereby nullifying the impact of code injection.