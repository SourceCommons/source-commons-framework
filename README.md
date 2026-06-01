# Source Commons Framework

Source Commons Framework is an open, versioned framework for documenting data sources, data tools, source evaluations, and practical reuse cases.

This repository is the home of the framework itself. It stores the canonical CSV schemas, the empty CSV files that future pull requests will update, and the written rules that explain how the standard is governed and maintained.

## Purpose

The framework helps teams describe sources in a way that is simple enough for CSV workflows and structured enough to connect with established metadata ecosystems.

It is designed for:

- Open data portals and public catalogues.
- Structured datasets with stable access paths.
- Fragmented sources such as reports, PDFs, web pages, filings, decisions, and archives.
- Tools used to discover, clean, extract, validate, publish, or evaluate data.
- Dated evaluations that separate evidence from opinion.
- Use cases that explain how sources can be reused responsibly.

## Repository Contents

- `data/sources.csv`: source records.
- `data/tools.csv`: tool records.
- `data/evaluations.csv`: evaluation records.
- `data/use-cases.csv`: reuse case records.
- `documentation.md`: field-level documentation for each CSV.
- `governance.md`: governance principles and review rules.

The CSV files are intentionally empty except for headers. Future pull requests can add proposed source records, tool records, evaluations, and use cases.

## Standards Alignment

Source Commons Framework uses existing standards where they fit:

- DCAT for dataset and catalogue metadata.
- DQV for data quality dimensions, metrics, and annotations.
- Dublin Core Terms for titles, descriptions, publishers, identifiers, licences, spatial coverage, and temporal coverage.
- Hugging Face Hub metadata for AI models, datasets, Spaces, discussions, and repository provenance.

Framework-specific fields extend these standards when practical reuse requires more detail, such as access cost, scraping position, join keys, legal risk, and workflow evidence.

## Contribution Model

This repository is the place where reviewed changes land. Future contributions should arrive through public pull requests that add or update CSV rows, improve documentation, or clarify governance.

Detailed contribution rules will be added before public source submissions open.
