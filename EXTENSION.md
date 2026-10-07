Brief: Decentralised Trust and Blockchain Integration
Purpose

This extension enhances the Integrity, Provenance, Trust and Data Quality Demonstrator by introducing a decentralised trust layer based on blockchain principles, decentralised identities, and verifiable credentials.

The objective is not to store operational asset data on a blockchain, but rather to demonstrate how blockchain technology can provide:

Immutable audit records
Independent verification of data integrity
Decentralised identity management
Cross-organisational trust
Tamper-evident provenance chains

This extension aligns with the principles demonstrated in Testbed-20: Integrity, Provenance, and Trust (IPT) Report, particularly around decentralised trust, verifiable credentials, provenance tracking, and cross-organisational verification.

Architectural Principles

The demonstrator shall implement the following principle:

Asset data remains in conventional databases whilst trust, provenance and verification artefacts are stored on a distributed ledger.

This allows:

Existing data models to remain unchanged.
Legacy systems to participate.
Verification to be performed independently of any single organisation.
Provenance records to become tamper-evident.

This follows a similar philosophy to the FACTS ecosystem demonstrated in Testbed-20: Integrity, Provenance, and Trust (IPT) Report.

New Capability 1: Decentralised Asset Owner Identity
Objective

Demonstrate how asset owners can be uniquely identified and verified without relying on a central trust authority.

Example Asset Owners
Water Utility
Electricity Network Operator
Telecommunications Provider


Each organisation receives:

Organisation Identifier
Public Key
Decentralised Identifier (DID)


Example:

did:demo:water-company
did:demo:electric-network
did:demo:telecom-provider

Demonstration

Users can view:

Dataset Owner
Identity Status
Credential Status


Example:

Water Utility

✓ Identity Verified
✓ Credential Valid
✓ Trusted Issuer

New Capability 2: Dataset Integrity Verification
Objective

Demonstrate that consumers can independently verify whether a dataset has been modified since publication.

Publishing Process

When a dataset is submitted:

Dataset
    ↓
Generate SHA256 Hash
    ↓
Write Hash to Ledger


Example record:

{
  "datasetId": "water-assets-v1",
  "hash": "8ab4394d...",
  "published": "2026-01-12"
}

Validation Process

When data is requested:

Current Dataset
       ↓
Recalculate Hash
       ↓
Compare To Ledger


Result:

{
  "integrityVerified": true
}

New Capability 3: Provenance Ledger
Objective

Demonstrate immutable provenance across processing activities.

Example Data Flow
Water Dataset
Electric Dataset
Telecom Dataset

        ↓

Asset Consolidation Process

        ↓

Integrated Asset Dataset


Each activity is recorded on the ledger.

Example:

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

User View

Users can inspect a complete chain of custody.

Source Dataset
        ↓
Validation
        ↓
Transformation
        ↓
Consolidation
        ↓
API Publication


Each step becomes independently verifiable.

New Capability 4: Verifiable Credentials
Objective

Demonstrate machine-verifiable assertions about data quality and ownership.

Credential Examples

Asset owners issue credentials describing datasets.

Example:

{
  "dataset": "Water Assets",
  "issuer": "Water Utility",
  "accuracy": "250mm",
  "completeness": 95
}


The credential is digitally signed.

Ledger Usage

The blockchain stores:

Credential Identifier
Issuer DID
Issue Date
Revocation Status


The complete credential remains off-chain.

Demonstration

Users can verify:

✓ Dataset Owner Verified

✓ Credential Active

✓ Quality Claims Issued By Source Organisation

New Capability 5: Trust Evidence Service
Objective

Generate trust ratings based on objective evidence.

The blockchain does not calculate trust directly.

Instead it provides evidence used to assess trust.

Evidence Sources
Identity
Verified DID

Integrity
Dataset Hash Verified

Provenance
Transformation Chain Verified

Quality
Quality Metadata Available

Freshness
Dataset Recently Published

Example Trust Score
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

New API Endpoints
Verify Identity
GET /owners/{id}/identity


Example response:

{
  "verified": true,
  "did": "did:demo:water-company"
}

Verify Integrity
GET /datasets/{id}/integrity


Example response:

{
  "verified": true,
  "ledgerHash": "8ab4394d..."
}

View Provenance
GET /datasets/{id}/provenance


Example response:

{
  "events": [
    "published",
    "validated",
    "transformed",
    "consolidated"
  ]
}

Verify Credential
GET /datasets/{id}/credential


Example response:

{
  "valid": true,
  "issuer": "Water Utility"
}

Demonstration Scenarios
Scenario 1: Successful Verification

An asset consumer requests data.

System response:

✓ Source Verified
✓ Integrity Verified
✓ Provenance Available
✓ Quality Metadata Available

Trust Rating: High

Scenario 2: Data Tampering Detection

After publication a dataset is modified manually.

The stored hash no longer matches.

System response:

✗ Integrity Verification Failed


API response:

{
  "integrityVerified": false,
  "trustScore": 35
}


This demonstrates the value of immutable integrity records.

Scenario 3: Credential Revocation

A credential is revoked.

User attempts verification.

System response:

✗ Credential Revoked

Trust Rating Reduced


This demonstrates lifecycle management of trust assertions.

Suggested Technology Stack

The demonstrator may utilise:

Asset Storage
PostgreSQL

APIs
REST API
OpenAPI

Provenance Model
W3C PROV

Identity
Decentralised Identifiers (DIDs)

Credentials
W3C Verifiable Credentials

Ledger
Hyperledger Fabric
or
Ethereum Test Network
or
Simple Private Blockchain


The implementation should remain lightweight and prioritise the demonstration of concepts over production-scale operation.

Additional Success Criteria

The demonstrator shall prove that:

Asset owners can be independently verified.
Datasets can be cryptographically validated.
Provenance records survive transformations.
Trust evidence can be independently verified.
Data tampering can be detected.
Trust can be established without relying on a single central authority.
Trust artefacts can exist independently from the underlying asset data.
Expected Outcome

The enhanced demonstrator will showcase not only how federated asset datasets can be shared, transformed and consumed, but also how consumers can independently verify the identity of data providers, the integrity of datasets, the provenance of transformations, and the trustworthiness of published information using decentralised trust technologies inspired by the concepts explored in Testbed-20: Integrity, Provenance, and Trust (IPT) Report.
