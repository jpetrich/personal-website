---
title: "Pseudorandom Generators"
published: true
---

This is my second post related to [MIT 6.875 - Foundations of Cryptography](https://mit6875.github.io/). My motivation for going through this course is in the [first post](https://joepetrich.com/2022/01/19/perfect-secrecy/).

## Pseudorandom Generators

While perfect secrecy is only achievable through a one-time pad, which is infeasible for most
communication, if we put a constraint on the adversary trying to decipher an encrypted message, we
can achieve secrecy with less effort. The constraint modern cryptography puts on the adversary is to
limit the adversary's computational power. We don't need to limit our adversary too much to accomplish
practical secrecy, but, we do need to take for granted something widely-accepted yet never proven -
that [P != NP](https://en.wikipedia.org/wiki/P_versus_NP_problem). Without getting into the weeds of
computational complexity theory, the idea is that there is a class of problems that are only solvable
in a categorically more computationally intensive manner than others, such that it would take massive
leaps in either the theory of computer science, or methods of computation, or both, to solve them.
What this idea allows us to do is to define precisely the idea of negligibility.

### Negligibility

The idea of negligibility in this context is similar to that of its plain-English meaning. The basic
idea is that if an adversary has enough computational power to make n guesses at our encrypted
message, the probability of success is 1/n. That is, the probability of successfully cracking the
encryption must be so low that it seems impossible. What this allows us to do is to broaden our
definition of secrecy somewhat to give us a practical way to accomplish secure cryptographic schemes,
given realistic computational constraints. Whereas in a perfectly secret scheme, the attacker has a 1/2 probability of guessing each bit of the original message, we can define a principle of computational
indistinguishability that will allow for practical secrecy.

### Computational Indistinguishability and Pseudorandom Generators

An encryption scheme has computational indistinguishability if the probability of an attacker computing each bit of the original message from an encrypted message is negligibly more than 1/2. How can we take advantage of this idea to make cryptography practical? Remember that a one-time pad, the perfectly secret method of encryption, relies on a truly random sequence of bits at least as long as the message to encrypt. What if we designed a function to generate a string of N bits from a random seed of a few bits, such that the resulting string of bits is computationally indistinguishable from a truly random string? We could then use this generated string to encrypt a message, shorter than N bits, and the attacker, limited not by theory, but practical computational limits, would be unable to decrypt the message.

Modern cryptography uses this approach. Pseudorandom generators, that can't be reverse engineered in polynomial time, are used to generate keys. If P != NP, then pseudorandom numbers are negligibly less secure than truly random numbers, and the resulting encryption functions will have computational indistinguishability, and therefore practical secrecy. Unfortunately, since P != NP hasn't been proven, it's not possible to prove that any such cryptographic scheme is theoretically secure. Since no one has proved P=NP though, cryptographers assume that modern cryptography is valid (or at least good enough for the internet!) and focus their efforts on defining functions that can act as pseudorandom generators. This topic of pseudorandom generators will lay the groundwork for the rest of the foundations of cryptography course.
