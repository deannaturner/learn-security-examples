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

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

When we query from the database, we are directly using the user-provided values from the query. This means we are not checking if the user-provided query is a valid query or a malicious query before executing it.

2. Briefly explain how a malicious attacker can exploit them.

Since there is no input sanitization, a malicious attacker can inject NoSQL into the query that will get executed to steal sensitive information in the database.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?

`secure.ts` implements input sanitization of the endpoint. It removes all non-alphanumeric characters before executing the query to the database. This ensures a NoSQL attack cannot happen.