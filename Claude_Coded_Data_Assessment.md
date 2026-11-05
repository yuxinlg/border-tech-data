# Claude-coded Border Tech Data: Field Inventory and Assessment

Folder: `/Users/yuxin/Dropbox/Border Tech Fall 2026/Claude-coded Data`
Prepared: 5 November 2026. Read-only inspection; no files were modified.
Companion documents: `Hand_Coded_Data_Assessment.md` (student-coded batch), `Border_Tech_Texts_Data_Report.md` (LexisNexis corpus), `Proposed_Pipeline_1.0.md`.

## 1. What the data is

Fifteen Excel workbooks, one per country, produced by an LLM (Claude) filling the same deployment template that the student coders use. Each workbook has a `Data Entry Sheet` and, in 14 of 15, a `Summary` sheet with country context. The files were Dropbox online-only placeholders until this session; file modification dates are 13 October 2026.

| Item | Value |
|---|---|
| Files | 15 xlsx (Venezuela has no Summary sheet; Israel file is marked `-3`, "v3, credibility-upgraded") |
| Rows | 130 |
| Countries | 15: Colombia, Finland, Iran, Israel, Jordan, Kazakhstan, North Korea, South Korea, Tunisia, Turkmenistan, UAE, Uruguay, Uzbekistan, Venezuela, Vietnam |
| Rows per country | 2 (Turkmenistan) to 23 (Israel); median 8 |
| Unit of a row | One technology deployment: country × border segment × technology subtype, same as the hand-coded batch |
| Sources | 384 http links, 327 unique; none from LexisNexis |
| `coding_date` | 2025-05-07 in every row that has one; 41 source labels are dated 2026, so this date is a placeholder, not the production date |
| `coder_id` | `CDN_<ISO3>_01`, one per country |

**Same batch as four files in the hand-coded folder.** Brazil, Kenya, South Africa and Thailand in `Hand-coded Data So Far` carry the identical signature (coder ID `CDN_BRA_01` etc., coding date 2025-05-07, no `Lists` sheet, prose-filled cells). They belong to this LLM batch, not to the student batch. Counting them here, the LLM batch is 19 countries and 188 rows, and the genuinely hand-coded batch is 15 countries and 319 rows plus Mexico.

**Links were not verified.** A sample check of 40 URLs was attempted but the network command was not permitted in this session. Whether the cited pages exist and say what the cells claim remains open.

## 2. Fields

Three template variants:

| Variant | Files | Columns | Difference from the hand-coded v2 template |
|---|---|---|---|
| v2, identical to hand-coded | Finland, Iran, Israel, Jordan, Kazakhstan, North Korea, South Korea, Tunisia, Turkmenistan, UAE, Uzbekistan | 40 | none |
| No cost columns; `checking_date` and `notes` instead of `coding_date` and `coder_id` | Colombia, Uruguay, Venezuela | 38 | `checking_date` and `notes` are empty in every row |
| No cost columns, no coding metadata | Vietnam | 36 | |

The field groups are the same as in the hand-coded assessment: identity and place, technology, operator, timing and status, money, supplier, purpose, evidence (5 sources with links), coding metadata.

The `Summary` sheet holds, per country: borders covered with lengths, key agencies, key programmes by border, technology types covered, key suppliers, primary purposes, security context, a "Sourcing Methodology Note", and in some files "Recency and Uncertainty Flags" or "Human Rights and Legal Concerns". It is a narrative codebook-style appendix, not structured data.

## 3. A column-shift defect affects half the rows

In 67 of 130 rows the values for `missing_data_reason`, `coding_date` and `coder_id` sit in the wrong columns. When a row has fewer than five sources, the writer did not pad the empty source slots, so the trailing values slid left: the coding date appears in `link_source5`, the coder ID in `missing_data_reason`, and so on.

| File | Rows | Shifted |
|---|---|---|
| South Korea | 9 | 8 |
| Uzbekistan | 8 | 7 |
| UAE | 9 | 7 |
| Vietnam | 10 | 6 |
| Iran | 7 | 5 |
| Kazakhstan | 7 | 5 |
| Tunisia | 7 | 5 |
| Israel | 23 | 12 |
| Finland | 6 | 4 |
| Jordan | 10 | 4 |
| North Korea | 5 | 2 |
| Turkmenistan | 2 | 2 |
| Colombia, Uruguay, Venezuela | 27 | 0 |

