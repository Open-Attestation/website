---
id: main-properties
title: About the verification properties
sidebar_label: Overview

---

To gain a comprehensive understanding of how the verification process works, look into the various properties the OA framework provides for your documents:

- [Document integrity](/docs/verify-section/document-integrity): OpenAttestation ensures that the content of the document has not been modified since the document was created, with the exception of data removed using the built-in obfuscation mechanism.
- [Issuance status](/docs/verify-section/issuance-status): OpenAttestation checks that the document has been issued and its issuance status is in good standing (for instance, it hasn't been revoked). As of today, OpenAttestation supports two ways to issue documents: DID signing and Ethereum smart contracts.
- [Issuance identity](/docs/verify-section/issuance-identity): OpenAttestation checks and returns the identity of the issuer. By default, OpenAttestation uses DNS to verify the identity, but you have the option to use a temporary DNS record. It's important to note that OpenAttestation does not endorse any issuers. It only verifies that the issuing party in the document has provided some sort of proof that it is the same party as claimed - for example, proving ownership over a domain by creating a DNS record.

>**Important:** Although the verification process can be split into separate steps, they are all complementary. For example, proving the authenticity of a document and the validity of its issuer is meaningless if the solution cannot verify that the document has not been tampered with. This concept works for any combination of verification steps.