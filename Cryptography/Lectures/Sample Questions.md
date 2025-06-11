#PRACTICE  

---
## Quiz: Short Answer Questions
#QUIZ

Answer each question in 2-3 sentences.

1. **Modular Inverse:** Explain what a multiplicative inverse modulo n is and under what condition it exists for an integer x.
2. **XOR Properties:** Describe two properties of the XOR operation that make it particularly useful in cryptography.
3. **Big-O Notation for Infeasibility:** How is Big-O notation used to define "computationally infeasible" attacks in cryptography?
4. **One-Time Pad Key Length:** What is a critical requirement for the key in a One-Time Pad, and why is this requirement difficult to meet in practice?
5. **Hybrid Proof Technique:** Briefly explain the purpose of the hybrid technique in proving cryptographic security.
6. **Shamir Secret Sharing Uniqueness:** In Shamir Secret Sharing, why does a degree-d polynomial require d+1 points to be uniquely determined?
7. **Symmetric Ratchet Forward Secrecy:** How does a symmetric ratchet provide forward secrecy against an attacker who compromises a device after a certain number of ciphertexts have been sent?
8. **PRP Invertibility:** What is a defining characteristic of a Pseudorandom Permutation (PRP) that distinguishes it from a general Pseudorandom Function (PRF)?
9. **Padding Oracle Attack Vulnerability:** What specific information does a padding oracle attack reveal to an adversary, and why is this information dangerous?
10. **RSA Modulus Factoring Hardness:** What mathematical problem is the security of RSA based on, and why is this problem considered hard?

## Answer Key

1. **Modular Inverse:** A multiplicative inverse x⁻¹ of an integer x modulo n is an integer such that x * x⁻¹ ≡ n 1. It exists if and only if the greatest common divisor (GCD) of x and n is 1, meaning x and n are relatively prime.
2. **XOR Properties:** XORing a string with itself results in all zeros (x ⊕ x = 0), enabling easy decryption by re-XORing with the key. Also, XORing with zeros has no effect (x ⊕ 0 = x), which is useful in certain constructions.
3. **Big-O Notation for Infeasibility:** In Big-O notation, a "computationally infeasible" attack is one whose running time grows faster than any polynomial function of the security parameter (e.g., exponential time). This implies that for sufficiently large parameters, the attack becomes impractical even with vast computational resources.
4. **One-Time Pad Key Length:** A critical requirement for the One-Time Pad key is that it must be at least as long as the plaintext message and used only once. This makes it difficult to meet in practice due to the challenges of secure key distribution and management for large amounts of data.
5. **Hybrid Proof Technique:** The hybrid technique is used to prove the indistinguishability between two complex cryptographic systems by constructing a sequence of intermediate "hybrid" systems. Each adjacent pair in the sequence differs by only a small, provably indistinguishable change, allowing the overall indistinguishability to be established.
6. **Shamir Secret Sharing Uniqueness:** A degree-d polynomial is uniquely determined by d+1 distinct points because if two distinct degree-d polynomials passed through the same d+1 points, their difference would be a degree-d polynomial with d+1 roots, which is only possible if the polynomial is identically zero.
7. **Symmetric Ratchet Forward Secrecy:** A symmetric ratchet ensures that if an attacker compromises a device at time 'n' and learns the current key sn, they cannot compute previous keys s0 through sn-1 because the previous keys are erased from memory. This prevents decryption of past messages even if the current key is compromised.
8. **PRP Invertibility:** A Pseudorandom Permutation (PRP) is a deterministic function that is efficiently invertible given the key. This invertibility property is crucial for block ciphers, allowing for both encryption and decryption with the same key, unlike a general PRF which doesn't necessarily need to be invertible.
9. **Padding Oracle Attack Vulnerability:** A padding oracle attack reveals whether a given ciphertext, when decrypted, results in valid padding. This seemingly small piece of information allows an attacker to iteratively deduce plaintext bytes by manipulating the ciphertext and observing the oracle's response.
10. **RSA Modulus Factoring Hardness:** The security of RSA is based on the computational hardness of factoring large composite numbers (N) into their two large prime factors (p and q). If an attacker could efficiently factor N, they could compute the private key (d) and decrypt any message or forge any signature.

## Essay Format Questions

1. Compare and contrast the security goals and underlying mathematical assumptions of symmetric-key encryption (e.g., CPA-secure AES in CTR mode) and public-key encryption (e.g., ElGamal). Discuss how the "key distribution problem" is addressed in each paradigm.
2. Explain the concept of indistinguishability in provable security. Choose one specific security definition (e.g., CPA security for symmetric encryption, or PRG security) and describe how it uses the indistinguishability paradigm, including the roles of the "real" and "random/fake" libraries and the "distinguisher."
3. Discuss the importance of padding schemes in block cipher modes of operation. Describe at least two different padding schemes (e.g., PKCS#7, ISO/IEC 7816-4, zero-padding) and explain how a padding oracle attack can exploit vulnerabilities related to improper padding validation.
4. Analyze the role of modular arithmetic in the construction and security of RSA. Explain how Euler's totient function and the concept of multiplicative inverses modulo $\phi(N)$ are crucial for the encryption and decryption processes.
5. Describe the Merkle-Damgård construction for hash functions. Explain how it enables the creation of a collision-resistant hash function from a collision-resistant compression function. Discuss a specific attack (e.g., length-extension attack) that can arise from this construction if the hash function is used in a context where its internal state is exposed.