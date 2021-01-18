# Web Authentication

## HTTP sessions

login once and the browser will remember you had login. thats how session works.

the way this works behind the scenes is with cookies.

### Cookies

cookies are a small data that are stored on a client side and sent to the client along with server request.

nothing more than a string passed in a request.

use client-sessions library to work with sessions in node.

cookies is used for :

- maintaining session
- adding user specific feature in web app

### Cookie-parser

provides middleware for parsing of cookies.

#### Creating Cookies

using `set-cookies`.

## Pasword Hashing

two concepts i need to know about password hashing:

- if hashing two of the same password, the same long random string will be the same
- once we have the long hash, we can never turn it back into the original password(one-way function)

whats the best tools to use:

- bcrypt(recommended)
- scrypt

## CSRF

Cross Site Request Forgery is when someone sends you an email with a link on it to trick you to automatically fill form in a withdraw page of a bank when you click the link.

## HTTP Request

every single Http Request have two components which is Headers and Body.

when requesting a webpage, the html code is in the Body and the header code is in the Header.
