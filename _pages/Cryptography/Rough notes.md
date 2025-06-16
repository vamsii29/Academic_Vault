
---

1. Hiding the existence of a communication channel is called **steganography**. 
2. **Kerckhoff's principle** : The method must not be required to be secret, and it must be able to fall into the enemy's hands without causing inconvenience. **(Design the systems to be secure even if the attacker has complete knowledge of all its algorithm)**.
3. **One time padding** : Also called as **Vernam's cipher** after Gilbert Vernam,(a telegraph engineer who patented the scheme in 1919.)
4. $\lambda$ to refer to the length (# of Bits) of the secret key in a scheme, so that keys are elements of the set $\{0, 1\}^\lambda$.
5. choice of $\lambda$ doesn't effect the security; however the length of the keys and plaintext must be compatible. 


Here is a detailed, one-by-one explanation of the requested cryptography topics, designed to help you prepare for a viva exam.

### 1. Introduction

Cryptography, at its core, is concerned with **controlling access to information** [1]. It breaks down the broad concept of "security" into more specific goals such as **confidentiality, authenticity, and integrity** [1].

This book, "The Joy of Cryptography," approaches the subject from the perspective of **provable security**, meaning that claims about security can be formally defined and mathematically proven [1]. A significant theme is the **logic of composing cryptographic building blocks** in secure ways [1, 2].

However, this book is **not** intended as a practical handbook for choosing specific algorithms, a guide for securely implementing production-ready libraries, a discussion of specific cryptographic software (like PGP, Tor, Signal, TrueCrypt) or cryptocurrencies (like Bitcoin), nor will it teach you how to become a hacker [2].

The book is aimed at anyone who needs to secure information with cryptography and is curious about what makes things "secure" or "insecure" [2]. For the best understanding, a solid foundation in **discrete mathematics** (including modular arithmetic, discrete probabilities, combinatorics, and proof techniques) is required, typically found in a second or third-year undergraduate CS program [3]. Background in algorithms, data structures, and theory of computation is also recommended, as the book deals with computations and algorithms at a high level of abstraction and with mathematical rigor [4].

Cryptography has a reputation for being difficult due to math, but the author argues it's more about the **high level of abstraction** [4, 5]. While concrete examples can illustrate *what* an algorithm does, they **cannot illustrate *why* an algorithm is secure** [6]. Security is a **global property** of a system across all possible inputs, not demonstrable by example [7]. Often, security definitions state that "the thing is secure if its outputs look like random junk," which means concrete examples of working algorithms will show meaningless garbage, offering little insight [7]. To truly understand security, one must come to terms with these abstract ideas [8].

A foundational concept in cryptography is **Kerckhoffs' Principle**, which states that the **security of a cryptographic system should depend only on the secrecy of the key, not on the secrecy of the algorithms** themselves [9]. This means the encryption (Enc) and decryption (Dec) algorithms, as well as the key generation (KeyGen) process, are assumed to be public knowledge [9, 10]. If a key is compromised, a new one can be chosen, rather than needing to invent entirely new algorithms [9].

The basic scenario involves **Alice sending a plaintext message (m) to Bob, while keeping its contents hidden from an eavesdropper, Eve** [11, 12]. Alice transforms `m` into a ciphertext (`c`) using an **encryption algorithm (Enc)** and a **secret key (k)** [9, 12]. Bob uses a corresponding **decryption algorithm (Dec)** and the same secret key `k` to recover `m` [12]. The collection of KeyGen, Enc, and Dec algorithms forms an **encryption scheme** [10].

Important limitations or "non-cryptographic" aspects discussed include:
*   **Hiding the fact of communication (steganography)** is not addressed [13].
*   **Reliable delivery of ciphertexts** is assumed [14].
*   Initially, the focus is on **passive eavesdropping**, not active tampering with messages (though active attacks are considered later) [14].
*   **Key distribution** (how Alice and Bob initially obtain a shared secret key) is a crucial but separate problem discussed later [14].
*   **Key management** (how keys are kept secret after establishment) is also distinct [15].
*   The assumption of **uniformly random strings** is fundamental; obtaining true randomness from deterministic computers is a real-world challenge [15].
*   **Encoding methods like base64** do not provide security as they involve no secret information [16]. Representing data in binary also offers no security [17].

### 2. Provable Security

Provable security is a cornerstone of modern cryptography, allowing us to **formally define what it means for a system to be secure and then mathematically prove claims about its security** [1, 18]. This contrasts with historical cryptography, where finding ways to break schemes was a continuous "cat-and-mouse game" [18].

Key aspects of security definitions:
*   **Not Syntax or Correctness:** A security definition does not specify the inputs/outputs of algorithms (syntax) [19, 20] nor does it guarantee that decryption correctly recovers the original plaintext (correctness) [21, 22]. These are separate, functional properties.
*   **Attacker's View:** Security definitions always consider the **attacker's view of the system** and the "interface" that legitimate users expose to the attacker [23, 24].

Two prominent styles of security definitions are introduced:
*   **"Real-vs-Random" Style (Uniform Ciphertexts - Definition 2.5):** An encryption scheme is considered good if its **ciphertexts look like random junk to an attacker** [23]. This is formalized by comparing two subroutines: `LΣ_ots$-real` (which generates a ciphertext by genuinely encrypting a plaintext) and `LΣ_ots$-rand` (which generates a ciphertext by simply picking a random string from the ciphertext space) [25]. If an attacker (calling program) cannot distinguish between these two implementations, the scheme has uniform ciphertexts [25, 26].
*   **"Left-vs-Right" Style (One-time Secrecy - Definition 2.6):** An encryption scheme is good if **encryptions of a chosen plaintext `m_L` look identical to encryptions of another chosen plaintext `m_R` to an attacker** [27]. This is formalized by comparing `LΣ_ots-L` (encrypting `m_L`) and `LΣ_ots-R` (encrypting `m_R`) [28]. The attacker provides both `m_L` and `m_R` and receives an encryption of one, without knowing which [29]. If they are indistinguishable, the scheme has one-time secrecy [30].

The book employs a **"code-based games" philosophy** for defining and proving security [31]:
*   **Libraries:** Security definitions are expressed as the **indistinguishability of two "libraries"** [31]. Libraries are collections of subroutines and private variables, with a common interface/API but different internal implementations [31, 32].
*   **Adversary as Calling Program:** An adversary is modeled as any **calling program** on the library's interface [31, 32]. The adversary controls arguments to subroutines and sees return values, but cannot see private variables within the library [31].
*   **Consistent Framework:** This approach provides a consistent framework for both proving and breaking security [33].
    *   **Breaking Security:** Corresponds to **writing a calling program (a "distinguisher")** that expects a particular interface and **behaves as differently as possible** in the presence of the two implementations [33, 34]. This involves computing output probabilities for the distinguisher when linked to each library and showing a non-negligible difference [35, 36].
    *   **Proving Security (Hybrid Technique):** Involves showing a **sequence of "hybrid" libraries**, where each hybrid is indistinguishable from the previous one, connecting the "real" and "ideal" libraries [33, 37, 38]. This breaks down a large proof into smaller, more manageable steps [38]. The steps often involve syntactic rewriting rules like inlining subroutines or factoring out statements [33]. It helps avoid complex "contrapositive" arguments common in conventional proofs [39].

**One-Time Pad (OTP)** (Construction 1.1) serves as a key illustrative example:
*   **Mechanism:** `KeyGen` chooses `k` uniformly from `{0,1}^λ`. `Enc(k,m) = k ⊕ m`. `Dec(k,c) = k ⊕ c` [40].
*   **Correctness (Claim 1.2):** `Dec(k, Enc(k,m)) = m` is always true, demonstrating that Bob can recover the message [41, 42].
*   **Security (Claim 1.3/2.7):** OTP satisfies the **one-time uniform ciphertexts property** because if the key is chosen uniformly and kept secret, the ciphertext appears uniformly distributed to an attacker [43, 44]. This also implies it satisfies one-time secrecy [30].
*   **The "Paradox":** While `c` can be decrypted to `m` if `k` is known (Alice & Bob's view), `c` reveals no information about `m` if `k` is unknown (Eve's view). This highlights the **importance of the secret key** [45, 46].
*   **Limitations:** OTP keys must be **as long as the plaintext** and can be used to **encrypt only one plaintext** (hence "one-time") [47]. Reusing a key leaks information about the XOR of plaintexts [48].

An example of an **insecure scheme** (Construction 2.8), where `Enc(k,m) = k & m` (bitwise AND), is used to demonstrate how to break security. This scheme does not have one-time uniform ciphertexts or one-time secrecy because `k & 0^λ` always results in `0^λ`, a predictable pattern that a distinguisher can exploit [34, 36, 49, 50].

Comparing security definitions, it's shown that if a scheme has one-time uniform ciphertexts, it **implies** one-time secrecy (Theorem 2.15) [51, 52]. However, the reverse is not always true; a scheme can have one-time secrecy but not uniform ciphertexts (e.g., OTP with "00" appended to ciphertexts - Theorem 2.16) [53, 54]. This helps illuminate the nuances of the definitions [55].

### 3. Computational Security

John Nash's profound insight was that **security does not require attacks to be impossible, only computationally infeasible** [56, 57]. This is the foundation of modern cryptography.

Key concepts in computational security:
*   **Security Parameter (λ):** This is a configurable "knob" that allows users to tune the desired level of security [58, 59]. For example, a brute-force attack (trying all possible keys) against a `λ`-bit key scheme would take `2^λ` steps [58]. Increasing `λ` exponentially increases the difficulty of such attacks [59].
*   **Asymptotic Running Time (Polynomial Time):** Cryptography aims to ensure that **no polynomial-time attack can successfully break security** [60]. Attacks requiring exponential time are generally considered infeasible and are not worried about [60]. A key property of polynomial-time processes is their **closure property**: repeating a polynomial-time process a polynomial number of times still results in an overall polynomial-time process [60].
    *   For numerical algorithms involving large numbers (e.g., thousands of bits), the security parameter is `n = log_2 N` (the number of bits to represent `N`), not `N` itself [61]. Algorithms are judged on whether they run in polynomial time *as a function of `n`* [61].
    *   Some numerical operations are computationally efficient (polynomial-time), while others are not known to be (e.g., factoring integers, discrete logarithm) on classical computers [62]. Interestingly, these "hard" problems often have efficient solutions on quantum computers [62].
*   **Negligible Probability (Definition 4.2):** An attack's success probability must be **negligibly small** [63]. A function `f(λ)` is negligible if, for every polynomial `p(λ)`, `lim (λ→∞) p(λ)f(λ) = 0` [64]. This means the probability approaches zero so fast that even multiplying it by a polynomial (representing a polynomial number of attack attempts) still results in a value that approaches zero [64].
    *   Examples of negligible functions: `1/2^λ`, `1/2^√λ` [65].
    *   Examples of non-negligible functions: `1/λ^5` (because `λ^6 * (1/λ^5)` goes to infinity, not zero) [65].
*   **Indistinguishability (f ≈ g or f ∼∼ g - Definition 4.4, Definition 4.5):** Two functions `f` and `g` are indistinguishable if their **absolute difference `|f(λ) - g(λ)|` is a negligible function** [66]. This concept is central to security definitions, meaning that a polynomial-time adversary cannot distinguish between two scenarios with more than a negligible advantage [66, 67]. Indistinguishability is also transitive, allowing for hybrid proofs [68].
*   **Birthday Probabilities:** This concept is crucial for understanding collision probabilities in cryptography.
    *   The **Birthday Paradox** states that in a set of `q` randomly chosen people, the probability that at least two will share a birthday is surprisingly high [69]. In cryptography, this translates to finding collisions. For `N` possible values, the probability of a collision becomes significant (around 0.5) after approximately `sqrt(N)` samples [69, 70].
    *   This is formalized with two libraries, `Lsamp-L` (samples with replacement) and `Lsamp-R` (samples without replacement) [71]. A calling program making `q` calls can distinguish them with an advantage of `BirthdayProb(q, 2^λ) = Θ(q^2 / 2^λ)` [72]. If `q` is polynomial in `λ`, this advantage is negligible [72].
    *   However, if `q` approaches `2^(λ/2)` (the square root of the keyspace size), the probability of collision becomes non-negligible, leading to **"birthday bound security,"** where a scheme offers effectively `λ/2` bits of security [73]. This informs the size of keys chosen in practice [74].
    *   A generalization (Lemma 4.12) extends this: if at each step, there are only polynomially many "problematic" values (e.g., values that would cause a collision or a specific event), the probability of choosing one of them is negligible [74, 75].

### 4. Pseudorandomness (Pseudorandom Generators and Pseudorandom Functions)

Pseudorandomness is a core concept that allows short secret keys to be "stretched" into long, seemingly random sequences or functions, enabling efficient cryptography.

#### Pseudorandom Generators (PRGs)

*   **Motivation:** One-time pad requires a key as long as the plaintext [76]. If Alice and Bob share a short `λ`-bit secret key `k` but need to encrypt a much longer plaintext, a PRG `G` can expand `k` into a long pseudorandom string `G(k)` which can then be used as a one-time pad [76, 77].
*   **Definition (Definition 5.1):** A deterministic function `G: {0,1}^λ → {0,1}^(λ+l)` (where `l > 0` is the **stretch**) is a secure PRG if its output distribution (when its input `s` is chosen uniformly at random) is **indistinguishable from a truly uniform random distribution** of the same length [78, 79]. This is formalized by comparing `L_G_prg-real` (outputs `G(s)`) and `L_G_prg-rand` (outputs a truly random string) [79].
*   **Perspective:** While a PRG's output `G(k)` cannot be *perfectly* uniform (as there are only `2^λ` possible outputs in a `2^(λ+l)` space), it is "close enough" for practical purposes if it's computationally indistinguishable from uniform [80, 81].
*   **Crucial Point:** **Randomness and pseudorandomness are properties of the *process* used to generate a string, not of individual strings themselves** [82, 83]. A specific string cannot be "random" or "pseudorandom"; rather, it was "chosen pseudorandomly" [82].
*   **Statistical Tests:** A PRG's security implies it passes all polynomial-time statistical tests, meaning no polynomial-time algorithm can find a discernible pattern in its outputs [84, 85].
*   **In Practice:** There are currently **no *proven* secure PRGs**; proving their existence would resolve the P vs. NP problem [86]. Cryptography relies on **candidate PRGs** that have withstood extensive public scrutiny [87]. Often, practical PRGs are built from **block ciphers** [88].
*   **"How NOT to Build a PRG":** A simple, insecure PRG is `G(s) = s‖s` (repeating the input) [89]. This is insecure because an attacker can easily distinguish it from a truly random string by checking if the first and second halves are identical [90, 91]. The distinguishing advantage is non-negligible (`1 - 1/2^λ`) [83].
*   **Application (Pseudo-OTP):** If `G` is a secure PRG, then `Enc(k,m) = G(k) ⊕ m` (Construction 5.2) provides **computational one-time secrecy** (Definition 5.3) [92-94]. The proof proceeds with hybrids, replacing `G(k)` with a truly random string `z`, then leveraging the perfect secrecy of OTP `z ⊕ m` [95-98].
*   **PRG-Feedback (Construction H1 vs. H2):** This illustrates a common pitfall in composing PRGs.
    *   `H1(s) = G(s) = x‖y; G(y) = u‖v; return x‖u‖v` is a **secure** PRG (if G is secure) [99-104]. The key intuition is that `y` is indistinguishable from random, so `G(y)`'s output `u‖v` is also indistinguishable from random, and `x` is also indistinguishable from random, making the combined output `x‖u‖v` indistinguishable from random [105].
    *   `H2(s) = G(s) = x‖y; G(y) = u‖v; return x‖y‖u‖v` is **insecure** [99, 106]. It leaks `y` (the input to the second `G` call) as part of the output, creating a discernible pattern that an attacker can check (`G(y) == u‖v`) [107, 108]. The proof of security breaks down because `y` is used in a way that doesn't allow its outputs to be treated as independent of its input `s` [106, 109].
*   **Symmetric Ratchet (Construction 5.9):** A stream cipher application where keys are updated iteratively using a PRG (`s_i‖t_i = G(s_i-1)`), and `t_i` is used for encryption [110, 111]. This provides **forward secrecy**: if a key `s_n` is compromised, future messages encrypted with `t_n+1, t_n+2, ...` are compromised, but **past messages encrypted with `t_1, ..., t_n` remain secure** because `s_n` does not reveal `s_n-1` (turning the ratchet backwards is hard) [111, 112]. The proof shows `n` ciphertexts remain pseudorandom even with `s_n` compromise [113-116].

#### Pseudorandom Functions (PRFs)

*   **Motivation:** To achieve the effect of a huge, shared table of random data (`T[x]`) that Alice and Bob can both access with a short key `k`, allowing them to encrypt many messages securely using `F(k,r) ⊕ m` [117-119].
*   **Definition (Definition 6.1):** A deterministic function `F: {0,1}^λ × {0,1}^in → {0,1}^out` is a secure PRF if, when its seed `k` is chosen uniformly, its input-output behavior (via a `lookup(x)` subroutine that returns `F(k,x)`) is **indistinguishable from a "randomly initialized lookup table"** [120-124]. The "random lookup table" (`L_F_prf-rand`) is populated **lazily/on-demand** by sampling outputs uniformly for each queried input `x` [122, 123].
*   **Discussion:** A PRF emulates a function chosen uniformly from *all possible functions* mapping `in` bits to `out` bits [124]. The key `k` selects one of `2^λ` such functions [125]. Unlike PRGs, the `lookup` subroutine of a PRF takes an input (`x`) [124].
*   **"How NOT to Build a PRF":** `F(k,x) = G(k) ⊕ x` (where `G` is a PRG) is **not a secure PRF** [126]. While `G(k) ⊕ x` looks pseudorandom for a single call, making *two* calls (`lookup(x1)` and `lookup(x2)`) reveals a pattern: `(G(k) ⊕ x1) ⊕ (G(k) ⊕ x2) = x1 ⊕ x2` [127]. An attacker can distinguish this from a truly random function where `z1 ⊕ z2` would be random, not `x1 ⊕ x2` [128, 129]. This highlights the challenge of ensuring independence of multiple outputs derived from a single short seed [130].
*   **Constructing a PRG from a PRF (Counter PRG - Construction 6.2):** A practical and common way to get a PRG. For example, a length-doubling PRG `G(s)` can be constructed as `F(s, 0...00) ‖ F(s, 0...01)` [131]. The security proof (Claim 6.3) uses a **variable hybrid technique** [132, 133]. It shows that `G` is a secure PRG because the outputs of `F` on distinct inputs (like `0...00` and `0...01`) are indistinguishable from uniform [132, 134-138].
*   **Theoretical Construction of a PRF from a PRG (GGM PRF - Construction 6.4):** This theoretical construction (by Goldreich, Goldwasser, and Micali) builds a PRF by chaining PRGs together in a binary tree structure [139]. `F(k,x)` involves traversing a path from the root (seeded with `k`) to a leaf corresponding to `x`, applying PRG functions at each node [140, 141]. Its security (Claim 6.5) is proven using a hybrid argument over the depth of the tree [142-146].

### 5. Pseudorandom Functions and Block Ciphers

This section delves into the relationship between PRFs and block ciphers, which are fundamental building blocks in practical cryptography.

*   **Block Ciphers (Pseudorandom Permutations - PRPs):**
    *   **Definition (Definition 6.6):** A block cipher `F: {0,1}^λ × {0,1}^blen → {0,1}^blen` is essentially a PRF where the input length (`in`) equals the output length (`out`), and for every key `k`, the function `F(k, ·)` is **guaranteed to be invertible** (`F⁻¹` exists) [146, 147].
    *   **Security:** A secure PRP is indistinguishable from a **randomly chosen *invertible* function** (permutation) [147, 148]. This is reflected in `L_F_prp-rand` which samples values without replacement (`{0,1}^blen \ T.values`) to ensure distinct outputs for distinct inputs [147, 149].
    *   **Invertibility:** Both `F` and `F⁻¹` require knowledge of the secret key `k` to compute [150].
*   **Relating PRFs and Block Ciphers:**
    *   **PRP Switching Lemma (Lemma 6.7):** For `blen = λ` (where `blen` is the blocklength), a randomly chosen permutation (`L_prp-rand`) is **indistinguishable from a randomly chosen unrestricted function** (`L_prf-rand`) [151, 152]. This is because a polynomial-time adversary can only query a negligible fraction of the exponentially large domain, making it highly unlikely to detect that the function is a permutation [151].
    *   **Corollary 6.8:** As a direct consequence of the switching lemma, **every secure PRP (with `blen = λ`) is also a secure PRF** [153, 154]. This is very important for practical use, as it means a good block cipher can be used as a PRF.
    *   **Feistel Construction:** This is a general method to build invertible functions from non-invertible ones, used in many block ciphers. A single Feistel round `F*(x‖y) = y‖(F(y) ⊕ x)` (Construction 6.9) is always invertible, regardless of the underlying function `F` [155]. A **Feistel cipher** (Construction 6.11) applies multiple Feistel rounds in succession, typically with different "round keys" [156, 157].
        *   While a single keyed Feistel round `F*(k, x‖y) = y‖(F(k,y) ⊕ x)` is invertible, it's not a secure PRP (it trivially leaks half of its input) [156].
        *   The **Luby-Rackoff Theorem (Theorem 6.14)** states that if `F` is a secure PRF, then a **3-round Feistel cipher** is a secure PRP [158]. (A 4-round Feistel cipher is a secure SPRP).
*   **Block Ciphers in Practice:**
    *   Block ciphers are a cornerstone of modern cryptography [158]. While they can be built from PRFs/PRGs in principle, in practice, they are often designed "from scratch" (e.g., AES) [158].
    *   The **Advanced Encryption Standard (AES)** is a prime example [159]. It was chosen through a competition, subjected to intense public scrutiny, and no significant weaknesses are known [159, 160]. AES has a **blocklength of 128 bits** and supports key lengths of 128, 192, and 256 bits [160].
    *   Thanks to the PRP switching lemma, **AES can be directly used as a secure PRF**. Also, it can be used to construct a simple PRG (like the Counter PRG, Construction 6.2) [160]. The security of these constructions is guaranteed to be as good as the PRP-security of AES itself [160].
*   **Strong Pseudorandom Permutations (SPRPs - Definition 6.13):**
    *   A stronger notion of PRP where the distinguisher can query **both the forward function `F` and its inverse `F⁻¹`** [161, 162].
    *   `L_F_sprp-rand` maintains two consistent associative arrays (`T` and `Tinv`) to simulate a random permutation queryable in both directions [162, 163].
    *   The Luby-Rackoff Theorem states that a **4-round Feistel cipher** (with a secure PRF as its round function) is a secure SPRP [164, 165].

### 6. Security Against Chosen-Plaintext Attacks (CPA Security)

The CPA security definition addresses the more practical scenario where a single key is used to encrypt **many plaintexts** [166].

*   **Definition (Definition 7.1):** An encryption scheme `Σ` has CPA security if `L_Σ_cpa-L` is indistinguishable from `L_Σ_cpa-R` [167].
    *   Both libraries perform key generation (`k ← Σ.KeyGen`) once at initialization, and this **key remains static** for all subsequent encryption calls [167].
    *   The `eavesdrop(m_L, m_R)` subroutine is called multiple times by the adversary, and it encrypts either `m_L` (in `L_Σ_cpa-L`) or `m_R` (in `L_Σ_cpa-R`) [167].
    *   This is often called "IND-CPA" (indistinguishability of ciphertexts under chosen-plaintext attack) [167].
*   **Limits of Deterministic Encryption:**
    *   A bare block cipher (used "as-is" for encryption) is **NOT CPA-secure** [168]. This is because it is **deterministic**: encrypting the same plaintext twice with the same key produces the identical ciphertext [169].
    *   An attacker can exploit this by requesting `eavesdrop(0^blen, 0^blen)` to get `c1` and `eavesdrop(0^blen, 1^blen)` to get `c2`. If `c1 = c2`, the attacker knows they are linked to `L_Σ_cpa-L` (where both plaintexts were `0^blen`); if `c1 != c2`, they are in `L_Σ_cpa-R` (where `0^blen` and `1^blen` were encrypted) [170, 171].
    *   **Key takeaway: Deterministic encryption can NEVER be CPA-secure** because it leaks whether two ciphertexts encode the same plaintext, which violates the security goal [169, 172].
*   **Avoiding Deterministic Encryption:**
    *   **Randomized Encryption:** The `Enc` algorithm incorporates fresh, independent randomness for each encryption. This is the most common approach for CPA security [173]. The PRF-based scheme (Construction 7.4) is an example.
    *   **Stateful Encryption:** The `Enc` or `Dec` algorithms modify a shared state (e.g., the key itself, like in the symmetric ratchet). This ensures different ciphertexts for repeated plaintexts but is fragile if synchronization is lost [174].
    *   **Nonce-Based Encryption:** An additional input called a **nonce** ("number used only once") is passed to Enc and Dec. The nonce doesn't need to be random or secret, but it **must be distinct for every encryption** under the same key [175]. The CPA definition can be adapted to enforce this, with an error if the adversary attempts to reuse a nonce [175, 176].
*   **Pseudorandom Ciphertexts (CPA$ Security - Definition 7.2):**
    *   A stronger form of CPA security where ciphertexts of *any* plaintext look uniform [177, 178].
    *   `L_Σ_cpa$-real` generates real ciphertexts, while `L_Σ_cpa$-rand` generates truly random strings from the ciphertext space `Σ.C` (adapted for variable lengths as `Σ.C(|m|)`) [178, 179].
    *   **`CPA$ security implies CPA security` (Claim 7.3)** [180-183]. This is proven with a hybrid argument, similar to the one-time case.
*   **CPA-Secure Encryption Based on PRFs (Construction 7.4):**
    *   Uses a secure PRF `F` (with `in = λ`) to achieve randomized CPA security [184].
    *   **Mechanism:** `Enc(k,m)`: choose a random `r ← {0,1}^λ`, then output `(r, F(k,r) ⊕ m)` [184]. `F(k,r)` acts as a one-time pad.
    *   **Security (Claim 7.5):** This scheme has CPA$ security (and thus CPA security) if `F` is a secure PRF [185]. The proof (explained via a Socratic dialogue) relies on:
        1.  `r` being uniformly random.
        2.  `F(k,r) ⊕ m` looking like a one-time pad because `F(k,r)` appears pseudorandom.
        3.  The **`r` values being distinct** across multiple encryptions (highly probable due to the birthday bound) [186]. If `r` values are distinct, then the PRF outputs `F(k,r)` are (computationally) independent and uniform [186, 187].
        4.  The proof uses hybrids, including the "sampling without replacement" lemma (Lemma 4.11) to justify treating `r` values as distinct, even if they are initially sampled with replacement [188, 189].
*   **Variable-Length Plaintexts and Length Leakage:**
    *   Most practical encryption schemes (like block cipher modes) leak the **length** of the plaintext [190, 191]. This means they don't strictly satisfy the original CPA definition (which implies hiding *all* information).
    *   The CPA definition is thus revised to **disallow queries where `|m_L| != |m_R|`** [179, 192]. The `CPA$` definition is similarly revised to ensure `L_Σ_cpa$-rand` produces ciphertexts of the correct length for a given plaintext length `|m|` [179, 193].
    *   While unavoidable for arbitrary-length plaintexts, **length leakage can lead to serious traffic analysis attacks** (e.g., inferring language, words, or speaker identity from encrypted voice chat) [194, 195].

### 7. Block Ciphers in Practice (Encryption Modes)

Block cipher modes are standardized ways to use a block cipher (which operates on fixed-size blocks) to **encrypt arbitrary-length data** [196]. All modes mentioned here assume the use of a secure block cipher `F` (or PRF for some modes).

*   **ECB: Electronic Codebook (NEVER USE THIS!):**
    *   **Mechanism (Construction 8.1):** The simplest, but most insecure. Each plaintext block `m_i` is encrypted independently: `c_i = F(k, m_i)` [197].
    *   **Insecurity:** It does **not provide CPA security** [197]. If two plaintext blocks are identical, their corresponding ciphertext blocks will also be identical, revealing patterns in the plaintext. For example, patterns in images encrypted with ECB mode are clearly visible [197].
*   **CBC: Cipher Block Chaining:**
    *   **Mechanism (Construction 8.2):** A **random Initialization Vector (IV)** (`c0`) is chosen for each encryption [198]. Each plaintext block `m_i` is XORed with the *previous ciphertext block* (`c_i-1`) before being encrypted: `c_i = F(k, m_i ⊕ c_i-1)` [199]. The `IV` acts as `c_0`.
    *   **Randomized Encryption:** CBC mode is a randomized encryption scheme due to the random IV, which is necessary for CPA security [198].
    *   **Inter-block Dependency:** The chaining mechanism ensures that each ciphertext block depends on all previous plaintext blocks, hiding patterns [199].
*   **CTR: Counter Mode:**
    *   **Mechanism (Construction 8.3):** A **random IV (`r`)** is chosen [200]. A **keystream** is generated by encrypting a sequence of counter values starting from `r`: `F(k,r), F(k,r+1), F(k,r+2), ...` [200]. Each plaintext block `m_i` is then XORed with the corresponding keystream block: `c_i = F(k,r) ⊕ m_i`, where `r` increments after each block [200]. The IV `r` is sent as `c0`.
    *   **No F⁻¹ required:** CTR mode only uses the forward block cipher `F`, not its inverse `F⁻¹` [201]. This means it can be instantiated with a PRF, not strictly a PRP.
*   **OFB: Output Feedback Mode:**
    *   **Mechanism (Construction 8.4):** Similar to CTR, it also generates a keystream by iteratively applying the block cipher, but instead of incrementing a counter, it **feeds the *output* of the previous block cipher application back as the *input* to the next** [202]. `F(k,r), F(k, F(k,r)), F(k, F(k,F(k,r))), ...` These blocks are then XORed with the plaintext [202].
    *   **No F⁻¹ required:** Like CTR, OFB also only uses the forward block cipher `F` [203].
    *   **Security (Claim 8.5):** OFB mode has **CPA$ security** if `F` is a secure PRF [203]. The proof is similar to the PRF-based encryption scheme (Construction 7.4), demonstrating that inputs to the PRF are distinct (due to the iterated output feedback and birthday bound), ensuring pseudorandomness of the keystream [204-207].
*   **Compare & Contrast (CBC vs. CTR - and OFB similarities):**
    *   **`F⁻¹` Requirement:** CTR (and OFB) do not require the block cipher's inverse, while CBC does for decryption [201].
    *   **Parallelization:** **CTR encryption can be parallelized** (each `F(k, r+i)` can be computed independently), while CBC encryption is inherently sequential [208]. Both have parallelizable decryption [208].
    *   **Pre-computation:** **CTR allows keystream pre-computation** (only IV affects `F` inputs), unlike CBC where plaintext influences `F` inputs [208].
    *   **Variable-Length Plaintexts:** CTR is relatively easy to adapt for arbitrary plaintext lengths without complex padding schemes [209].
    *   **IV Reuse:** **IV reuse is devastatingly insecure for CTR mode** (leads to plaintext leakage) [361, 394b]. For CBC mode, IV reuse can be safer if the first plaintext blocks differ [361, 394a]. This makes CBC mode more robust against common implementation errors [209].
*   **Padding & Ciphertext Stealing:**
    *   **Padding:** Methods to make arbitrary-length data a multiple of the blocklength for block ciphers [210].
        *   **`pad`:** Adds bytes to achieve block alignment.
        *   **`unpad`:** Reversible process to remove padding and recover original data [211].
        *   Examples: Null padding (problematic) [212], ANSI X.923 (last byte indicates length), PKCS#7 (padding bytes equal padding length) [212, 213]. Padding schemes themselves are not the source of insecurity but can enable attacks when misused [214].
    *   **Ciphertext Stealing (CTS):** A technique to handle partial last blocks **without adding a full extra padding block** [214]. It modifies the last two ciphertext blocks in CBC mode to encrypt the partial last block and ensure the ciphertext length matches the plaintext length plus one block (for the IV) [215-218].

### 8. Diffie-Hellman Key Agreement

Diffie-Hellman (DH) Key Agreement is a landmark protocol, being the **first published instance of public-key cryptography** [219]. It allows two parties to establish a shared secret key over an insecure, public channel without any prior shared secrets [219].

*   **Cyclic Groups (Section 14.1):**
    *   A **cyclic group** `G` is generated by a single element `д` (the **generator**), meaning `G = {д^i % n | i ∈ Z}` where `n = |G|` is the order of the group [220].
    *   **Modular exponentiation (`д^x % n`)** is computationally easy [221].
    *   The **Discrete Logarithm Problem (DLP)** is the inverse: given `д` and `X = д^x`, finding `x` is conjectured to be computationally hard in certain groups [219, 221].
*   **Diffie-Hellman Protocol (Construction 14.3):**
    *   **Public Parameters:** Alice and Bob publicly agree on a cyclic group `G` and a generator `д` [222].
    *   **Steps:**
        1.  **Alice** chooses a random secret integer `a` (from `Z_n`) and computes `A = д^a`. She sends `A` to Bob [222].
        2.  **Bob** chooses a random secret integer `b` (from `Z_n`) and computes `B = д^b`. He sends `B` to Alice [222].
        3.  **Alice** computes the shared key `K = B^a = (д^b)^a = д^ab` [222].
        4.  **Bob** computes the shared key `K = A^b = (д^a)^b = д^ab` [222].
    *   Both parties arrive at the same shared secret `д^ab`, which an eavesdropper (seeing only `д^a` and `д^b`) cannot easily compute due to the hardness of the DLP [223].
*   **Defining Security for Key Agreement (KA Security - Definition 14.4):**
    *   The protocol generates a **transcript** (the public messages exchanged, e.g., `(A, B)`) and a **secret key** (`K`) [223].
    *   **Security Goal:** The transcript should reveal **no useful information** about the key [224]. Specifically, the key should appear **pseudorandom** to an eavesdropper given the transcript [225].
    *   **Formalization:** `L_Σ_ka-real` (returns `(transcript, K)`) must be indistinguishable from `L_Σ_ka-rand` (returns `(transcript, K')` where `K'` is a randomly chosen, independent key) [226].
*   **Decisional Diffie-Hellman (DDH) Problem (Definition 14.5):**
    *   The security of the DHKA protocol is **equivalent to the Decisional Diffie-Hellman (DDH) assumption** holding true for the chosen group `G` [227, 228].
    *   **DDH Assumption:** It is computationally infeasible to distinguish between a "real" DDH triple `(д^a, д^b, д^ab)` and a "random" triple `(д^a, д^b, д^c)` (where `a,b,c` are random and independent) [229].
    *   **Important Caveat: DDH assumption is FALSE in `Z_p*` (integers modulo a prime `p`)** [228].
        *   **Euler's Criterion (Claim 14.7)** allows an attacker to determine the parity of the exponent of `X = д^x` (i.e., whether `x` is even or odd) from `X` alone, by computing `X^((p-1)/2) % p` [230].
        *   This allows a DDH distinguisher in `Z_p*`: `д^ab`'s exponent `ab` is even with probability 3/4 (unless `д` is not a primitive root), while `д^c`'s exponent `c` is even with probability 1/2. This difference in parity distribution allows an attacker to distinguish the real from the random tuple [230].
        *   **Better Groups:** To ensure DDH holds, groups like **quadratic residues modulo a safe prime `p` (`QR_p*`)** are used, where `p` is a prime such that `(p-1)/2` is also prime (Sophie Germain prime) [231, 232].

### 9. Public-Key Cryptosystems (ElGamal)

Public-key (or asymmetric) encryption schemes utilize **different keys for encryption and decryption** [233]. The **public key (pk)** can be freely distributed to anyone, allowing them to encrypt messages for the key's owner [233]. Only the owner, possessing the **secret/private key (sk)**, can decrypt these messages [233].

*   **Syntax:**
    *   `KeyGen`: Outputs a pair `(pk, sk)` [234].
    *   `Enc`: Takes `pk` and plaintext `m` as input, outputs ciphertext `c` [234].
    *   `Dec`: Takes `sk` and ciphertext `c` as input, outputs plaintext `m` [234].
*   **Correctness:** `Dec(sk, Enc(pk, m)) = m` (with high probability, as `Enc` can be randomized) [234].
*   **CPA Security for Public-Key Encryption (Definition 15.1):**
    *   Similar to symmetric CPA, allowing many chosen-plaintext queries [235].
    *   **Key Difference:** The adversary explicitly gains access to the `public key` via a `getpk()` subroutine, as `pk` is public knowledge [235, 236].
    *   Just like symmetric-key, **deterministic public-key encryption is NOT CPA-secure** (it still leaks if two plaintexts are identical) [236].
*   **CPA$ Security for Public-Key Encryption (Definition 15.2):**
    *   Similar to symmetric CPA$, requiring ciphertexts to look pseudorandom [237].
    *   **`CPA$ security implies CPA security` (Claim 15.3)** for public-key encryption, similar to the symmetric case [238].
*   **One-Time Security Implies Many-Time Security (Claim 15.5):**
    *   A **unique property of public-key encryption** [239]: if a public-key scheme is secure when an adversary sees only one ciphertext (one-time secrecy), it is also secure when the adversary sees many ciphertexts (CPA-secure) [239].
    *   This contrasts with symmetric-key schemes (like OTP) where one-time security doesn't imply many-time security [239].
    *   The formal `pk-ots` definition (Definition 15.4) allows the adversary to obtain `pk` before querying `challenge` (which is limited to one call) [240, 241].
    *   The proof (Claim 15.5) leverages the fact that the **adversary can compute encryptions using the public key `pk` themselves**, allowing for a "chain" of hybrids where `m_L` is replaced by `m_R` one query at a time [242-245].
*   **ElGamal Encryption (Construction 15.6):**
    *   A prominent public-key encryption scheme **based on the Diffie-Hellman Key Agreement protocol** [246].
    *   **Public Parameters:** A cyclic group `G` and its generator `д` [246].
    *   **Keys:** `sk = a ∈ Z_n` (Alice's secret exponent), `pk = A = д^a` (Alice's public key) [246].
    *   **Encryption `Enc(A, M)`:** To encrypt message `M ∈ G` for Alice:
        1.  Choose random `b ∈ Z_n`.
        2.  Compute `B = д^b` (Bob's ephemeral public key).
        3.  Compute `X = M · A^b` (message masked with the shared secret `A^b`).
        4.  Ciphertext is `(B, X)` [246].
    *   **Decryption `Dec(a, (B, X))`:** To decrypt ciphertext `(B, X)` using secret key `a`:
        1.  Compute `B^a = (д^b)^a = д^ab`.
        2.  Recover message `M = X · (B^a)⁻¹ = (M · д^ab) · (д^ab)⁻¹ = M` [246].
    *   **Security (Claim 15.7):** ElGamal is **CPA$ secure if the Decisional Diffie-Hellman (DDH) assumption holds in group `G`** [247, 248].
        *   Intuition: The value `д^ab` (the mask `M` is multiplied by) looks random to an adversary if DDH holds, making `X` appear as `M` masked with a random value [247].
        *   The proof involves hybrids that replace the actual `д^ab` with a truly random group element `д^c` (leveraging the DDH assumption) [249-252].
*   **Hybrid Encryption (Construction 15.8):**
    *   **Motivation:** Public-key encryption is generally **much more computationally expensive** than symmetric-key encryption, especially for long messages [253].
    *   **Mechanism:** To encrypt a large plaintext `m`:
        1.  Generate a **temporary symmetric key `tk`** using `Σsym.KeyGen` [254].
        2.  **Encrypt `tk` using the expensive public-key scheme:** `cpub = Σpub.Enc(pk, tk)` [254].
        3.  **Encrypt the actual plaintext `m` using the temporary symmetric key `tk` and the efficient symmetric-key scheme:** `csym = Σsym.Enc(tk, m)` [254].
        4.  The overall ciphertext is `(cpub, csym)` [254].
    *   **Decryption:**
        1.  Use `Σpub.Dec(sk, cpub)` to recover `tk` [254].
        2.  Use `Σsym.Dec(tk, csym)` to recover `m` [254].
    *   **Efficiency:** The expensive public-key operations are only performed on the small `tk`, making it efficient for large `m` [254].
    *   **Security (Claim 15.9):** Hybrid encryption `Σhyb` is **CPA-secure if `Σsym` is a one-time-secret symmetric-key encryption scheme AND `Σpub` is a CPA-secure public-key encryption scheme** [255]. `Σsym` does *not* need full CPA security because `tk` is used only once for a single plaintext [255]. The proof leverages the one-time secrecy of `Σsym` and the CPA security of `Σpub` in a multi-hybrid argument [256-259].

### 10. RSA Cryptosystems

RSA, named after Rivest, Shamir, and Adleman (1978), was one of the **first public-key cryptosystems** [260]. It serves as a building block for both public-key encryption and digital signatures.

*   **Modular Arithmetic Background:** RSA heavily relies on modular arithmetic concepts:
    *   **`Z_n`:** The set of integers `{0, 1, ..., n-1}` [261].
    *   **Congruence (`≡_n`)** and **modulus operator (`%`)** [261].
    *   **Multiplicative Inverse:** An element `x` has a multiplicative inverse `x⁻¹` modulo `n` if and only if `gcd(x, n) = 1` [262, 263]. The Extended Euclidean Algorithm (`extgcd(x,y)`) can find `a,b` such that `ax + by = gcd(x,y)`, which is useful for finding inverses [263].
    *   **`Z_n*`:** The **multiplicative group modulo `n`**, containing all elements `x` in `Z_n` such that `gcd(x, n) = 1` [262].
*   **RSA Function and its Inverse:**
    *   **Key Generation:** Choose two large distinct prime numbers, `p` and `q`. Compute `N = p * q` (the modulus). Compute **Euler's totient function `ϕ(N) = (p-1)(q-1)`** [264]. Choose a public exponent `e` such that `1 < e < ϕ(N)` and `gcd(e, ϕ(N)) = 1` [264]. Compute the private exponent `d` such that `ed ≡ 1 mod ϕ(N)` (i.e., `d = e⁻¹ mod ϕ(N)`) [264].
    *   **RSA Function (`f(x)`):** `x^e % N`. This is computationally easy to compute with public `N` and `e` [265].
    *   **RSA Inverse Function (`f⁻¹(y)`):** `y^d % N`. This is computationally easy to compute with private `d` and public `N` [265].
    *   **Correctness:** `(x^e)^d ≡ x mod N` and `(x^d)^e ≡ x mod N` hold (even for `x` not in `Z_N*`, though the proof is more involved and uses Chinese Remainder Theorem) [266, 267].
    *   **Efficient Computation:** `x^e % N` for huge numbers is computed using **modular exponentiation by repeated squaring** (or exponentiation by squaring) [268]. Direct computation would be infeasible [268].
*   **Security Properties:**
    *   RSA is a **trapdoor function**: it's easy to compute in one direction (using `e` and `N`) but computationally hard to invert without special "trapdoor" information (`d` or `p,q`) [265].
    *   **The security property:** Given only the public information `N` and `e`, it should be **hard to compute the RSA inverse** (`y^d % N`) on randomly chosen values [265].
    *   **Hardness:** The best known attacks to invert RSA (without `d`) involve **factoring the modulus `N` back into `p` and `q`** [269]. The difficulty of factoring depends on the number of bits in `N` (`n = log_2 N`) [269].
    *   **Practical Sizes:** To resist state-of-the-art factoring algorithms, RSA moduli `N` need to be very large, typically **2048-bit or 4096-bit** (meaning `p` and `q` are each 1024 or 2048 bits long) [270].
*   **"Textbook" RSA Signatures (Construction 13.7):**
    *   **Keys:** `vk = (N, e)` (verification key), `sk = (N, d)` (signing key) [271].
    *   **Sign(`m`):** Computes `σ = m^d % N` [271]. (Assumes `m` is an element of `Z_N`).
    *   **Verify(`vk, m, σ`):** Checks if `σ^e % N == m` [271].
    *   **INSECURE:** Textbook RSA signatures are **not secure** [271]. They are **malleable**; an attacker can easily forge new valid signatures on related messages. For example, if `σ` is a valid signature for `m`, then `σ^2` is a valid signature for `m^2` because `(m^d)^2 = (m^2)^d` [272]. This allows forging signatures on any message `m'` that is an arbitrary power of `m`.
*   **Hashed RSA Signatures (Construction 13.8):**
    *   **Modification:** To overcome the malleability of textbook RSA, a **cryptographic hash function `H`** is applied to the message *before* signing [272].
    *   **Sign(`m`):** Computes `σ = H(m)^d % N` [273].
    *   **Verify(`vk, m, σ`):** Checks if `σ^e % N == H(m)` [273].
    *   **Security:** This thwarts the previous attack because forging a signature on `m'` would require finding `m'` such that `H(m') = H(m)^2`, which is hard if `H` is a good hash function [273]. Its security is proven in the "random oracle model" [273].
*   **Chinese Remainder Theorem (CRT):**
    *   **Application:** CRT can significantly **speed up RSA exponentiation** (both encryption/signature and decryption/verification) when the factors `p` and `q` of `N` are known (i.e., for the private key operations) [274, 275].
    *   **Mechanism:** Instead of computing `X^e % N` directly, one computes `X^e % p` and `X^e % q` separately. Then, CRT is used to combine these two results back into a single result modulo `N` [275]. This is faster because exponentiating modulo `p` and `q` (which are smaller than `N`) is faster than modulo `N`.

### 11. Message Authentication Codes (MACs)

Message Authentication Codes (MACs) are cryptographic primitives that provide **authenticity** for data, ensuring it was generated by someone who knows the secret key, and that it has not been tampered with [276, 277]. Crucially, **authenticity is different from privacy/confidentiality**; a MAC does not hide information, it only certifies its origin and integrity [277]. MACs are a **symmetric-key primitive** [278].

*   **Definition (Definition 10.1):** A MAC scheme for message space `M` consists of:
    *   `KeyGen`: Samples a secret key `k` [279].
    *   `MAC`: A **deterministic** algorithm that takes `k` and message `m ∈ M` as input, and outputs a **tag `t`** [279].
    *   `Ver` (Verification): Implicitly, to verify a tag `t` on a message `m`, one recomputes `MAC(k, m)` and checks if it matches `t` [280]. Both MAC generation and verification require the same secret key `k` [278, 280].
*   **MAC Security Definition (Definition 10.2):**
    *   **Goal:** Only someone with the secret key `k` can generate a valid tag; an adversary cannot produce a **forgery** (a valid `(m, t)` pair where `t` was not legitimately generated by the holder of `k`, especially for a message `m` for which no tag was previously seen) [281].
    *   **Formalization:** Compares `L_Σ_mac-real` (which computes real MACs and verifies correctly) with `L_Σ_mac-fake` (which stores previously generated `(m,t)` pairs and only returns true if an `(m,t)` pair was in this set) [282]. If these two libraries are indistinguishable to a polynomial-time adversary, then the scheme is a secure MAC [282].
    *   The adversary can request valid tags for chosen messages (`gettag`) to simulate seeing legitimate traffic. These `gettag` outputs do not count as a forgery [282].
*   **A PRF is a MAC (Claim 10.4):**
    *   **Construction:** If `F` is a secure PRF, then `MAC(k,m) = F(k,m)` is a secure MAC for message space `{0,1}^in` [283].
    *   **Output Length:** This holds if the PRF's output length `out = λ` is sufficiently long (e.g., `λ` bits) to make blind guessing of tags negligible [284].
    *   **Distinction:** Not every PRF is a MAC (if output is too short). Not every MAC is a PRF (a MAC might not have pseudorandom looking tags if patterns exist, but it's still hard to forge). It's crucial to understand whether `pseudorandomness` or just `hardness to guess/forge` is required [285].
*   **MACs for Long Messages:** Similar to block ciphers, PRFs (as MACs) are typically for fixed-length inputs. Techniques are needed for arbitrary-length messages.
    *   **Insecure Approaches:** Simple concatenation (`MAC(k, m1‖m2)`) or independent MACs for each block (`MAC(k,m1) ‖ MAC(k,m2)`) are insecure due to malleability or the ability to reorder/combine blocks [286, 287].
    *   **CBC-MAC (Construction 10.5):** A common secure approach [287].
        *   **Mechanism:** Uses a PRF `F` (or block cipher) iteratively, similar to CBC encryption, but **only the very last block is output as the tag** [288]. It typically uses a fixed `IV` (e.g., all zeroes) [288].
        *   **Security (Theorem 10.6):** CBC-MAC is a secure MAC for messages of **fixed length** `λl` (multiple of block length `λ`) if `F` is a secure PRF [288].
    *   **ECBC-MAC (Theorem 10.8):** An extension of CBC-MAC that makes it secure for **variable-length messages** (any length that is a multiple of the block length) [289]. This often involves using different keys for the final block depending on whether it was a full block or a padded one.
*   **Encrypt-Then-MAC (EtM - Construction 10.9):**
    *   **Motivation:** The core application of MACs is to transform a **CPA-secure encryption scheme into a CCA-secure one** [276, 277, 289].
    *   **Mechanism:**
        1.  **Encrypt the plaintext `m` using a CPA-secure encryption scheme `E`**: `c = E.Enc(k_e, m)` [290].
        2.  **Compute a MAC tag `t` on the *ciphertext `c`* (NOT the plaintext `m`) using a secure MAC scheme `M`**: `t = M.MAC(k_m, c)` [290].
        3.  The final ciphertext is `(c, t)` [290].
        4.  **Decryption:** First, verify the MAC tag: if `t != M.MAC(k_m, c)`, return error. Otherwise, decrypt `c` using `E.Dec(k_e, c)` [290].
    *   **Key Property:** Separate, independent keys (`k_e`, `k_m`) are used for encryption and MAC [290].
    *   **Security (Claim 10.10):** If `E` has CPA security and `M` is a secure MAC, then `EtM` has **CCA security** [291].
    *   **Proof Intuition:** The proof (which is complex with many hybrids) shows that an adversary's attempts to forge a ciphertext (and thus trigger a useful decryption) will fail because the MAC scheme will detect any manipulation (due to its security) [291-298]. This means the decryption oracle provided to the adversary in the CCA game will almost always return an error for adversary-chosen ciphertexts, thus providing no useful information for distinguishing [296].
    *   **Authenticated Encryption (AE):** EtM also inherently provides **Authenticated Encryption (AE) security** (which ensures that only legitimately generated ciphertexts decrypt successfully), making it the "gold standard" for encryption [299-301].

### 12. Digital Signatures

Digital signatures are cryptographic primitives that provide **authenticity and non-repudiation** [278, 302]. They are similar to MACs but are **asymmetric-key primitives**, using different keys for signing and verifying [278].

*   **Syntax:**
    *   `KeyGen`: Outputs a pair of keys `(sk, vk)`, where `sk` is the **signing key** (private) and `vk` is the **verification key** (public) [278].
    *   `Sign`: Takes `sk` and a message `m` as input, outputs a **signature `σ`** [302].
    *   `Ver`: Takes `vk`, `m`, and a potential `σ` as input, and outputs a boolean (true if valid, false otherwise) [302].
*   **Key Idea:** The verification key `vk` is made **public**, allowing anyone to verify a signature [302]. However, **only the holder of the secret signing key `sk` can generate valid signatures** [302]. This guarantee holds even if an attacker sees many valid signatures of chosen messages [302].
*   **Security Definition (Definition 13.6):**
    *   **Goal:** It should be hard for an adversary to find any new `(m, σ)` pairs that cause `Ver(vk, m, σ)` to output true (a "forgery") [302, 303]. This applies even if the adversary can request legitimate signatures on messages of their choice (`getsig` subroutine) [303, 304].
    *   **Formalization:** Compares `L_Σ_sig-real` (which generates and verifies real signatures) with `L_Σ_sig-fake` (which tracks `(m,σ)` pairs it generated via `getsig` and only accepts those as valid) [303, 304]. Indistinguishability implies forging is difficult.
    *   The `getvk()` subroutine is added to make the public key available to the adversary, reflecting its public nature [305].
*   **"Textbook" RSA Signatures (Construction 13.7):**
    *   **Keys:** `vk = (N, e)`, `sk = (N, d)` (generated as in RSA) [271].
    *   **Sign(`m`):** Computes `σ = m^d % N` [271].
    *   **Verify(`vk, m, σ`):** Checks `σ^e % N == m` [271].
    *   **INSECURE:** Textbook RSA signatures are **not secure** [271]. They are **malleable** due to the algebraic structure of RSA. An attacker can easily compute `(σ)^2` from a known valid signature `σ` for message `m`, and this `(σ)^2` will be a valid signature for `m^2` (since `(m^d)^2 = (m^2)^d`) [272]. This allows forging signatures on new messages that are related to previously signed messages.
*   **Hashed RSA Signatures (Construction 13.8):**
    *   **Solution:** To fix the malleability of textbook RSA signatures, a **cryptographic hash function `H`** is applied to the message *before* signing [272].
    *   **Sign(`m`):** Computes `σ = H(m)^d % N` [273].
    *   **Verify(`vk, m, σ`):** Checks `σ^e % N == H(m)` [273].
    *   **Security:** This construction is considered secure. The hash function **breaks the algebraic relationship** between the signature and the message, making it hard for an attacker to forge signatures on related messages [273]. For example, forging a signature on `m'` given a signature on `m` would require finding `m'` such that `H(m') = (H(m))^2`, which is hard if `H` is a good hash function [273].
    *   Its security is typically proven in the **"random oracle model"**, where the hash function `H` is idealized as a truly random function [273].

This comprehensive overview should provide a solid foundation for your viva exam, covering key definitions, mechanisms, security properties, and practical considerations for each topic. Remember to explain the *why* behind concepts and highlight the differences and relationships between them. Good luck!