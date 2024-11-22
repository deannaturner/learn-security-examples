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

A user can log in as the admin with no actual authentication by guessing the user id of the admin account.

2. Briefly explain how a malicious attacker can exploit them.

A malicious user can guess the admin account, and then change the user roles for other users unchecked.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?

`secure.ts` implements session middleware, that is, identifiers on the userId trying to log in. If the user doesn't have a session UserId, they are forbidden from accessing the update-role endpoint. The app then finds and authenticates that user by the session UserId, and then checks for correct privileges.