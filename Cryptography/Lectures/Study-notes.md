---
layout : default
title : Cryptography Fundamentals: A Study Guide
---
#OVERVIEW 
#INTRODUCTION 
# Cryptography Fundamentals: A Study Guide
---

This study guide is designed to help you review and deepen your understanding of core cryptography concepts. It covers foundational mathematical principles, essential cryptographic primitives, and various security definitions and attack models.
## I. Core Concepts & Notation ([Lektion-0](Lektion-0.md))

- **[Logs and Exponents](Lektion-0.md#0.1-Logs-and-Exponents):** Understanding exponential relationships and their inverse, logarithms.
- **[Modular Arithmetic](Lektion-0.md#0.2-Modular-Arithmetic):** ($\mathbb{Z}_n$, congruence, GCD, inverse):** Operations on integers modulo n, including definitions of $\mathbb{Z}_n$, congruence ($a \equiv_{n} b$), and the concept of a multiplicative inverse. Euclid's algorithm for Greatest Common Divisor (GCD) and its extension for finding modular inverses.
- **[Strings (XOR)](Lektion-0.md#0.3-Strings):** Bitwise exclusive-or (XOR) operation on strings of equal length, its properties (self-inverse, identity, associativity, symmetry), and its interpretation as bit-flipping.
- **[Functions](Lektion-0.md#0.4-Functions):** Basic definitions and properties of functions relevant to cryptographic contexts.
- **[Probability](Lektion-0.md#0.5-Probability):** Fundamental probability concepts used in security definitions and analysis (e.g., Birthday Probabilities).
- **[Notation in Pseudocode](Lektion-0.md#0.6-Notations-in-Pseudocode):** Understanding common pseudocode conventions for algorithms.
- **[Asymptotics (Big-O, Omega, Theta)](Lektion-0.md#0.7-Asymptotic-Notations):** Characterizing the efficiency and growth rate of algorithms using Big-O, Omega, and Theta notation. Understanding "computationally infeasible" attacks in terms of asymptotic complexity.

## II. Cryptographic Primitives & Security Definitions

### A. One-Time Pad & Kerckhoffs' Principle ([Lektion-1](Lektion-1.md))

- **[One-Time Pad (OTP)](Lektion-1.md#One-TimePad):** Understanding the specifics of OTP encryption and its perfect secrecy.
- **Kerckhoffs' Principle:** The principle that a cryptosystem should be secure even if everything about the system, except the key, is public knowledge.

### B. Provable Security (Chapter 2)

- **Security Definitions:** Formalizing security definitions using indistinguishability between "real" and "random" or "fake" libraries.
- **Formalisms for Security Definitions (Hybrid Technique):** The hybrid argument as a proof technique to demonstrate indistinguishability between cryptographic schemes.
- **Demonstrating Insecurity with Attacks:** How to identify and describe distinguishing attacks that break a scheme's security.
- **Comparing/Contrasting Security Definitions:** Understanding the relationships and differences between various security models.

### C. Secret Sharing (Chapter 3)

- **Definitions:** Threshold Secret-Sharing Schemes (TSSS) and their security definitions.
- **Simple 2-out-of-2 Scheme:** A basic example of a secret sharing scheme.
- **Polynomial Interpolation:** Lagrange interpolation for uniquely determining a polynomial given a sufficient number of points. Its application in Shamir Secret Sharing.
- **Shamir Secret Sharing:** A (t, n)-threshold secret sharing scheme based on polynomial interpolation. Understanding its security proof.
- **Visual Secret Sharing:** A specialized secret sharing method.

### D. Foundations of Computational Security (Chapter 4)

- **Computationally Infeasible Attacks:** Defining what constitutes an "infeasible" attack in a computational setting, linking to asymptotic notation.
- **Negligible Success Probability:** Defining "negligible" probabilities for an adversary's success.
- **Indistinguishability:** A core concept in provable security, particularly for distinguishing between a "real" cryptographic object and a "random" or "fake" one.
- **Birthday Probabilities:** Understanding the Birthday Paradox and its implications for attack probabilities.

### E. Pseudorandom Generators (PRGs) (Chapter 5)

- **Definitions:** Formal definition of a PRG and its security.
- **PRGs in Practice:** Practical applications of PRGs.
- **Application: Shorter Keys in One-Time-Secret Encryption:** How PRGs allow for shorter keys in encryption schemes.
- **Extending the Stretch of a PRG:** Techniques for increasing the output length of a PRG.
- **Applications: Stream Cipher & Symmetric Ratchet:** Understanding these applications and their security implications.

### F. Pseudorandom Functions (PRFs) & Block Ciphers (Chapter 6)

- **Definition of PRF:** Formal definition of a PRF.
- **PRFs vs. PRGs; Variable-Hybrid Proofs:** Distinctions between PRFs and PRGs, and the use of variable-hybrid proofs.
- **Block Ciphers (Pseudorandom Permutations - PRPs):** Definition of a PRP and its properties, including invertibility.
- **Relating PRFs and Block Ciphers:** The relationship between PRFs and PRPs.
- **PRFs and Block Ciphers in Practice:** Real-world usage.
- **Strong Pseudorandom Permutations:** A stronger security notion for PRPs.

### G. Security Against Chosen Plaintext Attacks (CPA) (Chapter 7)

- **Limits of Deterministic Encryption:** Why deterministic encryption often fails against CPA.
- **Pseudorandom Ciphertexts:** The concept that ciphertexts should appear random under a CPA-secure scheme.
- **CPA-Secure Encryption Based On PRFs:** Constructions of CPA-secure encryption schemes using PRFs.

### H. Block Cipher Modes of Operation (Chapter 8)

- **Common Modes:** Understanding modes like CBC (Cipher Block Chaining) and CTR (Counter Mode).
- **CPA Security and Variable-Length Plaintexts:** How modes extend block ciphers to handle variable-length messages while maintaining CPA security.
- **Security of OFB Mode:** Analysis of Output Feedback (OFB) mode security.
- **Padding & Ciphertext Stealing:** Techniques for handling plaintext messages that are not a multiple of the block length (PKCS#7, ISO/IEC 7816-4, zero-padding, CBC-CTS).

### I. Chosen Ciphertext Attacks (CCA) (Chapter 9)

- **Padding Oracle Attacks:** A prominent example of a CCA against improperly implemented padding.
- **Defining CCA Security:** Formal definitions of CCA and CCA$.
- **Simple CCA-Secure Scheme:** Examples of schemes designed to resist CCA.

### J. Message Authentication Codes (MACs) (Chapter 10)

- **Definition of MAC:** Formal definition of a MAC and its security properties.
- **A PRF is a MAC:** The relationship between PRFs and MACs.
- **MACs for Long Messages:** Techniques for authenticating messages longer than a single block.
- **Encrypt-Then-MAC:** A common and generally recommended approach for achieving authenticated encryption.

### K. Hash Functions (Chapter 11)

- **Security Properties for Hash Functions:** Collision resistance, second pre-image resistance, and pre-image resistance.
- **Merkle-Damgård Construction:** A common method for building hash functions from compression functions.
- **Hash Functions vs. MACs: Length-Extension Attacks:** Understanding the differences and attacks specific to hash functions, like length-extension attacks.

### L. Authenticated Encryption & AEAD (Chapter 12)

- **Definitions:** Formal definitions of Authenticated Encryption (AE) and Authenticated Encryption with Associated Data (AEAD).
- **Achieving AE/AEAD:** Strategies for constructing AE/AEAD schemes.
- **Carter-Wegman MACs:** A type of MAC often used in AEAD constructions, relying on Universal Hash Functions (UHFs).
- **Galois Counter Mode (GCM) for AEAD:** A widely used AEAD mode.

### M. RSA & Digital Signatures (Chapter 13)

- **"Dividing" Mod n (Multiplicative Inverse):** Understanding modular inverse and its relationship to GCD (Bezout's theorem, Extended Euclidean Algorithm).
- **The RSA Function:** Definition of the RSA encryption and decryption functions, relying on modular exponentiation and Euler's totient function.
- **Digital Signatures:** Introduction to digital signatures, often based on RSA principles.
- **Chinese Remainder Theorem (CRT):** Solving systems of linear congruences and its applications in cryptography, particularly RSA.
- **The Hardness of Factoring N:** The computational problem underlying RSA security.
- **Square Roots of Unity Modulo N:** Properties of square roots modulo composite numbers.
- **Exponentiation by Repeated Squaring:** An efficient algorithm for modular exponentiation.

### N. Diffie-Hellman Key Agreement (Chapter 14)

- **Cyclic Groups:** Properties of cyclic groups, including generators and closure under multiplication and inverses.
- **Diffie-Hellman Key Agreement:** The protocol for two parties to establish a shared secret over an insecure channel.
- **Decisional Diffie-Hellman Problem (DDH):** The computational assumption underlying Diffie-Hellman security, distinguishing between a "real" Diffie-Hellman tuple and a "random" one.

### O. Public-Key Encryption (Chapter 15)

- **Security Definitions:** Security definitions for public-key encryption (e.g., one-time security).
- **One-Time Security Implies Many-Time Security:** How a strong one-time security definition can extend to multiple encryptions for public-key systems.
- **ElGamal Encryption:** A public-key encryption scheme based on the Diffie-Hellman assumption.
- **Hybrid Encryption:** Combining public-key and symmetric-key encryption for efficiency and security.

---


## Glossary of Key Terms

- **Authenticated Encryption (AE):** An encryption scheme that provides both confidentiality and integrity for the plaintext, ensuring that the message cannot be deciphered or tampered with without detection.
- **Authenticated Encryption with Associated Data (AEAD):** An AE scheme that also authenticates "associated data" (e.g., headers) that is not encrypted but needs integrity protection.
- **Asymptotics (Big-O, Omega, Theta):** Mathematical notation used to describe the limiting behavior of functions, particularly for characterizing the efficiency and scalability of algorithms in terms of their input size.
- **Birthday Probabilities:** The probabilities related to the "Birthday Paradox," which states that in a random set of n people, there's a surprisingly high probability that two people share the same birthday. In cryptography, it applies to collision probabilities in hash functions.
- **Bitwise Exclusive-OR (XOR, ⊕):** A binary operation that outputs true (1) if the inputs are different, and false (0) if they are the same. Used extensively in symmetric-key cryptography for its self-inverse property.
- **Block Cipher:** A deterministic algorithm that operates on fixed-size blocks of plaintext using a secret key to produce a fixed-size block of ciphertext. Typically models as a Pseudorandom Permutation (PRP).
- **Block Cipher Mode of Operation:** A method for using a block cipher to securely encrypt messages longer than the block size. Examples include CBC, CTR, and OFB.
- **Carter-Wegman MACs:** A type of Message Authentication Code (MAC) construction that uses Universal Hash Functions (UHFs) to achieve very efficient authentication, often with information-theoretic security guarantees.
- **Chosen Ciphertext Attack (CCA):** An attack model where the adversary can choose ciphertexts to decrypt and observe the corresponding plaintexts (except for the challenge ciphertext), and attempts to gain information about the key or plaintext.
- **Chosen Plaintext Attack (CPA):** An attack model where the adversary can choose plaintexts to encrypt and observe the corresponding ciphertexts, and attempts to gain information about the key or future plaintexts.
- **Chinese Remainder Theorem (CRT):** A theorem that provides a unique solution to a system of linear congruences with pairwise coprime moduli. Used in RSA for efficiency optimizations.
- **Cipher Block Chaining (CBC):** A block cipher mode of operation where each block of plaintext is XORed with the previous ciphertext block before being encrypted. It uses an Initialization Vector (IV).
- **Ciphertext Stealing (CTS):** A technique used with block cipher modes (like CBC) to handle plaintexts whose length is not a multiple of the block size without padding, by "stealing" ciphertext from the previous block.
- **Collision Resistance:** A property of a cryptographic hash function meaning it is computationally infeasible to find two distinct inputs that produce the same hash output.
- **Computationally Infeasible:** A task or attack is computationally infeasible if the time or resources required to perform it grow super-polynomially (e.g., exponentially) with respect to the security parameter, making it impractical for sufficiently large parameters.
- **Congruent Modulo n (a ≡_n b):** Two integers a and b are congruent modulo n if their difference (a - b) is an integer multiple of n, or equivalently, if they have the same remainder when divided by n.
- **Counter Mode (CTR):** A block cipher mode of operation that turns a block cipher into a stream cipher. It encrypts a sequence of incrementing "counters" with the key and XORs the results with the plaintext.
- **Cyclic Group:** A group that is generated by a single element, meaning every element in the group can be expressed as a power of that generator.
- **Decisional Diffie-Hellman (DDH) Problem:** The computational assumption that it is hard to distinguish between a "real" Diffie-Hellman tuple (g^a, g^b, g^ab) and a "random" tuple (g^a, g^b, g^c) in a cyclic group.
- **Digital Signature:** A cryptographic mechanism used to verify the authenticity and integrity of a digital message or document, ensuring its origin and that it has not been altered.
- **Diffie-Hellman (DH) Key Agreement:** A cryptographic protocol that allows two parties who have no prior knowledge of each other to jointly establish a shared secret key over an insecure communications channel.
- **Distinguisher:** In provable security, an algorithm (often probabilistic polynomial-time) that attempts to determine whether it is interacting with a "real" cryptographic construction or a "random" or "fake" one.
- **Encrypt-Then-MAC:** A common and recommended approach to achieving authenticated encryption, where the message is first encrypted, and then the resulting ciphertext is authenticated with a MAC.
- **Extended Euclidean Algorithm:** An extension of Euclid's algorithm that, in addition to finding the greatest common divisor (GCD) of two integers, also finds integers x and y such that ax + by = gcd(a, b). This is crucial for finding modular inverses.
- **Galois Counter Mode (GCM):** A widely used authenticated encryption mode that combines CTR mode for confidentiality with a Universal Hash Function (GHASH) for authentication.
- **Greatest Common Divisor (GCD):** The largest positive integer that divides two or more integers without leaving a remainder.
- **Hash Function:** A mathematical algorithm that maps data of arbitrary size to a bit string of a fixed size, designed to be one-way and collision-resistant.
- **Hybrid Technique:** A proof technique in cryptography where the security of a complex scheme is proven by showing that it is indistinguishable from a series of simpler, incrementally modified "hybrid" schemes, where each step is provably secure.
- **Indistinguishability:** A core concept in provable security, stating that two cryptographic objects or systems are computationally indistinguishable if no probabilistic polynomial-time adversary can tell them apart with a non-negligible advantage.
- **Kerckhoffs' Principle:** A fundamental principle in cryptography stating that a cryptosystem should be secure even if everything about the system, except for the secret key, is public knowledge.
- **Lagrange Interpolation:** A method for finding a polynomial that passes through a given set of data points. Crucial for the construction of Shamir Secret Sharing.
- **Length-Extension Attack:** An attack against hash functions constructed using the Merkle-Damgård paradigm (like MD5, SHA-1, SHA-256) where an attacker can append data to a message and compute the hash of the modified message without knowing the original message or the secret key, given only the hash of the original message.
- **Message Authentication Code (MAC):** A short piece of information used to authenticate a message and ensure its integrity. It is generated using a secret key and verifies that the message has not been altered and originates from an authorized sender.
- **Merkle-Damgård Construction:** A widely used method for building collision-resistant hash functions from collision-resistant compression functions.
- **Modular Arithmetic:** A system of arithmetic for integers, where numbers "wrap around" upon reaching a certain value (the modulus).
- **Multiplicative Inverse Modulo n:** See "Modular Inverse."
- **Negligible Function:** A function f(λ) (where λ is the security parameter) that decreases faster than the inverse of any polynomial. In cryptography, an adversary's success probability is considered negligible if it is bounded by a negligible function.
- **One-Time Pad (OTP):** An encryption scheme that is provably perfectly secure, but requires a pre-shared secret key that is at least as long as the plaintext and used only once.
- **Padding:** The process of adding extra data (often zeros or specific patterns) to a message to ensure it meets a required block size or format for cryptographic operations.
- **Padding Oracle Attack:** A type of chosen ciphertext attack against block ciphers used in CBC mode where the attacker can determine if a decrypted ciphertext has valid padding, allowing them to decrypt the message byte by byte.
- **Polynomial Interpolation:** See "Lagrange Interpolation."
- **Pre-image Resistance:** A property of a cryptographic hash function meaning it is computationally infeasible to find an input that hashes to a specific output.
- **Probabilistic Polynomial-Time (PPT):** An algorithm or adversary that runs in polynomial time with respect to the security parameter, and may make random choices. This is the standard computational model for adversaries in modern cryptography.
- **Pseudorandom Function (PRF):** A function that takes a secret key and an input, and produces an output that is computationally indistinguishable from the output of a truly random function.
- **Pseudorandom Generator (PRG):** A deterministic algorithm that takes a short, truly random seed as input and produces a long, computationally indistinguishable-from-random output string.
- **Pseudorandom Permutation (PRP):** A block cipher that is computationally indistinguishable from a truly random permutation. A PRP is a special type of PRF that is also invertible.
- **Public-Key Encryption:** An encryption system that uses a pair of keys: a public key for encryption and a private key for decryption.
- **Relatively Prime:** Two integers are relatively prime (or coprime) if their greatest common divisor (GCD) is 1.
- **RSA Function:** A public-key cryptographic algorithm used for secure data transmission and digital signatures. Its security relies on the difficulty of factoring large numbers.
- **Second Pre-image Resistance:** A property of a cryptographic hash function meaning it is computationally infeasible to find a second input that produces the same hash output as a given first input.
- **Secret Sharing:** A method for distributing a secret among a group of participants, each of whom is allocated a share of the secret. The secret can only be reconstructed when a sufficient number of shares are combined.
- **Shamir Secret Sharing:** A specific (t, n)-threshold secret sharing scheme where a secret can be reconstructed only if at least 't' out of 'n' shares are collected, based on polynomial interpolation.
- **Strong Pseudorandom Permutation (SPRP):** A stronger security notion for a PRP where the adversary cannot distinguish it from a random permutation even if they can query both the permutation and its inverse.
- **Symmetric Ratchet:** A cryptographic construction that allows parties to derive a sequence of fresh, independent keys from a shared secret, with the property that compromising a later key does not reveal earlier keys (forward secrecy).
- **Threshold Secret-Sharing Scheme (TSSS):** A secret sharing scheme where the secret can only be recovered if a minimum "threshold" number of shares are presented.
- **Z_n:** The set of integers modulo n, which includes the integers {0, 1, ..., n-1}.
