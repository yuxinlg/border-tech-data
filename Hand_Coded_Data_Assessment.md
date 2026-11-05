# Hand-coded Border Tech Data: Field Inventory and Assessment

Folder: `/Users/yuxin/Dropbox/Border Tech Fall 2026/Hand-coded Data So Far`
Prepared: 5 November 2026. Read-only inspection; no files were modified.
Companion documents: `Border_Tech_Texts_Data_Report.md` (LexisNexis corpus), `Proposed_Pipeline_1.0.md`.

## 1. What the data is

**This is not LexisNexis output.** It is a hand-coded deployment dataset built by student coders from the open web. None of the 1,191 source links points to LexisNexis; the most common domains are Wikipedia, defenceweb.co.za, idemia.com, reuters.com and biometricupdate.com. The LexisNexis material is the separate 32,812-document text corpus described in the companion report.

| Item | Value |
|---|---|
| Files | 19 Excel workbooks, 1 CSV (Canada), 1 PDF (Mexico, a printed spreadsheet) |
| Rows (xlsx + csv) | 377 |
| Rows in Mexico PDF | 12 (not machine-readable without re-entry) |
| Countries in `country_name_1` | 23 (Turkey file also holds Bulgaria, Georgia and Greece rows) |
| Coders | 11 coder IDs; 15 rows have none |
| Coding dates | May 2025 to May 2026 |
| Unit of a row | One technology deployment: country × border segment × technology subtype |

Four files (Brazil, Kenya, South Africa, Thailand) were all coded on 2025-05-07 under country-specific coder IDs (`CDN_BRA_01` etc.), have no `Lists` sheet, and fill every field with long prose and very specific missing-data explanations. They read like LLM "deep research" output rather than manual coding. Their links should be spot-checked for existence before they are trusted.

## 2. Fields

Three template versions are in use:

| Template | Files | Columns |
|---|---|---|
| v1, no cost fields | Australia, China, Greece, Indonesia, Turkey | 37 |
| v2, with `installation_cost`, `yearly_maintenance_cost`, `funding_source` | Bangladesh, Bhutan, Brazil, Canada, Egypt, India, Kenya, Pakistan, Saudi Arabia, South Africa, Spain, Thailand, Mexico | 40 |
| v2 minus `technology_subtype` | Chile, Portugal | 36 |

Field groups:

| Group | Fields |
|---|---|
| Identity and place | `border_id`, `country_name_1`, `country_name_2`, `border_segment`, `operational_domain` |
| Technology | `technology_type`, `technology_subtype`, `technology_subtype_reported`, `technology_detailed` |
| Operator | `force_structure` |
| Timing and status | `year_of_adoption`, `year_of_installation`, `installation_type`, `operational_status`, `year_of_suspension_termination` |
| Money (v2 only) | `installation_cost`, `yearly_maintenance_cost`, `funding_source` |
| Supplier | `supplier_country`, `supplier_self_use`, `supplier_company`, `technology_sharing_type`, `_type2`, `_type3` |
| Purpose | `purpose`, `purpose2`, `purpose3` |
| Evidence | `data_source1..5`, `link_source1..5` |
| Coding metadata | `missing_data_reason`, `coding_date`, `coder_id`, `personal notes` (Australia only) |

Controlled vocabularies (from the `Lists` sheet): 6 technology types, about 35 subtypes, plus the categories visible in the data for domain, force structure, installation type, status, sharing type and purpose.

## 3. Fill rates and value quality