The shift is mechanical and can be repaired by rule: for each row, keep the (source, link) pairs whose link starts with `http`, then reassign the remaining trailing cells to `missing_data_reason`, `coding_date`, `coder_id` in order. Until that is done, any column-wise read of these three fields is wrong, and so are the raw fill rates reported by a naive script (for example `coder_id` shows 98 blanks, of which 61 are shifted values and 37 are files without the column).

## 4. Fill rates and value quality

Counts below are after reading the shifted rows as written, so the three metadata fields are understated.

| Field | Blank | NA-token | Filled (of 130) | Note |
|---|---|---|---|---|
| technology_type | 0 | 0 | 130 | 5 values, spelled consistently (slash variants) |
| technology_subtype | 0 | 0 | 130 | 24 values, all on the `Lists` vocabulary; 2 "Other" |
| technology_subtype_reported | 0 | 0 | 130 | Median 33 words; no verbatim quotes |
| technology_detailed | 0 | 0 | 130 | Median 1,230 characters; 104 use attribution verbs ("reported that"); 1 contains a quoted span |
| force_structure | 0 | 0 | 130 | 25 distinct values; 58 rows multi-valued ("Army, Border Guards") |
| year_of_adoption | 0 | 0 | 130 | 129 are free text with parentheses or ranges |
| year_of_installation | 0 | 0 | 130 | 129 are free text |
| installation_type | 0 | 0 | 130 | Only "New Installation" (74) and "Both" (56); no "Major Upgradation" |
| operational_status | 0 | 0 | 130 | 111 Operational, 13 Under Construction, 4 Proposed, 2 Suspended |
| year_of_suspension_termination | 0 | 0 | 130 | 128 are "Ongoing": a default, not an observation |
| installation_cost | 37 | 39 | 54 | 93 filled cells; 33 contain a number, 67 say "not disclosed" in prose |
| yearly_maintenance_cost | 37 | 93 | 0 | No row has a value |
| funding_source | 0 | 0 | 130 | 104 distinct strings for 130 rows; 126 carry a parenthetical agency name |
| supplier_country | 0 | 7 | 123 | 38 multi-valued |
| supplier_self_use | 0 | 12 | 118 | Yes 88 / No 30 / Unknown 12; asserted, not sourced |
| supplier_company | 0 | 0 | 130 | 126 multi-valued with role annotations; many cells say "specific supplier not named in the sources reviewed" |
| technology_sharing_type | 0 | 11 | 119 | 7 values, on list; slot 2 is "None" in 108 rows |
| purpose | 0 | 0 | 130 | Mostly on list; "Insurgency" and "Environmental Monitoring" appear |
| link_source1 | 0 | 0 | 130 | 29 rows have one link only |
| missing_data_reason | 0 | 0 | 130 | Median 10 characters because of the shift; the real text runs to 578 characters |

Other checks:

- `border_id` is unique and follows `ISO3-ISO3-###` or `ISO3-INT-###` / `ISO3-ATL-###` consistently.
- `country_name_2` is a sentence in many rows: "Regional (Persian Gulf and Strait of Hormuz maritime approaches, adjoining UAE, Oman, Saudi Arabia, Qatar, Bahrain, Kuwait, and Iraq)", "Multiple (all Iranian citizens aged 15 and older; cross-referenced at all border crossings)".
- Source links fan out little: 281 links support one row, 35 support two, 11 support three. Only 3 rows share an identical link set with another row. This is healthier than the hand-coded batch, where one article supports up to 17 rows.
- Source domains are news and defence trade press (Times of Israel, GlobalSecurity, Biometric Update, Al Jazeera, Army Recognition, VietnamPlus); 17 links are government or official sites; 5 are Wikipedia.
- Source years cluster in 2021 to 2026 (231 of 292 dated labels), so the batch describes recent systems and thins out before 2015.

## 5. Field-by-field verdict

What this batch does better than the student batch:

- Categorical fields are clean. Technology type, subtype, domain, status and sharing type stay on the vocabulary, with no spelling drift, no trailing spaces and no type-level values in the subtype column.
- IDs are unique and systematic.
- Every row has a `missing_data_reason` that names what could not be found.
- Sources are more diverse per row and less recycled across rows.

What it does worse:

