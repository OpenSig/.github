# OpenSig

OpenSig is an open protocol for signing and notarising arbitrary digital data without revealing the data itself. It is designed for digital identity-based e-signature and notarisation solutions.

It provides a deterministic, verifiable mapping between:
- a file
- a signer
- a point in time

Anchored to a public execution layer (EVM-compatible chains).

---

## Overview

OpenSig defines a method for:

- generating signatures from a file locally
- publishing those signatures to a public registry
- deterministically discovering and verifying them given the original file

The protocol avoids:
- file upload
- centralised indexing
- dependence on a verifying authority

Only derived data is published.

---

## Properties

- **Local-first**  
  All hashing, signing, and encryption occurs client-side.

- **Non-disclosure**  
  The file and its raw hash are never published.

- **Unlinkability (without the file)**  
  Published signatures cannot be correlated to a file or to each other without possession of that file.

- **Deterministic discovery**  
  Signature ordering is derived from the file itself, not external indexing.

- **Chain-specific separation**  
  Signature sequences differ per chain, preventing replay.

- **Independent verification**  
  No reliance on a service provider for validation.

---

## Protocol Sketch

Given a file:

```
H_d = SHA256(file)
H_c = SHA256(chainId || H_d)

Sig₀ = SHA256(H_c)
Sigₙ = SHA256(H_c || Sigₙ₋₁)
```


Each signature is published once to a registry contract.

Verification proceeds by iterating the sequence and querying for existing entries.

---

## Data Model

A signature event contains:

- timestamp (block time)
- signer (address / DID)
- signature (bytes32)
- optional data payload (bytes)

Payload:
- supports arbitrary bytes, strings and object data (MessagePacked)
- optionally encrypted using `H_d` as key (AES-GCM)

Without `H_d`:
- payload cannot be decrypted
- signatures cannot be associated with a document

---

## Identity

OpenSig is compatible with:

- EVM keypairs
- `did:os` DID method

The DID method defines how identities resolve and how signatures bind to them. OpenSig DIDs are deterministically derived from the user's EVM address (EOA or smart account) and chain id.

---

## Repositories

### Protocol

- [`opensig-protocol`](https://github.com/OpenSig/opensig-protocol)  
  - standard specification  
  - `did:os` method  
  - registry contract code

### Reference Implementation

- [`opensig-ts`](https://github.com/OpenSig/opensig-ts)  
  - hashing and document model  
  - signature generation  
  - discovery and verification  
  - data encoding/decoding
  - encryption
  - DID resolution

### Legacy (Bitcoin)

Deprecated.

- [`opensig-btc`](https://github.com/OpenSig/opensig-btc)  
- [`opensig-btc-lib`](https://github.com/OpenSig/opensig-btc-lib)  

---

## Use

OpenSig is a primitive.

Possible applications include:

- digital identity systems
- document signing systems
- timestamping / proof-of-existence
- authorship and provenance tracking
- approval and audit logs
- verifiable publication systems

---

## Status

- standard: v0.1
- reference implementation available
- contracts deployed on multiple EVM chains
- `did:os` method defined and registered

---

## Contributing

Contributions are welcome:

- protocol review
- alternative implementations
- tooling and integrations

---

## License

MIT

---

## Notes

The OpenSig protocol does not attempt to define:
- UI/UX
- workflow semantics
- legal interpretation

These are expected to be implemented at higher layers. The OpenSig mobile app is such an implementation. See https://opensig.net