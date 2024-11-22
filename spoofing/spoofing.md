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

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.

The cookie in the session is not `httpOnly`, which means client-side JS can see the stored cookie. It also does not have the `sameSite` attribute, which means a cross-site forgery attack can steal it and use it.

2. Briefly explain different ways in which vulnerability can be exploited.

An attacker can steal the cookie (like in `mal-steal-cookie.html`) by printing out or storing the result of `document.cookie`, since the client-side JS can access that. An attacker can also perform a cross-site request forgery (CSRF) attack, like in `mal-csrf.html`, by stealing the cookie to authenticate as a user, and then injecting a script to perform unwanted actions whilst authenticated.

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.

In `secure.ts`, the session is updated to have the `httpOnly` attribute set to true, which means client-side JS cannot access the value in `document.cookie`. Also, the session has the `sameSite` attribute, which helps introduce security against CSRF attacks.