- **The evidence fields are paraphrase, not quotation.** `technology_detailed` is a 1,200-character narrative that attributes claims ("The Defense Post, a specialist defense-industry news outlet, reported that...") but quotes almost nothing. `technology_subtype_reported` is a 33-word summary, not the reported phrase. The student batch's quotes can be located in the source page; these cannot. For the pipeline, which needs evidence spans tied to a document, this batch gives none.
- **Apparent completeness is manufactured.** Nearly every cell is filled because the model writes "Not publicly disclosed (no cost figures identified in any source reviewed...)" instead of leaving a blank. The same NA-reason appears inside `supplier_company`, `installation_cost` and `funding_source`, so value and missingness are mixed in one cell. Real fill rates: cost 33 numeric of 130, maintenance 0 of 130.
- **Defaults stand in for observations.** `year_of_suspension_termination` is "Ongoing" in 128 rows; `installation_type` is "Both" in 56 rows; `supplier_self_use` is answered Yes or No in 118 rows with no source for the answer. These look like fields the model filled to avoid blanks rather than coded.
- **Years are unusable as numbers.** 129 of 130 adoption years and 129 of 130 installation years contain prose ("2008 onward (SICTVM first generation); 2012 (11-radar expansion announcement)"). The student batch had this in 59 and 81 rows of 377.
- **Scope creep.** 40 rows are coded against "Multiple" or `INT` rather than a border. 32 rows describe national ID databases, civil-registry AFIS, city CCTV networks (Bogotá C4), or nationwide population biometrics (Iran NOCR, Israel's biometric database) whose border relevance is indirect. The model stretched "border technology" to anything identity- or surveillance-related. The codebook needs a scope rule, and these rows need a flag.
- **Self-justifying text inside data cells.** Cells contain hedges and explanations ("compare PRK-CHN-002 for the separately documented Chinese-sourced camera component", "this figure covers one purchase and should not be read as the total nationwide programme cost"). The Turkmenistan Summary has a section titled "WHY THIS DATABASE IS SO MUCH SMALLER THAN OTHERS IN THIS SERIES". This is useful commentary but it has to live in a notes column, not in the value.
- **Multi-valued free text.** `force_structure` (58 rows), `supplier_country` (38), `supplier_company` (126) and `funding_source` (98) hold lists with role annotations in parentheses. Each needs either a long table or a controlled primary value plus a note.
- **The coding date is fictional.** Every row says 2025-05-07, but 41 cited sources are from 2026 and the files are dated October 2026.

Same structural issues as the student batch, unchanged: `country_name_2` overloaded; `technology_sharing_type` mixes acquisition channel with funding; ordered purpose slots; row-level `missing_data_reason`; template variants across files.

## 6. How this batch fits the pipeline

Treat these 130 rows (188 with the four misfiled countries) as **Phase A output: LLM bootstrap labels awaiting human verification**, which is exactly the role `Proposed_Pipeline_1.0.md` assigns to LLM output. They are not a gold set and not mergeable with the student batch as equals.

- As a candidate list they are valuable. Each row is a hypothesis with 1 to 5 links to check, and the model's `missing_data_reason` already says what the verifier should look for.
- As training or evaluation data for extraction they are not usable until each row is tied to an actual source passage, because the evidence fields are paraphrase.
- As a merge partner for the student data they need a `provenance` column (`llm` vs `human`) and a `verified` column (unverified / confirmed / corrected / rejected) before a single table makes sense.

Steps, in order:

1. Repair the column shift with the rule in section 3, and move the four misfiled countries from the hand-coded folder into this batch.
2. Add `provenance` = llm and `verified` = unverified to every row; convert `coding_date` to the file date and keep the model's date in a note.
3. Check that every link resolves, and for a sample of about 30 rows have a student read source 1 and confirm or correct subtype, year, supplier and status. The correction rate decides whether the rest is worth verifying row by row or should be regenerated with a stricter prompt.
4. Apply a scope filter: keep rows with a named border, crossing, airport, port or coastline; flag national-ID and domestic-surveillance rows as out of scope or as a separate category.
5. Normalise years to integers plus a note; split multi-valued cells; strip NA-reason prose out of value cells into `missing_data_reason`.
6. If the batch is regenerated, change the prompt so that `technology_subtype_reported` and `technology_detailed` must be verbatim quotes with the source number, every source slot is written even when empty, and unknowns are left blank rather than explained.
