# OpenSig

**Simply signatures. Private. Independently verifiable. For any file, any size.**

OpenSig is an open standard for digitally signing, proving, and verifying files — without ever uploading them.

It gives any file into **verifiable proof of existence, intent, and identity**, anchored to a permanent public record (any EVM-based blockchain).

---

## 🚀 What is OpenSig?

OpenSig is a **file-native signature and notarisation protocol**.

* Sign any file (PDFs, images, code, videos, datasets…)
* Prove *when it existed*
* Prove *who signed it*
* Verify independently — no vendor lock-in

> Files never leave your device. Only a derived proof is published.

---

## 🔑 Core Principles

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

---

## 🧠 How it Works (High Level)

1. A file is hashed (sha256) locally on the user’s device
2. A deterministic chain of signature hashes is generated
3. A signature (and optional data) is published to a public blockchain (any EVM-based chain supported) encrypted with the file hash.
4. Anyone with the original file can:

   * discover signatures
   * verify integrity
   * read associated data

Signatures form a **chain unique to each file and blockchain**, derived from its hash and the target blockchain id.

---

## 🧩 What You Can Build

OpenSig is a primitive.

You can build:

* Digital signing workflows
* Proof-of-authorship systems
* IP protection tools
* Approval / handoff systems
* Audit trails and compliance layers
* Verifiable messaging or publishing systems

---

## 📦 Repositories

### 🧾 Protocol & Standard

* **opensig-protocol**
  The core OpenSig protocol:

  * OpenSig Standard
  * `did:os` decentralised identity spec
  * OpenSig Registry smart contracts

### 🛠 Reference Implementation

* **opensig-ts**
  TypeScript implementation of the OpenSig standard

  * Sign and verify files
  * Generate and discover signature chains
  * Encode/decode signature data

### 🔱 Legacy BTC Protocol

No longer supported. Simple Bitcoin-based e-sign and notarisation. See https://opensig.net/opensig-btc-whitepaper.pdf.

* **opensig-btc**
  Command line client

* **opensig-btc-lib**
  Bitcoin e-sign library

---

## 🔐 Key Concepts

### File Privacy

The original file and its raw hash are never published.
Only derived, non-reversible signature data is stored.

### Signature Chain

Each file produces a deterministic sequence of signatures:

```
Sig₀ = H(H_c)
Sigₙ = H(H_c || Sigₙ₋₁)

where:

H = sha256
H_c = chain-specific hash
```

This ensures:

* uniqueness per file
* order of signatures
* signatures cannot be linked to each other or to the file without the original file
* resistance to replay across networks

### Encrypted Metadata

Optional signature data (e.g. message, purpose, URL):

* can be encrypted using the file hash
* readable only by those with the file

---

## 🧪 Status

* Open standard
* Working reference implementation
* `did:os:...` registered DID method
* Registry contracts deployed on multiple networks
* Mobile app in active development (closed source)

---

## 🤝 Contributing

OpenSig is an open standard and welcomes contributions.

Ways to contribute:

* protocol feedback
* SDKs in other languages
* integrations (creative tools, cloud storage, etc.)
* developer tooling and examples

---

## 📄 License

MIT License

---

## 🔗 Learn More

* Website: [https://opensig.net](https://opensig.net)
* Docs: [OpenSig standard](https://github.com/OpenSig/opensig-protocol/blob/main/standard/opensig-standard.md)

---

## 🧭 Vision

OpenSig is the foundation for a broader shift:

From:

* platform-dependent trust

To:

* **self-sovereign trust through digital identity**
