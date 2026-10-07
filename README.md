Demonstrator Brief: Integrity, Provenance, Trust and Data Quality for Federated Asset Data
Purpose

Create a lightweight demonstrator that showcases how Integrity, Provenance, Trust (IPT) and Data Quality (DQ) concepts can be applied to a federated asset data ecosystem.

The demonstrator should illustrate how multiple data owners can publish data, how data can be transformed and combined, and how consumers can access both the resulting data and evidence regarding:

Who supplied it
When it was supplied
How it was transformed
Whether it has been altered
The quality of the source data
Whether it can be trusted for a given purpose

The demonstrator should be technology-agnostic and focus on concepts rather than production-grade implementation.

Demonstration Scenario

Three independent asset owners publish datasets.

Asset Owner A - Water Utility

Dataset:

Water Mains


Example attributes:

Asset ID
Pipe Material
Diameter
Installation Date
Geometry


Quality Metadata:

Positional Accuracy: ±250mm
Completeness: 95%
Last Surveyed: 2024

Asset Owner B - Electricity Network

Dataset:

High Voltage Cables


Example attributes:

Asset ID
Voltage
Installation Date
Geometry


Quality Metadata:

Positional Accuracy: ±500mm
Completeness: 90%
Last Surveyed: 2021

Asset Owner C - Telecommunications Provider

Dataset:

Fibre Ducts


Example attributes:

Asset ID
Duct Type
Capacity
Geometry


Quality Metadata:

Positional Accuracy: ±100mm
Completeness: 98%
Last Surveyed: 2025

Demonstrated Concepts
1. Identity

Every asset owner receives a unique digital identity.

Example:

water-company-01
power-network-01
telecom-provider-01


The demonstrator must show that published datasets can be linked back to a verified source.

2. Provenance

Every dataset carries provenance information.

Example:

{
  "owner": "water-company-01",
  "created": "2026-01-12",
  "version": "1.0"
}


The demonstrator should preserve provenance through all subsequent processing.

3. Integrity

When datasets are submitted:

Generate a hash
Store the hash alongside metadata

Example:

{
  "sha256": "abc123..."
}


Users should be able to verify that a dataset has not changed since publication.

4. Data Quality

A standard quality model should accompany every dataset.

Example:

{
  "accuracy": "250mm",
  "completeness": 95,
  "confidence": "high"
}


Quality information must remain accessible after transformation.

Transformation Service

Implement a simple processing service:

Asset Consolidation Service


Inputs:

Water assets
Electricity assets
Telecom assets

Processing:

Convert all datasets into a common model
Standardise attribute names
Merge into a single dataset

Example:

water-main        -> underground-asset
hv-cable          -> underground-asset
fibre-duct        -> underground-asset


Output:

Integrated Asset Dataset

Provenance Recording

The processing service should automatically generate lineage metadata.

Example:

{
  "activity": "asset-consolidation",
  "inputs": [
    "water-dataset-v1",
    "electricity-dataset-v1",
    "telecom-dataset-v1"
  ],
  "output": "integrated-assets-v1"
}


The user should be able to inspect the lineage chain from source dataset to final dataset.

Trust Scoring

Generate a simple trust score using:

Source Verification
+
Integrity Check
+
Data Quality
+
Data Freshness


Example output:

{
  "trustScore": 87,
  "rating": "High"
}


This score is illustrative only and intended to demonstrate how trust information may be surfaced to consumers.

Public API

Expose a small REST API.

Asset Endpoint
GET /assets


Returns consolidated assets.

Provenance Endpoint
GET /assets/{id}/provenance


Returns:

{
  "owner": "water-company-01",
  "suppliedDate": "2026-01-12",
  "transformation": [
    "standardisation",
    "consolidation"
  ]
}

Quality Endpoint
GET /assets/{id}/quality


Returns quality metadata.

Integrity Endpoint
GET /assets/{id}/integrity


Returns:

{
  "verified": true,
  "hash": "abc123..."
}

Trust Endpoint
GET /assets/{id}/trust


Returns:

{
  "score": 87,
  "rating": "High"
}

Suggested User Interface

A simple web application showing:

Asset Catalogue
Asset Owner
Dataset
Asset Count
Trust Score
Asset Detail
Source organisation
Quality metrics
Integrity status
Provenance chain
Processing View

Visual flow:

Water Assets
        \
Electric Assets -----> Consolidation Service -----> Integrated Dataset
        /
Telecom Assets

Trust Dashboard

For each dataset:

✓ Identity Verified
✓ Integrity Verified
✓ Provenance Available
✓ Quality Metadata Present

Trust Rating: High

Success Criteria

The demonstrator successfully proves that:

Multiple independent asset owners can publish data.
Data ownership can be verified.
Integrity checks detect tampering.
Provenance survives transformation.
Data quality metadata can be standardised and exposed.
Trust indicators can be calculated and presented to users.
Consumers can access data and trust evidence through APIs.
Expected Outcome

The demonstrator should provide a tangible example of how an asset data platform could evolve from simply publishing datasets to delivering verifiable, traceable, quality-assured and trustworthy data products, bringing together the concepts from OGC IPT and Data Quality initiatives in a form that is easy for stakeholders to understand and evaluate.
