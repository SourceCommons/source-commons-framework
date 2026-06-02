# Governance

Source Commons Framework is maintained as a public standard for documenting sources, tools, evaluations, and reuse cases.

The governance model is based on public review, clear evidence, traceable changes, and shared responsibility.

## Principles

### Open Source and Community-Governed

The framework is maintained in the open. Maintainers coordinate versions, protect schema stability, and review changes. Contributors can suggest improvements through public issues and pull requests.

As the project grows, review, moderation, and curation roles should be documented and shared.

### Public by Default

Framework changes should happen through public pull requests whenever possible. A change should be visible, reviewable, and reversible.

### Non-Promotional

The framework is not a promotional directory.

Entries must not primarily promote brands, products, paid datasets, search visibility, or commercial positioning. An organization or product can be named when it helps explain provenance, access, tooling, or reuse.

Promotional or misleading entries can be rejected or removed.

### Open Focus, Not Open-Only

The framework naturally focuses on open sources, but useful data is not always free. Paid, fee-based, restricted, or licensed sources may be documented when their public value is clear.

Paid access, pricing, account requirements, access limits, and reuse restrictions must be documented clearly.

### Evidence-Based

Contributions should show what the source is, where it comes from, how it can be accessed, and when it was checked.

Evaluations must separate factual observations from interpretation. Claims about quality, access, legality, availability, or limitations should include dates, examples, checks, or source links.

### Source-Level Clarity

Every source should have a source level:

- `L1_meta_list`: a list or catalogue of sources.
- `L2_portal`: a portal, registry, or institutional access point.
- `L3_dataset`: a specific dataset with a stable access path.
- `L4_fragmented_source`: a useful source that requires extraction, reconciliation, or transformation.

Level 3 records should receive the most detailed structured metadata when available. Level 4 records should document extraction method, legal risk, evidence, and limits with extra care.

### Standards-Compatible

The framework should reuse existing standards before creating new fields. DCAT, DQV, Dublin Core Terms, Wikidata, GitHub metadata, and Hugging Face metadata are used where they fit. Source Commons fields are extensions for operational details that those standards do not cover directly.

### Curated External Integrations

External identifiers should make records easier to verify, reconcile, reproduce, or maintain.

Wikidata fields should use clear QIDs for primary entities, topics, and related entities. Advanced Wikidata relationships should rely on a curated property set and should not expose the full property universe to casual contributors.

GitHub fields should point to the most relevant repository, user, or organization for a source, tool, or use case. They should support provenance, implementation, issue tracking, maintenance, or reproducibility, not promotion.

Maintainers may reject external links that are ambiguous, unverifiable, promotional, stale, or only loosely related to the record.

### Quality Over Quantity

A small set of well-described records is more valuable than a large list of shallow links. Entries may be rejected if they are obsolete, duplicate, incomplete, promotional, unsupported, or too vague to reuse.

### Legal and Ethical Awareness

Public availability does not automatically mean unrestricted reuse.

Each source should document licence, terms, access rights, scraping limits, personal data concerns, redistribution risk, and recommended controls. Scraping should be a last resort when an API, export, bulk download, or official feed is unavailable.

### Reproducibility and Traceability

A record should explain how the source was accessed, when it was checked, what limits were observed, and what identifiers or join keys make reuse possible.

Use cases should document source relationships, join strategies, tools, outputs, confidence, and legal limits.

### Neutrality and Conflicts of Interest

The framework must remain neutral. Conflicts of interest should be disclosed when a contributor, maintainer, partner, vendor, or funder has a direct relationship with a source, tool, or use case.

A commercial relationship does not automatically disqualify a contribution, but it must not influence review, scoring, or visibility.

### Merit-Based Roles

Anyone can suggest a source, correction, tool, evaluation, or use case. Review roles should depend on contribution quality, subject-matter knowledge, reliability, and care for the framework.

No organization can buy maintainer authority.

### Inclusive and Respectful Collaboration

The framework should be usable by contributors with different backgrounds and skill levels. Debate is welcome when it improves clarity, evidence, or public value. Personal attacks, harassment, and bad-faith participation are not acceptable.

### Versioned and Stable

Schemas, criteria, vocabularies, and review rules should be versioned. Major changes should be discussed publicly before release. Older versions should remain accessible when possible.

### Public Value and Practical Reuse

The framework exists to make public-interest data easier to find, evaluate, connect, and reuse. A source matters when it supports real work. Use cases should document audience, impact, limits, and evidence.

## Review Expectations

Pull requests should be reviewed for:

- Schema validity.
- Evidence quality.
- Licence and access clarity.
- Duplicate or overlapping records.
- Standards alignment.
- Wikidata and GitHub identity accuracy when those fields are present.
- Legal and ethical risk.
- Practical usefulness.
- Neutral wording.

Maintainers may request changes, split large submissions, reject unsupported entries, or ask for additional evidence before merging.

## Future Process

The public contribution process will be documented before broad source submissions open. It should include issue templates, pull request templates, validation checks, versioning rules, and review roles.
