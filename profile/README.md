# OpenSig

OpenSig is an open e-sign and digital notarisation standard for privately signing and verifying files of any type and size.

It gives a file verifiable proof of existence, intent, and possession, anchored to a permanent public record (any EVM-based blockchain).

---

## What is OpenSig?

OpenSig is a **file-native signature and notarisation protocol**.

* Sign or notarise any file (PDFs, images, code, videos, zips, datasets…) locally on device
* Prove when it existed
* Prove who signed it
* Include optional intent or metadata
* Verify independently - no vendor lock-in

Files never leave your device. Only a derived, encrypted proof is published.

---

## Core Principles

* **Privacy-first**
  
  Files are never uploaded. Proofs are meaningless without the original file. File hash is never exposed.

* **Independent verification**

  Anyone can verify a signature without trusting OpenSig.

* **Open standard**

  Fully open and free to build on.

* **File-native**

  Works with *any* file type, not just PDFs.

* **Immutable proofs**

  Once published, signatures cannot be altered or repudiated.

* **Digital identity ready**

  DID compatible with the `did:os:...` method.

---

## How it Works

1. A file is hashed (sha256) locally on the user’s device
2. A deterministic chain of signature hashes is generated
3. The next free signature (with optional data) is published to a public blockchain (any EVM-based chain supported) directly with the user's digital identity (OpenSig DID or ppk pair), encrypted with the file hash.
4. Anyone with the original file can:

   * discover signatures
   * verify integrity
   * read associated data

   Without the original file:

   * signatures cannot be linked to the original file
   * signatures cannot be linked to each other
   * intent cannot be decrypted

See the [protocol spec](https://github.com/OpenSig/opensig-protocol/blob/main/standard/opensig-standard.md) for details.

---

## What You Can Build

OpenSig is a primitive.

You can build:

* Digital signing workflows
* Proof-of-authorship systems
* IP protection tools
* Approval / handoff systems
* Audit trails and compliance layers
* Verifiable messaging or publishing systems

---

## Repositories

### Protocol & Standard

* **[opensig-protocol](https://github.com/OpenSig/opensig-protocol)**
  The core OpenSig protocol:

  * OpenSig Standard
  * `did:os` decentralised identity spec
  * OpenSig Registry smart contracts

### Reference Implementation

* **[opensig-ts](https://github.com/OpenSig/opensig-ts)**
  TypeScript implementation of the OpenSig standard

  * Sign and verify files
  * Generate and discover signature chains
  * Encode/decode signature data

### Legacy BTC Protocol

No longer supported. Simple Bitcoin-based e-sign and notarisation. See https://opensig.net/opensig-btc-whitepaper.pdf.

* **[opensig-btc](https://github.com/OpenSig/opensig-btc)**
  Command line client

* **[opensig-btc-lib](https://github.com/OpenSig/opensig-btc-lib)**
  Bitcoin e-sign library

---

## Key Concepts

### File Privacy

- Hashing happens locally on device. 
- The original file and its raw hash are never published.
- Only derived, non-reversible signature data is published on-chain.

### Signature Chain

Each file produces a deterministic sequence of signatures:

```
Sig₀ = H(H_c)
Sigₙ = H(H_c || Sigₙ₋₁)

where:

H = sha256
H_c = H(chainId || H_d)
H_d = H(file)
```

This ensures:

* uniqueness per file
* sequence of signatures
* signatures cannot be linked (without original file)
* network replay protection

### Encrypted Metadata

Optional signature data (e.g. message, purpose, URL, app-layer metadata):

* can be encrypted using the file hash
* readable only by those with the file

---

## Status

* Open standard
* Working reference implementation
* `did:os:...` registered DID method
* Registry contracts deployed on multiple networks
* Mobile app in active development (closed source)

---

## Contributing

OpenSig is an open standard and welcomes contributions.

Ways to contribute:

* protocol feedback
* SDKs in other languages
* integrations (creative tools, cloud storage, etc.)
* developer tooling and examples

---

## License

MIT License

---

## Learn More

* Website: [https://opensig.net](https://opensig.net)
* Docs: [OpenSig standard](https://github.com/OpenSig/opensig-protocol/blob/main/standard/opensig-standard.md)

---

## Vision

OpenSig is the foundation for a broader shift:

From:

* platform-dependent trust

To:

* **self-sovereign trust through digital identity**
