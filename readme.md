This is just an example app that has a frontend SPA in Vue and a backend API in Laravel using Laravel Passport.

The idea is to demonstrate the PKCE extension working. Some relevant bits:

- The code the redirects the user when they click the "Login" button in the SPA is [here](./client/src/views/Login.vue);
- The code that performs the exchange when API redirects back to SPA after user authorizes the client is [here](./client/src/views/Callback.vue).

In the API side, when you are creating the client, you need to unmark the "Confidential" checkbox.