| Field | Blank | NA-token | Filled (of 377) | Note |
|---|---|---|---|---|
| technology_type | 2 | 0 | 375 | 11 distinct spellings for 6 categories |
| technology_subtype | 44 | 0 | 333 | 42 distinct values; 28 "Other"; column absent in Chile and Portugal |
| technology_subtype_reported | 2 | 0 | 375 | Verbatim phrase from source; good |
| technology_detailed | 15 | 0 | 362 | Quote or paragraph; good |
| force_structure | 22 | 0 | 355 | Egypt uses free text ("Egyptian Armed Forces / Border Guards") |
| year_of_adoption | 24 | 5 | 348 | 59 are free text with parentheses |
| year_of_installation | 26 | 5 | 346 | 81 are free text |
| operational_status | 10 | 0 | 367 | Clean |
| year_of_suspension_termination | 131 | 78 | 168 | Mixes "Ongoing", "N/A", blank, "Was Never Installed" |
| installation_cost | 194 | 35 | 148 | Free text, mixed currencies and units (per sensor vs programme total) |
| yearly_maintenance_cost | 197 | 147 | 33 | Almost empty |
| funding_source | 196 | 2 | 179 | 45 distinct values; "Government Budget" plus long free text |
| supplier_country | 60 | 7 | 310 | Multi-country strings ("India, initially Israel"); "European Union" for a US vendor |
| supplier_self_use | 67 | 49 | 261 | 116 unknown or blank; several multi-answer sentences |
| supplier_company | 78 | 12 | 287 | |
| technology_sharing_type | 99 | 35 | 243 | "Not specified" used as filler in slots 2 and 3 |
| purpose | 7 | 0 | 370 | Off-list values: "Insurgency", "Border Surveillance" |
| link_source1 | 3 | 0 | 374 | 74 rows have one source only |
| missing_data_reason | 175 | 52 | 150 | Row-level; does not say which field is missing |
| coding_date | 25 | 0 | 352 | Four date formats, one value in 1900, one in the future |
| coder_id | 15 | 0 | 362 | |

Other checks:

- `border_id` is not unique: MAR-001 to MAR-004, EGY-SDN-003, GRC-TUR-001, TUR-IRN-001 and TUR-SYR-014 each appear twice. ID patterns vary (`AUS-AIR-001`, `MAR-001`, `AIR-001`).
- `country_name_2` holds neighbouring countries in most rows but also "Air", "Water", "Airport", "Port", "Red Sea", "Multiple (all international passengers)". It mixes two concepts: the counterpart country and the kind of border.
- Granularity is inconsistent. Portugal codes the EU Entry/Exit System as 17 rows, one per airport, with identical content. Indonesia does one row per airport. Saudi Arabia codes a whole 900 km corridor as one row. Brazil splits SISFRON into separate rows per component (radar, UAV, sensors). Row counts per country are therefore not comparable.
- 128 of 374 rows share an identical set of source links with at least one other row; one article supports up to 17 rows. Rows per unique link: 525 links support one row, 124 support two, 11 support 11 to 17 rows.
- Spain row ESP-MAR-001 has its source columns shifted by one (the URL sits in `data_source2`).
- Portugal rows give `supplier_country` = Italy and `supplier_company` = France; the two fields are swapped or wrong.
- Thermal imagers on the India–Pakistan border are coded with purpose "Environmental Monitoring"; this looks like a mis-click.

## 4. Field-by-field verdict

Keep as designed:

- `technology_subtype_reported` and `technology_detailed`. A verbatim phrase plus a supporting quote is exactly the evidence span the pipeline document asks for. This is the strongest part of the design.
- `technology_type` / `technology_subtype` with a controlled list. The taxonomy is usable; it just needs enforcement.
- `year_of_adoption` vs `year_of_installation`, and `operational_status`. The distinction is meaningful. Store the year as an integer and move the parenthetical into a note column.
- `force_structure`, `operational_domain`, `border_segment`, `supplier_country`, `supplier_company`. Sound, but `supplier_country` should be a list, not a sentence.
- Up to five sources with links, `coder_id`, `coding_date`. Standard and necessary.

Redesign:

- `country_name_2`: split into `counterpart_country` (ISO code, nullable) and `border_type` (land / air / sea / internal / multiple). `operational_domain` already covers the domain, so "Air" in this field is redundant.
- `year_of_suspension_termination`: keep only a year or blank. "Ongoing" is already encoded by `operational_status`.
- `installation_cost` and `yearly_maintenance_cost`: split into `amount`, `currency`, `cost_year`, `cost_scope` (unit / contract / programme) and `cost_note`. As free text they cannot be summed or compared.
- `technology_sharing_type` 1–3, `purpose` 1–3: ordered slots with "Not specified" filler. Store as multi-valued (semicolon list or a long table) with no implied ranking, or decide that slot 1 is the primary purpose and say so in the codebook. The sharing-type list also mixes acquisition channel (direct sale, licensing, joint production) with funding (security assistance) and investment (FDI); separate those.
- `funding_source`: overlaps with `technology_sharing_type`; reduce to a short closed list (national budget / foreign government / multilateral or EU / private / mixed / unknown) plus a funder entity field.
- `missing_data_reason`: either make it per field, or replace with a per-field NA code (not disclosed / classified / not searched).
- `border_id`: generate from a rule (ISO3 of deploying country, ISO3 of counterpart or border type, running number) and enforce uniqueness across files.

