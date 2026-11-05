# Border Tech Texts: Proposed Pipeline 1.0

Status: draft for discussion with collaborators  
Date: 28 October 2026  
Companion document: `Border_Tech_Texts_Data_Report.md` (inventory of the current LexisNexis corpus)

## Summary

We have a LexisNexis corpus of about 32,800 unique English-language documents (1990 – 2025) on border technology, retrieved country by country. The next phase has two tasks:

1. **Coverage expansion.** Extend the corpus to as many countries and languages as possible, 1990 to the present, using code-driven retrieval from archives, with LLMs used for query design and relevance filtering rather than as a search engine.
2. **Structured dataset.** Turn the existing and new texts into a structured dataset of border-technology deployments. The chosen path is: LLM-generated labels on a small sample, human verification, fine-tuning of GLiNER on the verified labels, then full-corpus extraction with the fine-tuned model.

Both tasks share one design change from the current corpus: retrieval and extraction are **concept-first**, and country assignment is derived from the text, not from the query.

## 1. Starting point

- 65,618 country × document rows, 32,812 unique documents, 1.15 billion words (full text plus LexisNexis metadata).
- 168 country folders, extremely uneven (US 8,067 documents; 34 countries under 10). Country folders reflect the search query, so some are noisy (e.g. central_african_republic matches "Central African").
- Half of all rows are the same document filed under more than one country. The two download batches disagree for Greece.
- Effectively English only. Roughly a quarter of rows are templated financial briefs or blog aggregators.
- Each `FullText` ends with a LexisNexis index block (subject, industry, geography codes) that must be stripped before text processing, but is useful as weak labels.

## 2. Task 1: Coverage expansion

### 2.1 Goal

A document store covering border-technology reporting from 1990 to the present for the largest feasible set of countries and languages, with every document carrying provenance, retrieval query, language, and a relevance score.

### 2.2 Principles

- **LLMs do not retrieve.** They cannot return a 1995 Arabic newspaper article and their "search" is not reproducible. We use them to (a) translate and localise query terms, (b) classify relevance, (c) discover which archives exist for a country. All documents come from indexed archives through logged, re-runnable queries.
- **Concept-first queries.** Search by technology concepts and named systems, not by country name. Country is assigned afterwards from geography tags and extracted entities (see Task 2).
- **Recall first, then filter.** Broad queries, followed by a classifier, with precision and recall measured on a hand-labelled validation set.
- **Coverage is a result, not an assumption.** Maintain a country × year × language × source matrix. Absence of documents is distinguished from absence of events.
- **Licensing.** Full text from licensed databases stays internal. Public releases contain structured records and short evidence spans only.

### 2.3 Sources by period

No single archive covers 1990 – present multilingually, so sources are layered by period and region.

| Period | Sources | Notes |
|---|---|---|
| All years, first step | LexisNexis re-run with translated term lists | Current queries were English-only; Nexis itself holds large German, French, Spanish, Dutch, Italian, Portuguese press. Cheapest gain. |
| 1990 – 2013, non-English world | FBIS Daily Reports (to 1996), World News Connection (1995 – 2013), BBC Monitoring (already partly in Nexis) | Systematic English translations of foreign media; the only broad option for the 1990s outside Western Europe. |
| 1980s – present | Factiva | About 30 languages, Reuters and Dow Jones wires, stronger Asia and Latin America coverage than Nexis. |
| 2008 – present | Media Cloud, GDELT (full multilingual from 2015, metadata and URLs only), Common Crawl News (2016 –) | Open; good for recent years and for discovering outlets. |
| Regional press databases | Europresse (French), Genios (German), East View (Russian and post-Soviet), Wisers (Chinese, 1998 –), BigKinds (Korean, free, 1990 –), AllAfrica (1997 –) | Access depends on library subscriptions. |
| Non-news, all years | EU TED tenders, Frontex and eu-LISA reports, World Bank / AfDB / ADB project documents, IOM border-management programmes, parliamentary records, vendor press releases and annual reports (Thales, IDEMIA, NEC, Elbit, Huawei, Securiport, Veridos, etc.) | More structured than news and better coverage of the Global South; tenders and project documents are direct evidence of procurement. |

### 2.4 Query taxonomy

One taxonomy drives every source and language:

- **Technology concepts**: biometrics (fingerprint, face, iris), e-passports and e-visas, automated gates, document readers, surveillance towers and ground sensors, CCTV, drones and UAVs, radar, X-ray and radiation scanners, licence-plate readers, entry/exit and API/PNR data systems, integrated border management systems, smart-border and digital-wall programmes.
- **Named systems and programmes**: SIS, VIS, Eurodac, EES, ETIAS, Eurosur, SIVE, US-VISIT, IDENT, SBInet, Integrated Fixed Towers, Secure Freight Initiative, PISCES, MIDAS, and national equivalents collected as we go.
- **Actors**: border and customs agencies, Frontex, IOM, ICAO, vendors.

