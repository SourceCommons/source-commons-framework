# Documentation

This document defines the Source Commons Framework CSV files, required fields, allowed values, formats, and examples.

The framework uses CSV because it is easy to review in pull requests, easy to validate, and compatible with many data tools. Multiple values in one cell must be separated with a semicolon and a space: `value one; value two`.

## Field Prefixes

| Prefix | Source | Meaning |
| --- | --- | --- |
| `dct_` | [Dublin Core Terms](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/) | General resource metadata such as title, description, publisher, identifier, license, location, and time. |
| `dcat_` | [DCAT 3](https://www.w3.org/TR/vocab-dcat-3/) | Catalogue, dataset, distribution, data service, access, and download metadata. |
| `dqv_` | [Data Quality Vocabulary](https://www.w3.org/TR/vocab-dqv/) | Quality dimensions, metrics, measurements, methods, and annotations. |
| `wikidata_` | [Wikidata](https://www.wikidata.org/) | Entity identifiers, topics, related entities, and curated entity-property relationships. |
| `github_` | [GitHub REST API](https://docs.github.com/en/rest) | Repository, user, organization, source code, maintainer, and reproducibility metadata. |
| `hf_` | [Hugging Face Hub API](https://huggingface.co/docs/hub/api) | Hub repository, model, dataset, Space, discussion, license, task, and provenance metadata. |
| `sc_` | Source Commons | Framework extension terms used when existing standards do not cover operational reuse details. |

## CSV Files

| File | Purpose |
| --- | --- |
| `data/sources.csv` | Documents source records, access paths, legal context, join keys, DCAT mapping, Wikidata entities, GitHub links, and Hugging Face links when relevant. |
| `data/tools.csv` | Documents tools used to discover, extract, clean, validate, publish, or evaluate sources, including Wikidata, GitHub, and Hugging Face links when relevant. |
| `data/evaluations.csv` | Stores dated evaluations of source quality, access, legal risk, and recommended actions. |
| `data/use-cases.csv` | Documents practical reuse workflows that connect sources, tools, outputs, audiences, limits, topic identities, and reproducible GitHub references. |
| `data/skills.csv` | Indexes reusable Source Commons skills and links each CSV row to its canonical Markdown file. |
| `skills/*.md` | Stores skill documentation with generated YAML frontmatter followed by human-readable Markdown content. |

## General Formats

| Format | Rule | Example |
| --- | --- | --- |
| Identifier | Stable ASCII identifier with an uppercase prefix. | `SRC-CA-TORONTO-BUILDING-PERMITS` |
| URL | Absolute URL beginning with `https://` when available. | `https://open.toronto.ca/dataset/building-permits-active-permits/` |
| Wikidata item | A Wikidata QID. Store the QID as the stable value; a label may be included for review in list fields. | `Q142` or `Employment (Q12737077)` |
| Wikidata property | A Wikidata PID used only for curated advanced relationships. | `P137` |
| Wikidata advanced relation | Compact JSON object with a Wikidata property and item value. Multiple objects may be separated with `; `. | `{"property":"P137","value":"Q95"}` |
| GitHub resource id | Repository full name for repositories, or login for users and organizations. | `openrefine/openrefine` or `github` |
| Date | ISO 8601 calendar date. | `2026-05-30` |
| Date time | ISO 8601 date time with timezone when known. | `2026-05-30T14:32:00Z` |
| Temporal coverage | ISO 8601 date, year, date interval, or clear text when the source only publishes a human label. | `2020-01-01/2025-12-31` |
| Country | Prefer ISO 3166-1 alpha-2 for country codes; plain country names are allowed when the source uses them. | `CA` |
| Region | Prefer ISO 3166-2 for subdivisions when available; otherwise use the official source label. | `CA-ON` |
| Boolean | Lowercase `true` or `false`; use `Unknown` when the answer was not checked. | `false` |
| Multiple values | Separate values with `; `. | `CSV; JSON; API` |
| Related record list | Separate Source Commons record ids with `; `. | `SRC-CA-TORONTO-BUILDING-PERMITS; TOOL-FRICTIONLESS` |
| Empty value | Leave blank only when not applicable or not yet known. Use `N/A`, `Unknown`, or `Not checked` when that distinction matters. | `Not checked` |

## Inter-record Links

Every CSV can link to existing Source Commons items without a fixed limit. Use these optional fields when a relationship is useful but is not already represented by a more specific field such as `source_ids`, `tools_used`, `datasets`, `use_cases`, `related_skills`, or `crosswalk_source_ids`.

| Field | Links to | Cardinality | Notes |
| --- | --- | --- | --- |
| `related_source_ids` | `data/sources.csv` | Multiple | Related datasets, portals, crosswalk candidates, or upstream/downstream sources. |
| `related_tool_ids` | `data/tools.csv` | Multiple | Tools that support, evaluate, transform, inspect, or publish the record. |
| `related_use_case_ids` | `data/use-cases.csv` | Multiple | Reuse cases demonstrated, supported, or affected by the record. |
| `related_skill_ids` | `data/skills.csv` | Multiple | Skills that explain, reuse, or complement the record. |
| `related_evaluation_ids` | `data/evaluations.csv` | Multiple | Evaluations that qualify, review, or contextualize the record. |

Relationship fields are identifiers, not public contributor names. The website may also mirror these fields into a relational database so the catalogue can show connected records without reading every CSV cell.

## Controlled Values

These values are Source Commons controlled values unless a field notes an external standard.

| Field group | Allowed values |
| --- | --- |
| Source level | `L1_portal`, `L2_dataset`, `L3_fragmented_source` |
| Risk level | `Low`, `Medium`, `High`, `Unknown` |
| Confidence | `Low`, `Medium`, `High`, `Unknown` |
| Metadata status | `Available`, `Partial`, `Not found`, `Not checked`, `N/A` |
| Required boolean | `true`, `false`, `Unknown` |
| Access rights | `Public`, `Open`, `Restricted`, `Gated`, `Private`, `Unknown` |
| Account required | `true`, `false`, `Unknown` |
| Authentication method | `None`, `API key`, `OAuth`, `Token`, `User agent`, `Login`, `IP allowlist`, `Unknown` |
| Rate limit scope | `IP`, `Account`, `Token`, `Endpoint`, `Organization`, `None`, `Unknown` |
| Rate limit period | `second`, `minute`, `hour`, `day`, `month`, `year`, `Unknown` |
| Access cost type | `Free`, `Paid`, `Freemium`, `Restricted`, `Unknown` |
| Pricing model | `free_open_access`, `free_with_fair_use`, `subscription`, `per_request`, `per_seat`, `bulk_license`, `institutional_license`, `custom_quote`, `unknown` |
| Structuredness | `Structured`, `Semi-structured`, `Unstructured`, `Mixed`, `Unknown` |
| Fragmentation level | `Low`, `Medium`, `High`, `Unknown` |
| Extraction difficulty | `Low`, `Medium`, `High`, `Unknown` |
| Scraping position | `No scraping needed`, `Scraping unnecessary if API is used`, `Scraping discouraged when API exists`, `Scraping allowed with limits`, `Scraping legally unclear`, `Scraping prohibited`, `Unknown` |
| GitHub resource type | `repository`, `user`, `organization`, `N/A` |
| Hugging Face repository type | `model`, `dataset`, `space`, `N/A` |
| DQV expected datatype | `boolean`, `integer`, `decimal`, `string`, `date`, `dateTime`, `uri`, `duration`, `percentage`, `count` |
| Rating | Integer from `1` to `5` |
| Reuse status | `Draft`, `Tested`, `Reusable`, `Published`, `Archived`, `Deprecated`, `Unknown` |
| Skill status | `draft`, `experimental`, `stable`, `deprecated`, `archived` |

## Source Levels

| Value | Meaning |
| --- | --- |
| `L1_portal` | A portal, catalogue, registry, or institutional access point that hosts multiple datasets or records. |
| `L2_dataset` | A specific dataset, file collection, API, repository dataset, or stable data access path. |
| `L3_fragmented_source` | A source that requires extraction, parsing, reconciliation, cross-referencing, or transformation before reuse. |

## DCAT Connections

For structured open data, DCAT fields can be prefilled from open data portal APIs. Examples include CKAN package APIs, data.gov harvest records, data.gouv.fr dataset APIs, and open.canada.ca catalogue APIs.

When a portal exposes DCAT or DCAT-like JSON, contributors should use the official API or catalogue export to populate fields such as title, description, publisher, identifier, landing page, access URL, download URL, media type, license, spatial coverage, temporal coverage, themes, and keywords.

Source Commons does not replace DCAT. It keeps DCAT-compatible fields and adds operational fields for access method, pricing, rate limits, legal risk, extraction difficulty, join keys, crosswalks, and workflow context.

## Wikidata Connections

Wikidata fields make Source Commons records easier to reconcile with a shared knowledge graph. They should be treated as identifiers and assisted relationships, not as free-text tags.

Level 1 is the optional `wikidata_id` field on entity-bearing tables. It stores one primary Wikidata item for the source, tool, or use case when a clear item exists. Examples include `Q142` for France, `Q95` for Google, `Q8908` for Wikimedia Foundation, and `Q720467` for Hugging Face.

Evaluation rows do not get a separate `wikidata_id` in this version because they describe dated observations about another record. They inherit entity context through `source_id`.

Level 2 adds assisted source relationships with `wikidata_main_topics` and `wikidata_related_entities`. Autocomplete should search Wikidata labels and aliases, while the stored value should preserve the QID. For example, a France Travail open data source could use `Employment (Q12737077)` as a main topic and `France Travail (Q124556307); Ministry of Labour (Q3406276)` as related entities.

Level 3 uses `wikidata_advanced_relations` for curated property-value relationships. Store each relation as a compact object such as `{"property":"P137","value":"Q95"}`, where `P137` is a Wikidata property and `Q95` is a Wikidata item. Because relation objects contain commas, quote the CSV cell when a relation is present. The UI should offer a small curated property list for common relationships such as owner, publisher, funder, operator, and covered area, with property search available only inside the advanced relation control.

Contributors should not choose freely from all Wikidata properties in normal editing. Properties such as `P31`, `P279`, `P361`, `P527`, `P749`, `P1269`, and `P2578` may be useful in expert curation, but they are too broad or specialized for default contributor workflows.

## GitHub Connections

GitHub fields connect a source, tool, or use case to a primary repository, person account, or organization account when that link helps explain provenance, implementation, maintenance, issue tracking, or reproducibility.

Use `github_resource_type` to choose `repository`, `user`, `organization`, or `N/A`. Use `github_resource_id` for the repository full name or account login. Examples include `openrefine/openrefine` for a repository, `github` for an organization, and `octocat` for a user account.

Use `github_url` for the public GitHub URL and `github_api_url` for the REST API metadata endpoint when checked. Examples include `https://github.com/openrefine/openrefine`, `https://api.github.com/repos/openrefine/openrefine`, `https://api.github.com/orgs/github`, and `https://api.github.com/users/octocat`.

GitHub links should be factual and relevant. A record should not link to a promotional account when an official repository, maintainer organization, or reproducibility repository is available.

## Hugging Face Connections

Hugging Face metadata appears only in fields beginning with `hf_`.

These fields can point to models, datasets, Spaces, discussions, or workflow dependencies. They should be filled from public Hugging Face Hub API responses or repository metadata. Contributors should still verify licenses, gated access, model cards, dataset cards, and redistribution limits before relying on a repository.

## Required Fields

Required fields are the minimum fields needed for a pull request to be reviewable. Operational details such as account requirements, authentication, rate limits, pricing, join keys, and legal notes are encouraged when known, but they are optional so public datasets can be submitted without unnecessary friction.

| File | Required fields |
| --- | --- |
| `data/sources.csv` | `source_id`, `source_level`, `dct_title`, `dct_description`, `dct_publisher`, `dcat_landing_page`, `access_method` |
| `data/tools.csv` | `tool_id`, `dct_title`, `tool_category`, `tool_homepage`, `open_source_license`, `typical_tasks`, `legal_risk_level` |
| `data/evaluations.csv` | `evaluation_id`, `source_id`, `dqv_dimension`, `dqv_metric_uri`, `dqv_metric`, `dqv_expected_datatype`, `rating_1_5`, `confidence`, `evaluator_id` |
| `data/use-cases.csv` | `use_case_id`, `dct_title`, `source_ids`, `sector`, `workflow_summary`, `tools_used`, `legal_aspects`, `impact`, `source_join_keys_used`, `join_strategy` |
| `data/skills.csv` | `skill_id`, `title`, `summary`, `version`, `status`, `keywords`, `solves`, `skill_url`, `markdown_path` |

## `data/sources.csv`

| Field | Required | Cardinality | Type or format | Values | Example | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `source_id` | Yes | Single | Identifier | Prefix `SRC-` | `SRC-CA-TORONTO-BUILDING-PERMITS` | Stable Source Commons source id. |
| `source_level` | Yes | Single select | Controlled value | Source level values | `L2_dataset` | Use `L1_portal` for catalogues, `L2_dataset` for stable datasets, and `L3_fragmented_source` when extraction or reconciliation is needed. |
| `dct_title` | Yes | Single | Text | Source title | `Building Permits - Active Permits` | Maps to Dublin Core title. |
| `dct_description` | Yes | Single | Text | Source description | `Information on currently active building applications and permits in Toronto.` | Keep concise and factual. |
| `dct_publisher` | Yes | Single | Text or URI | Publisher name or identifier | `City of Toronto` | Maps to Dublin Core publisher. |
| `dct_identifier` | No | Single | Text or URI | Official identifier | `toronto-building-permits-active` | Use the source identifier, catalogue id, DOI, accession number, or repository id. |
| `wikidata_id` | No | Single | Wikidata item | QID | `Q142` | Primary Wikidata item for the source when one clear item exists. |
| `dcat_landing_page` | Yes | Single | URL | Official landing page | `https://open.toronto.ca/dataset/building-permits-active-permits/` | Maps to DCAT landing page. |
| `dcat_access_url` | No | Single or multiple | URL list | Access URL values | `https://ckan0.cf.opendata.inter.prod-toronto.ca/api/3/action/package_show?id=building-permits-active-permits` | Maps to DCAT access URL. |
| `dcat_download_url` | No | Single or multiple | URL list | Download URL values | `https://example.org/download.csv` | Maps to DCAT download URL. |
| `dcat_distribution_format` | No | Multiple select or text | Format list | IANA media label, file extension, or source format label | `CSV; JSON; API` | Maps to DCAT distribution format. |
| `dcat_media_type` | No | Single or multiple | IANA media type | Media type values | `text/csv` | Maps to DCAT media type. |
| `dcat_endpoint_url` | No | Single | URL | API endpoint URL | `https://example.org/api/search` | Maps to DCAT endpoint URL for a data service. |
| `dcat_prefill_url` | No | Single | URL | Portal metadata URL | `https://open.canada.ca/data/en/api/3/action/package_show?id=example` | The API or metadata record used to fill DCAT fields. |
| `dcat_prefill_status` | No | Single select | Controlled value | Metadata status values | `Available` | Status of the portal metadata prefill. |
| `dct_access_rights` | No | Single select or source text | Controlled value or official source label | Access rights values | `Public` | Maps to Dublin Core access rights. Public open data submissions may default to `Public`. |
| `dct_license` | No | Single | Text or URL | License name, SPDX id, rights statement, or terms URL | `City of Toronto Open Data Licence` | Prefer official license URLs or SPDX ids when possible. |
| `dct_spatial` | No | Single or multiple | Country, region, geometry, URI, or text | ISO 3166 codes preferred for countries and regions | `CA-ON` | Maps to Dublin Core spatial coverage. |
| `dct_temporal` | No | Single | Temporal coverage | ISO 8601 date, year, interval, or source label | `2020-01-01/2025-12-31` | Maps to Dublin Core temporal coverage. |
| `dcat_theme` | No | Single or multiple | Text, URI, or controlled source theme | Theme values from source catalogue when available | `Urban planning` | Maps to DCAT theme. |
| `dcat_keywords` | No | Multiple | Text list | Keywords | `building permits; development; construction` | Maps to DCAT keyword. |
| `wikidata_main_topics` | No | Multiple | Wikidata item list | QIDs or labels with QIDs | `Employment (Q12737077)` | Main concepts covered by the source. Store the QID as the stable value. |
| `wikidata_related_entities` | No | Multiple | Wikidata item list | QIDs or labels with QIDs | `France Travail (Q124556307); Ministry of Labour (Q3406276)` | Organizations, places, people, products, laws, or other entities related to the source. |
| `wikidata_advanced_relations` | No | Multiple | Wikidata advanced relation list | Curated property-value objects | `{"property":"P137","value":"Q95"}` | Advanced relationships such as operator, owner, publisher, funder, or covered area. |
| `access_method` | Yes | Single or multiple | Text list | API, bulk download, file download, web page, repository files, request process, export | `Open data API; file download` | Practical access route for users. |
| `access_account_required` | No | Single select | Boolean-like | `true`, `false`, `Unknown` | `false` | Whether account creation is required. Optional unless access requires an account. |
| `auth_method` | No | Single or multiple select | Controlled value list | Authentication method values | `None` | Use `None` when no authentication is required. Optional for simple public downloads. |
| `rate_limit_declared` | No | Single select | Boolean-like | `true`, `false`, `Unknown` | `Unknown` | Whether the source declares a rate limit. Optional unless the contributor knows the limit. |
| `rate_limit_scope` | No | Single select | Controlled value | Rate limit scope values | `IP` | Required when a rate limit is known. |
| `rate_limit_value` | No | Single | Number | Positive number | `10` | Numeric rate limit value. |
| `rate_limit_period` | No | Single select | Controlled value | Rate limit period values | `second` | Period for `rate_limit_value`. |
| `rate_limit_notes` | No | Single | Text | Notes | `Use conservative polling when no limit is published.` | Explain fair use or undocumented limits. |
| `access_cost_type` | No | Single select | Controlled value | Access cost type values | `Free` | Broad access cost class. Public open data may default to `Free`. |
| `pricing_model` | No | Single select | Controlled value | Pricing model values | `free_open_access` | Practical pricing model. Public open data may default to `free_open_access`. |
| `pricing_currency` | No | Single | ISO 4217 code or `N/A` | Currency code | `USD` | Use only when pricing applies. |
| `pricing_amount` | No | Single | Decimal number or `N/A` | Price amount | `0` | Use `N/A` when no price applies. |
| `pricing_unit` | No | Single select or text | Pricing unit | `request`, `month`, `year`, `seat`, `dataset`, `download`, `N/A` | `month` | Unit attached to `pricing_amount`. |
| `pricing_notes` | No | Single | Text | Notes | `No fee declared for official API or downloads.` | Explain uncertain pricing. |
| `update_frequency` | No | Single select or source text | Frequency | `real-time`, `hourly`, `daily`, `weekly`, `monthly`, `quarterly`, `annual`, `irregular`, `unknown`, or official DCAT frequency URI | `daily` | Can be prefilled from DCAT accrual periodicity. |
| `structuredness` | No | Single select | Controlled value | Structuredness values | `Structured` | Describes machine readability. |
| `fragmentation_level` | No | Single select | Controlled value | Fragmentation level values | `Low` | How scattered the source is. |
| `extraction_difficulty` | No | Single select | Controlled value | Extraction difficulty values | `Low` | Estimated effort to turn the source into usable data. |
| `stable_identifiers` | No | Single or multiple | Text list | Identifier names | `permit_number; address` | Stable ids provided by the source. |
| `join_keys` | No | Multiple | Text list | Field names | `permit_number; address; ward` | Concrete fields usable for joins. |
| `legal_risk_level` | No | Single select | Controlled value | Risk level values | `Low` | Overall legal and ethical risk. Recommended when legal or ethical reuse constraints are known. |
| `legal_risk_notes` | No | Single | Text | Notes | `Open data license; geocoding and personal data minimization should be checked.` | Include license, terms, privacy, copyright, and redistribution issues. |
| `scraping_position` | No | Single select | Controlled value | Scraping position values | `No scraping needed` | Prefer official APIs, exports, and bulk downloads. |
| `documented_exception_cases` | No | Single | Text | Notes | `Use API rather than rendered pages.` | Known exceptions, limits, or safer access paths. |
| `dct_conforms_to` | No | Multiple | Text or URI list | Standards and profiles | `DCAT-3; DQV; SourceCommons-ODSP-0.1` | Maps to Dublin Core conforms to. |
| `join_key_types` | No | Multiple select | Controlled value list | `entity_id`, `entity_name`, `organization`, `person`, `geography`, `address`, `date`, `time`, `document_id`, `filing_id`, `topic`, `category`, `amount`, `version`, `other` | `address; geography; date` | Optional types of join keys when known. |
| `join_key_examples` | No | Multiple | Text list | Examples | `permit_number=24 123456; ward=10` | Show realistic values. |
| `join_key_granularity` | No | Single | Text | Granularity label | `Permit and parcel level` | Optional description of the row, entity, observation, document, or event level. |
| `join_key_confidence` | No | Single select | Controlled value | Confidence values | `High` | Confidence in joining this source to others. |
| `crosswalk_source_ids` | No | Multiple | Identifier list | Source ids | `SRC-CA-HOC-HANSARD` | Other Source Commons sources that can be linked. |
| `crosswalk_notes` | No | Single | Text | Notes | `Address and ward keys allow joins with planning sources.` | Include caveats and matching methods. |
| `github_resource_type` | No | Single select | Controlled value | GitHub resource type values | `organization` | Primary GitHub resource type linked to this source. |
| `github_resource_id` | No | Single | GitHub resource id | Repository full name or account login | `github` | Repository `owner/name`, organization login, or user login. |
| `github_url` | No | Single | URL | GitHub URL | `https://github.com/github` | Public GitHub URL for the linked resource. |
| `github_api_url` | No | Single | URL | GitHub REST API URL | `https://api.github.com/orgs/github` | API metadata endpoint for the linked resource. |
| `github_metadata_status` | No | Single select | Controlled value | Metadata status values | `Available` | Status of GitHub metadata verification. |
| `hf_repo_type` | No | Single select | Controlled value | Hugging Face repository type values | `dataset` | Use only when the source is represented on Hugging Face. |
| `hf_repo_id` | No | Single | `namespace/name` | Hugging Face repository id | `rabuahmad/climatecheck` | Repository id from the Hub. |
| `hf_api_url` | No | Single | URL | Hub API URL | `https://huggingface.co/api/datasets/rabuahmad/climatecheck` | API metadata endpoint. |
| `hf_metadata_status` | No | Single select | Controlled value | Metadata status values | `Available` | Status of Hub metadata. |

## `data/tools.csv`

| Field | Required | Cardinality | Type or format | Values | Example | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `tool_id` | Yes | Single | Identifier | Prefix `TOOL-` | `TOOL-FRICTIONLESS` | Stable Source Commons tool id. |
| `dct_title` | Yes | Single | Text | Tool name | `Frictionless Framework` | Maps to Dublin Core title. |
| `wikidata_id` | No | Single | Wikidata item | QID | `Q720467` | Primary Wikidata item for the tool or platform when one clear item exists. |
| `tool_category` | Yes | Single or multiple select | Controlled value list | `AI repository metadata`, `Validation`, `Cleaning`, `Reconciliation`, `Extraction`, `Browser automation`, `Analytics`, `Publishing`, `Geocoding`, `Quality evaluation`, `Other` | `Validation` | Tool role in the framework. |
| `tool_homepage` | Yes | Single | URL | Official URL | `https://framework.frictionlessdata.io/` | Prefer official documentation or repository. |
| `open_source_license` | Yes | Single | SPDX id, license name, access statement, or `Unknown` | License values | `MIT` | For closed or hosted tools, document access terms. |
| `input_formats` | No | Multiple | Text list | Formats | `CSV; Excel; JSON` | Input formats the tool can process. |
| `output_formats` | No | Multiple | Text list | Formats | `validated CSV; schema reports` | Output formats the tool can produce. |
| `source_levels_supported` | No | Multiple select | Controlled value list | Source level values | `L2_dataset; L3_fragmented_source` | Source levels where the tool is useful. |
| `typical_tasks` | Yes | Single | Text | Task summary | `Validate CSV structure, infer schemas, create data packages.` | Keep operational and concrete. |
| `legal_use_guidance` | No | Single | Text | Guidance | `Legal risk depends on the source being processed.` | Explain safe use boundaries. |
| `legal_risk_level` | Yes | Single select | Controlled value | Risk level values | `Low` | Risk from typical use of the tool. |
| `recommended_controls` | No | Single | Text | Controls | `Keep original source URL, license, retrieval date, and transformation logs.` | Safeguards for responsible use. |
| `dct_conforms_to` | No | Multiple | Text or URI list | Standards and profiles | `Data Package; DCAT-compatible metadata mapping; SourceCommons-ODSP-0.1` | Standards or APIs the tool supports. |
| `github_resource_type` | No | Single select | Controlled value | GitHub resource type values | `repository` | Primary GitHub resource type linked to the tool. |
| `github_resource_id` | No | Single | GitHub resource id | Repository full name or account login | `frictionlessdata/framework` | Repository `owner/name`, organization login, or user login. |
| `github_url` | No | Single | URL | GitHub URL | `https://github.com/frictionlessdata/framework` | Public GitHub URL for the linked resource. |
| `github_api_url` | No | Single | URL | GitHub REST API URL | `https://api.github.com/repos/frictionlessdata/framework` | API metadata endpoint for the linked resource. |
| `github_metadata_status` | No | Single select | Controlled value | Metadata status values | `Available` | Status of GitHub metadata verification. |
| `hf_repo_type` | No | Single select | Controlled value | Hugging Face repository type values | `model` | Use for models or Spaces represented on the Hub. |
| `hf_repo_id` | No | Single | `namespace/name` | Hugging Face repository id | `climatebert/distilroberta-base-climate-detector` | Repository id from the Hub. |
| `hf_api_url` | No | Single | URL | Hub API URL | `https://huggingface.co/api/models/climatebert/distilroberta-base-climate-detector` | API metadata endpoint. |
| `hf_task_or_sdk` | No | Single or multiple | Text list | Hub task, SDK, or library label | `text-classification` | From Hub metadata when available. |
| `hf_license` | No | Single | SPDX id, Hub license tag, or `N/A` | License value | `apache-2.0` | Verify against the model or Space card. |
| `hf_last_modified` | No | Single | ISO 8601 date time or date | Date time | `2026-05-30T14:32:00Z` | From Hub metadata when available. |
| `hf_metadata_status` | No | Single select | Controlled value | Metadata status values | `Available` | Status of Hub metadata. |

## `data/evaluations.csv`

| Field | Required | Cardinality | Type or format | Values | Example | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `evaluation_id` | Yes | Single | Identifier | Prefix `EVAL-` | `EVAL-001` | Stable Source Commons evaluation id. |
| `source_id` | Yes | Single | Identifier | Existing `SRC-` id | `SRC-US-ED-CRDC-HARASSMENT` | Source being evaluated. |
| `dqv_dimension` | Yes | Single select or URI-like label | DQV or Source Commons dimension | `dqv:Availability`, `dqv:Completeness`, `dqv:Consistency`, `dqv:Accuracy`, `dqv:Timeliness`, `dqv:Licensing`, `sc:Exploitability`, `sc:LegalRisk`, `sc:Joinability` | `dqv:Availability` | DQV does not require a closed list; Source Commons recommends these starting values. |
| `dqv_dimension_uri` | No | Single | URI | DQV or Source Commons URI | `https://www.w3.org/ns/dqv#Dimension` | URI for the quality dimension when available. |
| `dqv_metric` | Yes | Single | Text | Metric label | `DCAT_record_available` | Human-readable or machine-friendly metric name. |
| `dqv_metric_uri` | Yes | Single | URI or compact URI | Metric URI | `sc:metric/DCATRecordAvailable` | Stable metric identifier. |
| `dqv_expected_datatype` | Yes | Single select | Controlled value | DQV expected datatype values | `boolean` | Expected datatype for `dqv_value`. |
| `dqv_value` | No | Single | Value matching expected datatype | Metric value | `true` | Observed metric value. |
| `dqv_unit` | No | Single | Text or URI | Unit | `boolean` | Unit for the value when relevant. |
| `rating_1_5` | Yes | Single select | Integer | `1`, `2`, `3`, `4`, `5` | `5` | Human rating where `5` is strongest. |
| `confidence` | Yes | Single select | Controlled value | Confidence values | `High` | Confidence in the evaluation. |
| `dqv_computed_on` | No | Single | ISO 8601 date or date time | Date or date time | `2026-05-30` | Date the evaluation was performed. |
| `dqv_measurement_method` | No | Single | Text | Method description | `Checked harvest record JSON and first download URL.` | Manual check, script, API call, or review method. |
| `evaluator_id` | Yes | Single | Identifier | Contributor or organization id | `CONTRIB-001` | Evaluator id. |
| `evaluator_role` | No | Single | Text | Role label | `Source curator` | Expertise or responsibility of evaluator. |
| `dqv_quality_annotation` | No | Single | Text | Annotation | `A DCAT JSON record can prefill core metadata.` | Maps to DQV quality annotation. |
| `legal_risk_level` | No | Single select | Controlled value | Risk level values | `Low` | Legal or ethical risk observed during evaluation. |
| `legal_risk_comment` | No | Single | Text | Risk comment | `Attribution and context should be preserved.` | Explain risk and evidence. |
| `recommended_action` | No | Single | Text | Action | `Add importer mapping for data.gov harvest records.` | Suggested fix or follow-up. |

## `data/use-cases.csv`

| Field | Required | Cardinality | Type or format | Values | Example | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `use_case_id` | Yes | Single | Identifier | Prefix `UC-` | `UC-001` | Stable Source Commons use case id. |
| `dct_title` | Yes | Single | Text | Use case title | `Urban development early signal monitor` | Maps to Dublin Core title. |
| `wikidata_id` | No | Single | Wikidata item | QID | `Q12737077` | Primary Wikidata item for the use case topic when one clear item exists. |
| `source_ids` | Yes | Multiple | Identifier list | Existing `SRC-` ids | `SRC-CA-TORONTO-BUILDING-PERMITS; SRC-CA-HOC-HANSARD` | Sources used by the workflow. |
| `sector` | Yes | Single or multiple | Text list | Domain labels | `Urban planning` | Sector or problem area. |
| `user_org_type` | No | Single | Text | Organization type | `City strategy team` | Type of user or team. |
| `question_answered` | No | Single | Text | Question | `Where are construction and policy signals increasing?` | Main question addressed. |
| `workflow_summary` | Yes | Single | Text | Workflow summary | `Normalize permits, geocode addresses, extract policy mentions, aggregate by district and topic.` | Short operational workflow. |
| `tools_used` | Yes | Multiple | Identifier list | Existing `TOOL-` ids | `TOOL-OPENREFINE; TOOL-FRICTIONLESS` | Tools used by the workflow. |
| `output_type` | No | Single or multiple select | Controlled value list | `Dataset`, `Dashboard`, `API`, `Notebook`, `Report`, `Briefing`, `Model`, `Knowledge base`, `Map`, `Other` | `Dashboard; briefing` | Output produced by the workflow. |
| `result_link` | No | Single | URL or status label | URL, `not_published_demo`, `internal_only`, `N/A` | `not_published_demo` | Link to output when available. |
| `legal_aspects` | Yes | Single | Text | Legal notes | `Use official open data API and cite municipal source.` | License, terms, privacy, scraping, or redistribution considerations. |
| `impact` | Yes | Single | Text | Impact statement | `Earlier detection of local development pressure.` | Practical value or expected outcome. |
| `audience` | No | Single or multiple | Text list | Audience labels | `Researchers; public teams` | Intended users or beneficiaries. |
| `reuse_status` | No | Single select | Controlled value | Reuse status values | `Draft` | Maturity of the use case. |
| `confidence` | No | Single select | Controlled value | Confidence values | `Medium` | Confidence in the workflow or evidence. |
| `source_join_keys_used` | Yes | Multiple | Text list | Source id and key names | `SRC-CA-TORONTO-BUILDING-PERMITS: ward; address; application_date` | Join keys actually used. |
| `join_strategy` | Yes | Single | Text | Strategy description | `Geocode addresses, aggregate by ward and week, then join with policy topics.` | How sources are connected. |
| `join_confidence` | No | Single select | Controlled value | Confidence values | `Medium` | Confidence in source joins. |
| `github_resource_type` | No | Single select | Controlled value | GitHub resource type values | `repository` | Primary GitHub resource type linked to the use case. |
| `github_resource_id` | No | Single | GitHub resource id | Repository full name or account login | `example-org/urban-monitor-demo` | Repository `owner/name`, organization login, or user login. |
| `github_url` | No | Single | URL | GitHub URL | `https://github.com/example-org/urban-monitor-demo` | Public GitHub URL for the linked resource. |
| `github_api_url` | No | Single | URL | GitHub REST API URL | `https://api.github.com/repos/example-org/urban-monitor-demo` | API metadata endpoint for the linked resource. |
| `github_metadata_status` | No | Single select | Controlled value | Metadata status values | `Not checked` | Status of GitHub metadata verification. |
| `hf_models_used` | No | Multiple | `namespace/name` list | Hub model ids or `N/A` | `climatebert/distilroberta-base-climate-detector` | Hugging Face models used. |
| `hf_spaces_used` | No | Multiple | `namespace/name` list | Hub Space ids or `N/A` | `narcis2007/ClimateBERT` | Hugging Face Spaces used. |
| `hf_datasets_used` | No | Multiple | `namespace/name` list | Hub dataset ids or `N/A` | `rabuahmad/climatecheck` | Hugging Face datasets used. |
| `hf_discussion_refs` | No | Multiple | URL list | Hub discussion URLs or API URLs | `https://huggingface.co/api/models/example/model/discussions` | Hub discussions, issues, or review context. |

## `data/skills.csv`

Skills are reusable capability descriptions: a method, recipe, promptable workflow, context package, or operational procedure that helps someone do a recurring task. A skill can mention tools and datasets, but it is not itself a software tool. A skill can support many use cases.

Every skill is represented twice:

- one row in `data/skills.csv` for indexing, search, and review;
- one Markdown file in `skills/{skill_id}.md` with generated YAML frontmatter and editable Markdown body.

| Field | Required | Cardinality | Type or format | Values | Example | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `skill_id` | Yes | Single | Identifier | Prefix `scf-skill-` plus UUID | `scf-skill-6f4d8e5c-12c2-4b61-9f62-c6b3e713b35d` | Generated by scframework.org. Stable public skill id. |
| `title` | Yes | Single | Text | Skill title | `Geocode addresses` | Human-readable name. |
| `summary` | Yes | Single | Text | Short summary | `Convert postal addresses into geographic coordinates.` | One sentence for cards and search. |
| `version` | Yes | Single | Semantic-ish version | Version string | `0.1` | Increment when the method meaningfully changes. |
| `status` | Yes | Single select | Controlled value | Skill status values | `stable` | Maturity of the skill. |
| `keywords` | Yes | Multiple | Text list | Keywords | `geocoding; addresses; maps` | Search terms. |
| `solves` | Yes | Multiple | Text list | Problems solved | `address matching; territorial analysis` | Problems or tasks the skill helps solve. |
| `description` | No | Single | Markdown-capable text | Description | `Convert postal addresses into coordinates using open datasets and APIs.` | Longer description, also included in frontmatter when provided. |
| `authors` | No | Multiple | Text list | People or organizations | `Source Commons Lab` | Authors or maintainers. |
| `license` | No | Single | SPDX id or license label | License value | `CC-BY-4.0` | License for the skill text and method. |
| `created` | No | Single | ISO 8601 date | Date | `2026-06-05` | Initial creation date. |
| `updated` | No | Single | ISO 8601 date | Date | `2026-06-05` | Last meaningful update date. |
| `categories` | No | Multiple | Text list | Category labels | `geography; transport` | Broad skill category. |
| `domain` | No | Multiple | Text list | Domain labels | `mobility` | Domain where the skill is useful. |
| `use_cases` | No | Multiple | Text list | Use case labels or ids | `delivery optimization; territory observatories` | Use cases helped by the skill. |
| `inputs` | No | Multiple | Text list | Inputs | `postal address` | Expected input material. |
| `outputs` | No | Multiple | Text list | Outputs | `latitude; longitude` | Expected outputs. |
| `tools` | No | Multiple | Text list or ids | Tools | `DuckDB; Python` | Tools often used by the skill. |
| `datasets` | No | Multiple | Text list or ids | Datasets | `OpenStreetMap; BAN` | Useful datasets. |
| `mcp_servers` | No | Multiple | Text list | MCP server ids | `datagouv-mcp` | Optional MCP servers supporting the skill. |
| `related_skills` | No | Multiple | Identifier or slug list | Skill ids or slugs | `reverse-geocoding` | Related or complementary skills. |
| `works_with` | No | Multiple | File, format, or context labels | Context references | `context.md; GeoJSON` | Files or formats the skill can operate with. |
| `references` | No | Multiple | URL list | Absolute URLs | `https://wiki.openstreetmap.org/wiki/Nominatim` | References and documentation. |
| `canonical_url` | No | Single | URL | Absolute URL | `https://sourcecommons.org/skills/geocode-addresses` | External canonical page when one exists. |
| `language` | No | Single | BCP 47 language tag | Language code | `en` | Main language. |
| `alternate_languages` | No | Multiple | BCP 47 language tags | Language codes | `fr` | Languages available or expected. |
| `skill_url` | Yes | Single | URL path or absolute URL | scframework URL | `https://scframework.org/skill/scf-skill-...` | Public page generated by scframework.org. |
| `markdown_path` | Yes | Single | Repository path | Markdown file path | `skills/scf-skill-....md` | Markdown file written in the same pull request. |

The generated YAML frontmatter should preserve the same field names as the CSV where possible. Multi-value fields are YAML arrays in Markdown and semicolon-separated lists in CSV.

## Example Source Row

The CSV files in this repository remain empty except for headers. This example shows the expected style for a future source pull request.

```csv
source_id,source_level,dct_title,dct_description,dct_publisher,dct_identifier,wikidata_id,dcat_landing_page,dcat_access_url,dcat_download_url,dcat_distribution_format,dcat_media_type,dcat_endpoint_url,dcat_prefill_url,dcat_prefill_status,dct_access_rights,dct_license,dct_spatial,dct_temporal,dcat_theme,dcat_keywords,wikidata_main_topics,wikidata_related_entities,wikidata_advanced_relations,access_method,access_account_required,auth_method,rate_limit_declared,rate_limit_scope,rate_limit_value,rate_limit_period,rate_limit_notes,access_cost_type,pricing_model,pricing_currency,pricing_amount,pricing_unit,pricing_notes,update_frequency,structuredness,fragmentation_level,extraction_difficulty,stable_identifiers,join_keys,legal_risk_level,legal_risk_notes,scraping_position,documented_exception_cases,dct_conforms_to,join_key_types,join_key_examples,join_key_granularity,join_key_confidence,crosswalk_source_ids,crosswalk_notes,related_source_ids,related_tool_ids,related_use_case_ids,related_skill_ids,related_evaluation_ids,github_resource_type,github_resource_id,github_url,github_api_url,github_metadata_status,hf_repo_type,hf_repo_id,hf_api_url,hf_metadata_status
SRC-CA-TORONTO-BUILDING-PERMITS,L2_dataset,Building Permits - Active Permits,Information on currently active building applications and permits in Toronto.,City of Toronto,toronto-building-permits-active,,https://open.toronto.ca/dataset/building-permits-active-permits/,https://ckan0.cf.opendata.inter.prod-toronto.ca/api/3/action/package_show?id=building-permits-active-permits,,CSV; JSON; API,application/json,https://ckan0.cf.opendata.inter.prod-toronto.ca/api/3/action/package_show?id=building-permits-active-permits,https://open.toronto.ca/dataset/building-permits-active-permits/,Partial,Public,City of Toronto Open Data Licence,CA-ON,Current,Urban planning,building permits; development; construction; addresses,,,,Open data API; file download,false,None,Unknown,IP,,,No public limit found; check API behavior before monitoring.,Free,free_open_access,N/A,N/A,N/A,No fee declared for official API or downloads.,daily,Structured,Low,Low,Permit numbers and addresses,permit_number; address; ward; application_date,Low,Open data license; geocoding and personal data minimization should be checked.,No scraping needed,Use official open data API or downloads.,DCAT-3; DQV; SourceCommons-ODSP-0.1,address; geography; date,permit_number=24 123456; ward=10; application_date=2026-01-12,Permit and parcel level,High,N/A,Address and ward keys allow joins with planning and zoning sources.,,,,,N/A,N/A,N/A,N/A,N/A,N/A,N/A,N/A,N/A
```

## Identifier Rules

Identifiers should be stable and human-readable. Suggested prefixes:

- `SRC-` for sources.
- `TOOL-` for tools.
- `EVAL-` for evaluations.
- `UC-` for use cases.
- `scf-skill-` plus a UUID for skills.

Records should not reuse an identifier for a different entity after publication.
