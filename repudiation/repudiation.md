# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.

In repudiation, there is no way to tell who is associated with what actions/transactions in a system. 

2. Briefly explain why the vulnerability is addressed in __secure.ts__.

In `secure.ts`, we implement logging to track the users making requests. This way, we know who is performing what action/transaction in our system.

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?

It's lifting the state in a sort of way. We tell the app to use the logging we provide it, which then can be utilized by the other endpoints of the app.