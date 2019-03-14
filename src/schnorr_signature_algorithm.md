# Schnorr Signature Algorithm

## Initial process

1. Create a public and private keypair using [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm). Private key, \\( k\\) and public key, \\( P\\) such that 
\\[ P = kG\\]
where \\( G\\) is elliptic curve base point.
2. Generate a nonce keypair using ECDSA. Private nonce, \\( r\\) and public nonce \\( R\\) such that 
\\[ R = rG\\]
3. Send message \\( (m)\\), public nonce \\( (R)\\) and public key \\( (P)\\) to recipient.

Note: Public and private keys can be reused, but a new nonce keypair should be generated for each signature.

## Signature creation

1. Create a challenge \\( e\\),
\\[ e = H( R || P || m )\\]
where \\( H\\) is a 256 bit hash function (SHA256)
2. Create signature \\( s\\),
\\[ s = r + ke\\]

## Signature verification

Recipient can calculate \\( e\\), since they already know \\( m\\), \\( R\\) and \\( P\\). But they don't know the private key \\( (k)\\) and private nonce \\( (r)\\).

Let's start from signature \\( s\\),
\\[ s = r + ke\\]
Multiply both sides by \\( G\\) (elliptic curve base point),
\\[ sG = (r + ke)G\\]
\\[ sG = rG + (kG)e\\]
By substitution,
\\[ sG = R + Pe\\]
Recipient can verify this equation to verify the signature \\( s\\).