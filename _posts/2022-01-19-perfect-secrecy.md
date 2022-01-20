---
title: "Perfect Secrecy"
published: true
---

I've been interested in cryptocurrencies for several years, and [recently got into the technical
side of them](https://joepetrich.com/2021/07/24/hack-money-hackathon/), learning to build on top
of Ethereum. As I learned more, my interest in the foundation of cryptocurrencies increased,
and so I read a couple of introductions to cryptography - [Crypto](https://en.wikipedia.org/wiki/Crypto_(book))
and [The Code Book](https://en.wikipedia.org/wiki/The_Code_Book). Learning about the cryptography
throughout the centuries, culminating in information theory and the battle around public key
cryptography and a secure internet in the late 20th century, made me want to learn more about the
fundamental math and computer science behind the cryptography that enables a secure internet,
decentralized blockchains, and self sovereignty. To that end, I decided to work through
[MIT 6.875 - Foundations of Cryptography](https://mit6875.github.io/) which has lectures, papers,
and homework all available on GitHub. [I created a schedule for myself to work through it in a
year](https://skitter-naranja-b42.notion.site/01aed573d0384dc090ce5d07004aaf82?v=9dc0c1ffe29c4d04af98c3e01e4f56b0),
[invited anyone to join me](https://twitter.com/jpetrichsr/status/1480689628860624899?s=20), and
started [a small Discord](https://discord.gg/h8C7UP8HzP) for discussing the lectures. The course
is technical, requiring a background in mathematical proofs and computer science, but the
concepts are broadly interesting and relevant to anyone interested in the foundations of secure
communication. I'll be writing a few pieces here about the course material to help myself - what
better way to learn than to teach? - and hopefully interest more people in 'the crypto behind
crypto.'

## Perfect Secrecy

At the foundation of cryptography is the idea of secrecy - how can Alice send a message to Bob
without Eve the eavesdropper understanding the message? When designing a cryptographic system, we
must assume that Eve can intercept the encrypted message - the ciphertext - and process it however
she pleases. In [Communication Theory of Secrecy Systems](https://en.wikipedia.org/wiki/Communication_Theory_of_Secrecy_Systems), Claude Shannon outlined an information-theory approach to cryptography using this idea. He outlined three algorithms in the system:

1. Key Generation creates a key to be used in encryption and decryption.
2. Encryption takes a plaintext message and a key, and generates a ciphertext by combining them somehow.
3. Decryption takes a ciphertext and a key, and returns the plaintext.

Alice and Bob meet at some point, and use the key generation algorithm to generate a shared key.
Eve has access to all three of these algorithms, as well as the ciphertext, but wasn't there when
Alice and Bob generated the key. Because she knows the key generation algorithm, it's important
that it be *random*. If it is deterministic, Eve will be able to generate the key that Alice and
Bob are using, and get the plaintext just like Bob can. The perfect cryptographic system would
guarantee what Shannon called "Perfect Secrecy," where, no matter how much computing power Eve
has, or how sophisticated an algorithm, her chance at guessing the plaintext from the ciphertext
*is the same as if she didn't even have the ciphertext.* Put differently, having the ciphertext
gives Eve no information about the plaintext.

### Is Perfect Secrecy Achievable?

Is perfect secrecy achievable? Yes, with a one-time pad. A one-time pad is a key, longer than the message, that is only used once. The one-time pad is used as follows:

1. Generate the one-time pad by generating as many bits as necessary randomly.
2. Take your message (in binary) and [exclusive-or](https://en.wikipedia.org/wiki/Exclusive_or)
it with the one-time pad. This means you take each bit one by one and compare it. 1 XOR 1 = 0,
XOR 0 = 1, 0 XOR 0 = 0, 0 XOR 1 = 1.
3. On the decryption side, XOR the key with the ciphertext. As you can see, XOR reverses the
encryption perfectly.

The randomness of the one-time pad is paramount, because any pattern used in its generation could
be replicated by Eve to generate the same key. If it is completely random, the ciphertext will be
completely random, and Eve will have no way to get information from it. However, if the one-time
pad is reused, the system is no longer secure! Two ciphertexts generated from the same key can be
XOR'd together, and the result is the XOR of the two plaintexts. This is because (Ciphertext A)
XOR (Ciphertext B) = (Plaintext A XOR Key) XOR (Plaintext B XOR Key), and the Key XOR Key cancels
each other out. Since the plaintexts are not generated randomly, the XOR of the two provides Eve
some information, violating perfect secrecy.

### What is the Cost of Perfect Secrecy?

Perfect secrecy requires the use of a one-time pad, which, as you can imagine, is infeasible.
Alice and Bob will need to generate as many one-time pads as they will ever need to exchange
messages, and each key will need to be as large as or larger than the message it is used to
encrypt. Does every web browser come with a one-time pad large enough to secure all your
communication with all websites for as long as you might use the internet? Of course not! While
perfect secrecy is only achievable only with great effort, we can define bounds on Eve's
computational resources. With these bounds defined, we only need to prove that our cryptographic
system is unsolvable within those bounds. It is this concept upon which modern cryptography is
built.
