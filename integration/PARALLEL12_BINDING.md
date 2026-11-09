# Parallel-12 ML-DSA Native Binding Boundary

This repository provides the C90 ML-DSA implementation and public API in
`mldsa/mldsa_native.h`. The integration branch intentionally does not add a
second cryptographic implementation or guess a compiler configuration.

## Required binding contract

- Consume the configured public API from the exact pinned mldsa-native commit.
- Select and record the parameter set explicitly (ML-DSA-44, ML-DSA-65, or ML-DSA-87).
- Check every return value; the API marks return values as must-check.
- Enforce buffer lengths from the configured parameter set.
- Never overlap input and output buffers.
- Validate imported secret keys with the documented key-validation API before signing.
- Keep signing keys in the device key boundary; never serialize them into task envelopes or SCAR.
- Bind signatures to canonical task/evidence digests and signer identity.
- Treat signature verification failure, RNG failure, build mismatch, or missing symbols as DENY.

## Status

The native library is not yet linked into the Swift or Python application targets.
No signing or verification operation is claimed by this integration document.
Native build, vector tests, ABI review, and cross-language interoperability remain
required acceptance gates.