An LLM produces first-draft term lists per language; native speakers review them, because literal translations ("e-gate") are often not the terms local media use. Term lists are versioned.

### 2.5 Retrieval and filtering

1. Run the term lists against each source through its API or export tool; log query string, source, date range, result count, retrieval date.
2. Normalise every document to one schema: `doc_id, source_db, outlet, title, date, language, country_hints, text, query_id, retrieval_date, licence`.
3. Deduplicate: exact by source ID, then near-duplicate by MinHash on cleaned text (the current corpus is 50% repeats).
4. Relevance classification with a small LLM against a written definition of "relevant" (reports a border-technology deployment, procurement, plan, policy or evaluation; excludes incidental mentions). Build a validation set of about 500 documents, hand-labelled, stratified by source and period; tune the threshold on it and report precision and recall.
5. Record the coverage matrix and publish it alongside the corpus.

### 2.6 Outputs

- Document store (Parquet plus raw text files) with provenance.
- Versioned query taxonomy and multilingual term lists.
- Coverage matrix and a short retrieval report per source.

## 3. Task 2: Structured dataset with fine-tuned GLiNER

### 3.1 Unit of analysis and target schema

The unit is a **border-technology deployment record**: one technology, in one place, by one set of actors, at one time. Draft fields:

| Field | Type | Example |
|---|---|---|
| record_id | id | |
| country | ISO code | ZM |
| location | normalised place | Chirundu border post |
| location_type | category | land crossing / airport / seaport / border segment / national |
| technology | taxonomy code | border management information system |
| system_name | string | Zambia Immigration Management System |
| vendor | linked entity | |
| implementing_agency | linked entity | Zambia Department of Immigration |
| funder | linked entity | Zambia Threshold Project (MCC) |
| date_announced / date_deployed | date | 2008-08 |
| cost | amount + currency | |
| status | category | planned / tendered / deployed / operational / cancelled |
| purpose | category | migration control / customs and trade / counter-terrorism / health |
| evidence | doc_id + char offsets + quote | |

Fields are filled only when supported by an evidence span. The codebook defining each field and category is a deliverable in its own right.

### 3.2 Preprocessing

- Strip the LexisNexis index block and the repeated header from `FullText`; keep the index codes as separate weak labels.
- Drop or flag templated sources (Industry SnapShot, Briefing.com, CountryWatch) and blog aggregators.
- Deduplicate by `ResultId`, then near-duplicates by MinHash.
- Split documents into paragraph-based chunks of roughly 300 – 400 tokens, keeping character offsets into the original document.
- Language detection on every chunk (current corpus is English; new sources will not be).

### 3.3 Entity label scheme for GLiNER

GLiNER extracts spans, so the label set is concrete and span-shaped. Draft labels:

| Label | Definition | Example span |
|---|---|---|
| TECHNOLOGY | A border-control technology or equipment type | "facial recognition gates", "ground sensors" |
| SYSTEM_NAME | A named system or programme | "Eurodac", "ZIMS" |
| VENDOR | Company supplying technology | "Thales", "NEC" |
| AGENCY | Government body operating or procuring | "Customs Service", "Frontex" |
| FUNDER | Organisation financing | "World Bank", "European Commission" |
| BORDER_LOCATION | Specific crossing, airport, port or border segment | "Chirundu border", "Calais" |
| DATE | Date or period tied to the deployment | "September 2007" |
| MONEY | Cost or contract value | "US$25 million" |
| STATUS_PHRASE | Wording that signals status | "has been installed", "tender launched" |

Categories that are not spans (purpose, location_type, final status) are assigned in step 3.4 Phase E from the extracted spans and the surrounding chunk.

### 3.4 The chosen path: LLM bootstrap, human verification, GLiNER fine-tuning

**Phase A: LLM bootstrap labelling.** Select a stratified sample of chunks (by country, period, source type, and, once available, language), on the order of 1,500 – 3,000 chunks. An LLM labels each chunk with the scheme in 3.3, returning spans with character offsets in strict JSON. The prompt carries the codebook. Every output is checked programmatically for offset validity.

**Phase B: Human verification.** Annotators review and correct the LLM labels in an annotation tool (Label Studio, Argilla or Prodigy). A subset of about 20% is double-annotated to measure agreement per label. Disagreements feed back into the codebook. Output: a verified gold set, split into train, development and test, with the test split never seen during tuning.

