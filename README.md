# Asymmetric RSA Key Pair Generator

![Python Version](https://img.shields.io/badge/python-3.6%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)

A **production‑ready**, pure‑Python implementation of RSA key generation, encryption, and decryption.  
Uses **only** built‑in modules (`math`, `random`, `time`, `sys`) – no external cryptographic libraries.  
Designed for educational clarity and demonstrable mathematical transparency.

---

## Technical Overview

This script implements the full RSA asymmetric cryptosystem from first principles:

- Generates two **distinct prime numbers** (`p`, `q`) using a **Miller–Rabin primality test**.
- Computes the **RSA modulus** `n = p·q` and **Euler’s totient** `φ(n) = (p‑1)·(q‑1)`.
- Selects the **standard public exponent** `e = 65537` (coprime to `φ(n)`).
- Derives the **private exponent** `d` as the modular multiplicative inverse of `e` modulo `φ(n)` using the **Extended Euclidean Algorithm**.
- Accepts a user‑supplied text message, encrypts it via **modular exponentiation** (`c = m^e mod n`), and decrypts it back (`m = c^d mod n`).
- Displays all intermediate values (primes, keys, ciphertext in hex, recovered plaintext) in clean ASCII boxes.

The implementation is **fully self‑contained** and runs on any Python 3 interpreter without additional dependencies.

---

## Number Theory & Prime Factorization Mechanics

The security of RSA rests on the practical difficulty of factoring the modulus `n`.

| Component | Formula / Derivation | Mathematical Role |
|-----------|----------------------|-------------------|
| **Prime generation** | Random odd number → Miller‑Rabin primality test (k=8 rounds) | Provides the two large primes `p` and `q`. |
| **RSA modulus** | `n = p × q` | The public/private key modulus. Its bit length defines the key size. |
| **Euler’s totient** | `φ(n) = (p‑1) × (q‑1)` | Number of integers `< n` coprime to `n`. Critical for key pair validity. |
| **Public exponent** | `e = 65537` (commonly used) | Must satisfy `gcd(e, φ(n)) = 1`. |
| **Private exponent** | `d = e⁻¹ mod φ(n)` | Computed via modular inverse. The decryption exponent. |
| **Encryption** | `c = m^e mod n` | Modular exponentiation – one‑way without the private key. |
| **Decryption** | `m = c^d mod n` | Inverses encryption by Euler’s theorem. |

---

## Extended Euclidean Algorithm (EEA)

The script implements a **recursive extended Euclidean algorithm** to compute the modular inverse:
