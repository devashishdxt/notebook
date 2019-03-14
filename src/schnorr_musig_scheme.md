# Schnorr Multi-Signature Scheme

## Initial process

1. Each signer has a public and private keypair using [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm). Private key, \\( k_i\\) and public key, \\( P_i\\), such that,
\\[ P_i = k_iG\\]
where \\( G\\) is elliptic curve base point.
2. Each signer generates a nonce keypair using ECDSA. Private nonce, \\( r_i\\) and public nonce, \\( R_i\\), such that 
\\[ R_i = r_iG\\]

## Nonce commitment sharing

1. Each signer shares \\( H(R_i)\\) with all other participants. Here, \\( H\\) is a 256-bit hash function.
2. Upon receipt of \\( H(R_i)\\) from every other signer, each signer communicates \\( R_i\\) to all participants.
3. The recipient verifies that each \\( R_i\\) is consistent with previously communicated hash, \\( H(R_i)\\).

## Signature creation

1. Each signer calculates the combined public key, \\( P\\), as follows:
\\[ \ell = H( P_1 || P_2 || \cdots || P_n )\\]
\\[ \mu_i = H( \ell || P_i )\\]
where, \\( \mu_i\\) is MuSig coefficient.
\\[ P = \sum_{i = 0}^n \mu_i P_i\\]
2. Each signer calculates combined nonce, \\( R\\), and a challenge, \\( e\\), as follows:
\\[ R = \sum_{i = 0}^n R_i\\]
\\[ e = H( R || P || m )\\]
where, \\( m\\) is the message to be signed.
3. Each signer computes their partial signature, \\( s_i\\), as follows:
\\[ s_i = r_i + k_i \mu_i e\\]
4. Complete signature is then \\( (s, R)\\) where \\( s\\) is,
\\[ s = \sum_{i = 0}^n s_i\\]

## Signature verification

Recipient can calculate \\( e\\), since they already know \\( m\\), \\( R\\) and \\( P\\).

Let's start from signature \\( s\\),
\\[ s = \sum_{i = 0}^n s_i\\]
By substitution,
\\[ s = \sum_{i = 0}^n ( r_i + k_i \mu_i e)\\]
Multiply both sides by \\( G\\) (elliptic curve base point),
\\[ sG = \sum_{i = 0}^n ( r_i + k_i \mu_i e)G\\]
\\[ sG = \sum_{i = 0}^n r_i G + \sum_{i = 0}^n \mu_i (k_i G) e\\]
By substitution,
\\[ sG = \sum_{i = 0}^n R_i + \sum_{i = 0}^n \mu_i P_i e\\]
\\[ sG = R + Pe\\]
Recipient can verify this equation to verify the signature \\( (s, R)\\).