**Phase C: Fine-tune GLiNER.** Start from a multilingual GLiNER checkpoint (e.g. `urchade/gliner_multi-v2.1`). Fine-tune on the train split, select on development, report precision, recall and F1 per label on the test split. Run error analysis and one or two rounds of active learning: sample chunks where the model is uncertain or disagrees with the LLM labels, verify them, retrain.

**Phase D: Full-corpus inference.** Run the fine-tuned model over all chunks of the existing and new corpus. Store every mention with label, text, confidence, doc_id and offsets. GLiNER is light enough that this runs on one GPU in hours, not days.

**Phase E: From mentions to records.** Assemble deployment records from co-occurring mentions within a chunk or adjacent chunks, using rules: a record needs at least a TECHNOLOGY or SYSTEM_NAME plus a BORDER_LOCATION or country. Normalise entities: vendors to Wikidata or GLEIF, agencies to a controlled list, places to GeoNames, technologies to the taxonomy. Derive status and purpose from STATUS_PHRASE and chunk context with a small classifier. Cluster records across duplicate and near-duplicate articles into one event with links to all sources.

**Deferred to 1.1.** If rule-based assembly in Phase E is not accurate enough, an LLM pass restricted to chunks that already contain a candidate record can assemble relations and attributes. This is kept out of 1.0 to keep cost and dependence on LLM output low.

### 3.5 Quality assurance

- Gold test split from Phase B is the fixed benchmark for every model version.
- A second, record-level gold set (about 200 – 300 deployment records, double-coded by humans from source documents) measures end-to-end accuracy of Phase E, not just span extraction.
- Every field in the released dataset carries an evidence span, so any value can be checked against its source.
- Model, codebook and term-list versions are recorded with every run.

### 3.6 Data model

Four tables, stored as Parquet, raw text kept separately under licence:

- `documents`: one row per unique document, with provenance and language.
- `chunks`: chunk boundaries and offsets.
- `mentions`: one row per extracted span (output of Phase D).
- `records` and `record_sources`: deployment records and their links to supporting documents.

## 4. Multilingual handling and translation

- Source-language text is always kept; translation is a processing layer.
- For languages with Latin script, the multilingual GLiNER base can be fine-tuned directly on source-language chunks, so the gold set in Phase B should include chunks in each major language once the new sources arrive.
- For non-Latin scripts (Chinese, Arabic, Russian, Korean and others), the collaborators' translation model is applied first and extraction runs on the English output. Decide per language after a test on 50 – 100 chunks comparing source-language extraction with translate-then-extract.
- Machine translation fails most on exactly the terms we care about: system names, equipment names, agency acronyms. Ask the translation partner for glossary support, and have bilingual annotators spot-check translations per language.
- Record the translation model version with every translated chunk.

## 5. What to do, in order

| Step | Work | Deliverable |
|---|---|---|
| 1 | Clean and deduplicate the existing corpus; strip LexisNexis metadata; chunk; filter templated sources | Document and chunk tables for the current corpus |
| 2 | Write the codebook: deployment record schema, technology taxonomy, entity label definitions with examples | Codebook v0.1 |
| 3 | Phase A and B on the existing English corpus: LLM bootstrap labels, human verification, agreement report | Gold set v1 (train / dev / test) |
| 4 | Phase C: fine-tune GLiNER, evaluate, one active-learning round | GLiNER-border v1 with per-label scores |
| 5 | Phase D and E on the existing corpus | Structured dataset v0.1 (English only) with evidence spans |
| 6 | In parallel with steps 3 – 5: build the query taxonomy and multilingual term lists; re-run LexisNexis with translated terms; set up access to FBIS / WNC, Factiva and regional databases | Term lists v1; retrieval report; coverage matrix |
| 7 | Ingest new sources through the normalisation and relevance filter; add non-English chunks to the gold set; retrain GLiNER; decide translate-first languages | Corpus v2; GLiNER-border v2 |
| 8 | Record-level evaluation; freeze dataset v1.0 with documentation | Dataset v1.0 and data paper draft |

Steps 1 – 5 only need the data already in hand and can start immediately. Step 6 depends on database access and on native-speaker reviewers.

## 6. Decisions needed

- Final list of fields and categories in the deployment record, and whether policy and evaluation documents (not only deployments) are in scope.
- Which databases the team or its libraries can access (Factiva, FBIS / WNC, East View, Wisers, Europresse, Genios).
- Priority languages for the first multilingual round, and who reviews term lists and translations for each.
- Annotation tool and annotator pool for Phase B.
- Whether the translation partner's model can take a glossary.
- Release policy: what is published (records and evidence spans) versus kept internal (full text).