Drop or rethink:

- `supplier_self_use`. The concept (does the supplier use this technology on its own borders?) is ambiguous when the supplier is a company, is unknown in 116 rows, and coders answered it with sentences. It costs effort and does not yield a usable variable.
- `installation_type` ("New Installation" / "Major Upgradation" / "Both" / "Notsure"). Hard to code reliably from press coverage; "Both" and "Notsure" are 54 rows. Consider a simpler `is_upgrade` yes / no / unknown.
- `personal notes` column (Australia): remove before merging.

Process fixes needed regardless of schema:

- One template, locked dropdowns, no free text in categorical columns. Collapse the slash and spacing variants ("Maritime/Undersea Systems", "Cyber Systems/Automated Border Processing", "Major Up-gradation").
- Re-enter Mexico from the PDF into the template.
- Write the unit-of-analysis rule into the codebook: one row per technology subtype per programme per country, with sites listed in `border_segment`, not one row per site. Then recode Portugal, Indonesia and Chile accordingly.
- Verify a sample of links in the four same-day files.

## 5. Reshaping the LexisNexis text into article × technology × country

The question: is it reasonable to turn the LexisNexis text corpus into a dataset with one row per article × technology × country?

**Verdict: reasonable as an intermediate mention table, not as the analysis dataset.** It is in fact the `mentions` layer that `Proposed_Pipeline_1.0.md` already proposes, aggregated to the document level. The conditions below decide whether it is useful.

Why it cannot be the final unit:

- An article is not a deployment. In the hand-coded data one deployment is supported by 1 to 5 articles (mean 3.2) and one article supports up to 17 rows. In LexisNexis, half of all rows are the same document filed under several countries, 27% are US hearing transcripts and 21% are templated financial briefs. Counting article × tech × country rows measures media attention, weighted toward the US and toward Congress, not technology adoption.
- The country has to come from the text, not from the folder. The folder is the search query; LexisNexis geography tags show the US in 56% of rows regardless of folder, and `central_african_republic` holds 6,656 documents because the query matched "Central African". An article about Thales selling radars to Saudi Arabia involves at least three countries with different roles (deployer, supplier, neighbour), exactly as the hand-coded schema separates `country_name_1`, `country_name_2` and `supplier_country`. So the triple needs a role: article × technology × country × role.
- The technology dimension needs one taxonomy. The hand-coded `Lists` sheet has 6 types and about 35 subtypes; the keyword list in `Border_Tech_Keywords_Short.md` has 39 term groups at a different granularity. Unless the keyword groups are mapped onto the subtype taxonomy, the text dataset and the hand-coded dataset cannot be joined.
- Keyword matching yields mentions, not events. The short keyword list reaches about 50% recall and 75% precision on tagged articles. A row "article mentions biometrics and Kenya" says nothing about whether Kenya deployed biometrics. Each row needs a relation label (deployment / procurement / plan / policy / incidental mention) and an evidence span, which is a classification step, not a reshape.
- No link-level join to the hand-coded data is possible. The hand-coded sources are open-web pages, not LexisNexis documents. The two datasets meet only at the level of (country, technology subtype, year).

Recommended structure:

1. `documents`: one row per unique `ResultId`, with the LexisNexis index block stripped and kept as weak labels; drop or flag templated sources.
2. `doc_country`: many-to-many, from geography tags plus entity extraction, with `role` (deployer / supplier / counterpart / other) and `method` (tag / NER / folder).
3. `doc_tech`: many-to-many, with technology subtype from the shared taxonomy, evidence span and confidence.
4. The article × technology × country table is then a join of 2 and 3, filtered to rows where a technology mention and a country mention co-occur in the same chunk.
5. Aggregate to country × technology × year for analysis, and use the 389 hand-coded deployments as the validation set: for each hand-coded (country, subtype, year ± 1), does the text pipeline produce at least one supporting document? That number is the recall of the text approach, and the cases it misses tell you which sources LexisNexis does not cover.

Done this way, the reshape is not only reasonable but necessary. Done as a flat keyword-count table with country taken from the folder, it will reproduce the US-centric noise of the current corpus and will not be comparable with the hand-coded data.
