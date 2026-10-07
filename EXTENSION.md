# Decentralised Trust and Blockchain Integration

## Purpose

This extension enhances the Integrity, Provenance, Trust and Data Quality Demonstrator by introducing a decentralised trust layer based on blockchain principles, decentralised identities, and verifiable credentials.

The objective is not to store operational asset data on a blockchain, but rather to demonstrate how blockchain technology can provide:

- immutable audit records
- independent verification of data integrity
- decentralised identity management
- cross-organisational trust
- tamper-evident provenance chains

This extension aligns with the principles demonstrated in Testbed-20: Integrity, Provenance, and Trust (IPT) Report, particularly around decentralised trust, verifiable credentials, provenance tracking, and cross-organisational verification.

## Architectural principles

The demonstrator shall implement the following principle:

Asset data remains in conventional databases whilst trust, provenance and verification artefacts are stored on a distributed ledger.

This allows:

- existing data models to remain unchanged
- legacy systems to participate
- verification to be performed independently of any single organisation
- provenance records to become tamper-evident

This follows a similar philosophy to the FACTS ecosystem demonstrated in Testbed-20: Integrity, Provenance, and Trust (IPT) Report.

## Capability 1: Decentralised asset owner identity

### Objective

Demonstrate how asset owners can be uniquely identified and verified without relying on a central trust authority.

### Example asset owners

- Water Utility
- Electricity Network Operator
- Telecommunications Provider

Each organisation receives:

- Organisation Identifier
- Public Key
- Decentralised Identifier (DID)

### Example

```text
did:demo:water-company
did:demo:electric-network
did:demo:telecom-provider
```

### Demonstration

Users can view:

- Dataset Owner
- Identity Status
- Credential Status

Example:

- Water Utility
  - ✓ Identity Verified
  - ✓ Credential Valid
  - ✓ Trusted Issuer

## Capability 2: Dataset integrity verification

### Objective

Demonstrate that consumers can independently verify whether a dataset has been modified since publication.

### Publishing process

When a dataset is submitted:

```text
Dataset
  ↓
Generate SHA256 Hash
  ↓
Write Hash to Ledger
```

Example record:

```json
{
  "datasetId": "water-assets-v1",
  "hash": "8ab4394d...",
  "published": "2026-01-12"
}
```

### Validation process

When data is requested:

```text
Current Dataset
      ↓
Recalculate Hash
      ↓
Compare To Ledger
```

Result:

```json
{
  "integrityVerified": true
}
```

## Capability 3: Provenance ledger

### Objective

Demonstrate immutable provenance across processing activities.

### Example data flow

```text
Water Dataset
Electric Dataset
Telecom Dataset
      ↓
Asset Consolidation Process
      ↓
Integrated Asset Dataset
```

Each activity is recorded on the ledger.

Example:

```json
{
  "transactionType": "transformation",
  "activity": "asset-consolidation",
  "inputs": [
    "water-v1",
    "electric-v1",
    "telecom-v1"
  ],
  "output": "integrated-assets-v1"
}
```

### User view

Users can inspect a complete chain of custody.

```text
Source Dataset
      ↓
Validation
      ↓
Transformation
      ↓
Consolidation
      ↓
API Publication
```

Each step becomes independently verifiable.

## Capability 4: Verifiable credentials

### Objective

Demonstrate machine-verifiable assertions about data quality and ownership.

### Credential examples

Asset owners issue credentials describing datasets.

Example:

```json
{
  "dataset": "Water Assets",
  "issuer": "Water Utility",
  "accuracy": "250mm",
  "completeness": 95
}
```

The credential is digitally signed.

### Ledger usage

The blockchain stores:

- Credential Identifier
- Issuer DID
- Issue Date
- Revocation Status

The complete credential remains off-chain.

### Demonstration

Users can verify:

- ✓ Dataset Owner Verified
- ✓ Credential Active
- ✓ Quality Claims Issued By Source Organisation

## Capability 5: Trust evidence service

### Objective

Generate trust ratings based on objective evidence.

The blockchain does not calculate trust directly. Instead it provides evidence used to assess trust.

### Evidence sources

- Identity
  - Verified DID
- Integrity
  - Dataset Hash Verified
- Provenance
  - Transformation Chain Verified
- Quality
  - Quality Metadata Available
- Freshness
  - Dataset Recently Published

### Example trust score

```json
{
  "trustScore": 92,
  "rating": "High",
  "evidence": [
    "verified-identity",
    "verified-integrity",
    "verified-provenance",
    "quality-metadata-present"
  ]
}
```

## API endpoints

### Verify identity

`GET /owners/{id}/identity`

Example response:

```json
{
  "verified": true,
  "did": "did:demo:water-company"
}
```

### Verify integrity

`GET /datasets/{id}/integrity`

Example response:

```json
{
  "verified": true,
  "ledgerHash": "8ab4394d..."
}
```

### View provenance

`GET /datasets/{id}/provenance`

Example response:

```json
{
  "events": [
    "published",
    "validated",
    "transformed",
    "consolidated"
  ]
}
```

### Verify credential

`GET /datasets/{id}/credential`

Example response:

```json
{
  "valid": true,
  "issuer": "Water Utility"
}
```

## Demonstration scenarios

### Scenario 1: Successful verification

An asset consumer requests data.

System response:

- ✓ Source Verified
- ✓ Integrity Verified
- ✓ Provenance Available
- ✓ Quality Metadata Available

Trust Rating: High

### Scenario 2: Data tampering detection

After publication a dataset is modified manually. The stored hash no longer matches.

System response:

- ✗ Integrity Verification Failed

API response:

```json
{
  "integrityVerified": false,
  "trustScore": 35
}
```

This demonstrates the value of immutable integrity records.

### Scenario 3: Credential revocation

A credential is revoked. A user attempts verification.

System response:

- ✗ Credential Revoked
- Trust Rating Reduced

This demonstrates lifecycle management of trust assertions.

## Suggested technology stack

The demonstrator may utilise:

- Asset Storage: PostgreSQL
- APIs: REST API, OpenAPI
- Provenance Model: W3C PROV
- Identity: Decentralised Identifiers (DIDs)
- Credentials: W3C Verifiable Credentials
- Ledger: Hyperledger Fabric, Ethereum Test Network, or a simple private blockchain

The implementation should remain lightweight and prioritise the demonstration of concepts over production-scale operation.

## Additional success criteria

The demonstrator shall prove that:

- asset owners can be independently verified
- datasets can be cryptographically validated
- provenance records survive transformations
- trust evidence can be independently verified
- data tampering can be detected
- trust can be established without relying on a single central authority
- trust artefacts can exist independently from the underlying asset data

## Expected outcome

The enhanced demonstrator will showcase not only how federated asset datasets can be shared, transformed and consumed, but also how consumers can independently verify the identity of data providers, the integrity of datasets, the provenance of transformations, and the trustworthiness of published information using decentralised trust technologies inspired by the concepts explored in Testbed-20: Integrity, Provenance, and Trust (IPT) Report.
