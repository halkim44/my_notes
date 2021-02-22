# bcrypt

storing password in plaintext must never be an option. However, hashing alone is not sufficient to mitigate attacks such as rainbow tables.

a better way to store passwords is to add salt to the hashing process.

## What is bcrypt?

designed by **Niels Provos** and **David Mazières** based on the Blowfish cipher.

b for Blowfish and crypt for the name of the hashing function used by the UNIX password system.
