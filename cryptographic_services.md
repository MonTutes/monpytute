# Cryptographic Services
## hashlib — Secure hashes and message digests

This module can provide common hashing functions. They can be used for verifying integrity of data. They also allow for more secure storage of passwords, making it harder for attackers who break in and obtain data to retrieve the original plaintext.

<b>Warning:</b> Some of these algorithms including md5 and sha1 are considered cryptographically insecure due to collisions.
Using these hashes directly without a [salt](https://en.wikipedia.org/wiki/Salt_(cryptography)) also carries the risk of [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) attacks. The best practices for password hashing change over time and it's best to do your own research. As of writing, I would recommend using the external [`bcrypt` package](https://pypi.org/project/bcrypt/) for passwords over these functions. 

sha1(), sha224(), sha256(), sha384(), sha512(), blake2b(), and blake2s()

md5(), sha3_224(), sha3_256(), sha3_384(), sha3_512(), shake_128(), shake_256()

## hmac — Keyed-Hashing for Message Authentication
## secrets — Generate secure random numbers for managing secrets
