# Secure Shell Protocol (SSH)

another protocol(like http, ftp..) that allows two computers to communicate over the internet.

it allows users to:

- share files
- control/modify remote computers over the internet

need a certain protocol to enable connection between two devices.

it use encryption to secure connection between HOST and CLIENT.

```bash
ssh {user}@{host}
```

## Encryption technique

1. Symmetrical Encryption
2. Asymmetrical Encryption
3. Hashing

asymmetric Encryption is used to share a secret key and then using the secret key for further communication. Hashing is used to verify the authentication of the messages. finally is to authenticate the user.

### Symmetric Encrpytion

- uses one **secret key** for both encryption and decryption.
- uses "Key Exchange Algorithm" for secure key exchange between computer

### Asymmetrical Encryption

- uses two separate(Public and Private key) key for encryption and decryption
- public key is shared with anybody and are used to incrypt
- private key is never shared with anybody and re used to decrypt
- uses the Diffie Hellman Key Exchange which a device will generate a symmetric key using its private and public key and the public key of the device it connected to
- when two devices who had shared public key communicate, the sender will encrypt its message using its public key, the message will only be decrypted using the private key of a device that the sender have share public key with.

### Hashing

- generate a unique value of a fixed length for each input that it gets.
- each message that is transmited must contain MAC
- MAC is a hash generated from the symmetric key, the packet sequence number, and the message content
- The Host will run through the same hash function on the message receive and see if it match with the client

### RSA

prove the identity without a password through the ssh connection.

use `ssh-keygen -C {email}`

1. generate an ssh id in a device
2. add the generated ssh id usning `ssh-add`
3. copy the public key generated from the new ssh id
4. paste the key to authorized_keys file inside the .ssh folder of another device we want to connect
5. enjoy accessing without the need of a password.
