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

There is no input sanitization for the name box, which means things other than names can be fed into the app, like scripts. The app has no way of knowing where a script came from, so it will execute the script it is fed, which is potentially very dangerous.

2. Briefly explain how a malicious attacker can exploit them.

A malicious attacker can send a script through something that doesn't sanitize inputs. This is called cross-site scripting (XSS). They can be used to steal session data, cookies or other sensitive information.

3. Briefly explain why **secure.ts** does not have the same vulnerabilties?

`secure.ts` calls `escapeHTML` in its /register endpoint, which sanitizes the inputs to prevent XSS attacks.