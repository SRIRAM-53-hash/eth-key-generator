## eth key generator 
This script demonstrates how to generate an Ethereum private key, public key, and address using the ecdsa and pycryptodome libraries. It uses the SECP256k1 curve for elliptic curve cryptography and Keccak-256 for hashing.

## Requirements
Ensure you have the following Python packages installed:
ecdsa
pycryptodome
## You can install these packages using pip:

pip install ecdsa pycryptodome

## Script Overview
The script performs the following steps:

1.Generates a random private key.
2.Derives the corresponding public key.
3.Hashes the public key using Keccak-256 to generate the Ethereum address.
## Code

import codecs
import ecdsa                    # Install ecdsa
from Crypto.Hash import keccak  # Install pycryptodome
import os

# Generate a random private key (32 bytes)
private_key_bytes = os.urandom(32)

# Generate the public key using the SECP256k1 curve
key = ecdsa.SigningKey.from_string(private_key_bytes, curve=ecdsa.SECP256k1).verifying_key

# Convert keys to byte strings
key_bytes = key.to_string()
private_key = codecs.encode(private_key_bytes, 'hex')
public_key = codecs.encode(key_bytes, 'hex')

# Print the private and public keys
print("Private key: ", private_key)
print("Public key: ", public_key)

# Decode the public key from hex to bytes
public_key_bytes = codecs.decode(public_key, 'hex')

# Create a Keccak-256 hash object and update it with the public key bytes
hash = keccak.new(digest_bits=256)
hash.update(public_key_bytes)
keccak_digest = hash.hexdigest()

# Take the last 20 bytes of the Keccak-256 hash to form the Ethereum address
address = '0x' + keccak_digest[-40:]
print("Address:", address)
## Detailed Steps
1.Import Libraries:

import codecs
import ecdsa
from Crypto.Hash import keccak
import os
2.Generate Private Key:

private_key_bytes = os.urandom(32)

This generates a random 32-byte private key.

3.Derive Public Key:

key = ecdsa.SigningKey.from_string(private_key_bytes, curve=ecdsa.SECP256k1).verifying_key
key_bytes = key.to_string()
This derives the public key using the SECP256k1 elliptic curve.

4.Encode Keys in Hex:

private_key = codecs.encode(private_key_bytes, 'hex')
public_key = codecs.encode(key_bytes, 'hex')
This converts the keys to hexadecimal strings.

5.Print Keys:

print("Private key: ", private_key)
print("Public key: ", public_key)
6.Decode Public Key:

public_key_bytes = codecs.decode(public_key, 'hex')
7.Generate Keccak-256 Hash:

hash = keccak.new(digest_bits=256)
hash.update(public_key_bytes)
keccak_digest = hash.hexdigest()
8.Form Ethereum Address:

address = '0x' + keccak_digest[-40:]
print("Address:", address)
The Ethereum address is derived by taking the last 20 bytes of the Keccak-256 hash of the public key.

## Output
The script outputs the private key, public key, and Ethereum address:

Private key:  <private_key>
Public key:  <public_key>
Address: 0x<ethereum_address>

##Notes
Keep your private key secure. Exposing it can result in loss of funds.
The generated address can be used to receive Ethereum and tokens on the Ethereum blockchain.
