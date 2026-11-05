# Border Tech Texts: Data Inventory Report

Folder: `/Users/yuxin/Dropbox/Border Tech Texts`  
Prepared: 28 October 2026. Read-only inspection; no files in the folder were modified.

## 1. What the data is

A LexisNexis full-text corpus on border technology, exported in two batches (27 and 30 April 2026) and organized by country and year. Each row is one LexisNexis document (news article, transcript, government document, industry brief, or press release) with its full text and metadata.

| Item | Value |
|---|---|
| Archives | 10 zip files (7 from 27 Apr, 3 from 30 Apr 2026) |
| Size | 7.08 GB compressed, 21.5 GB uncompressed |
| Files inside | 5,217 CSV files, one identical 16-column schema |
| Country / region folders | 168 (167 countries and territories + `south_africa_airports`) |
| Year coverage | 1990 – 2025 |
| Document rows (country × document) | 65,618 |
| Unique documents (by `ResultId`) | 32,812 |
| Total words of full text | 1.15 billion |
| Words per document (10th pct / median / 90th pct) | 392 / 6,194 / 40,783 |
| Language | English only in practice (`Language` column is blank in every row) |

**Columns**: `Country, ResultId, Title, Date, Language, Source, WordLength, Overview, Snippet, FullText, Byline, Section, Location, Jurisdiction, WebNewsUrl, MediaReadLink`. `FullText` ends with LexisNexis index metadata (subject, industry and geography codes, copyright line, retrieval timestamp), which should be stripped before text analysis.

## 2. File organisation

| Pattern | Files | Meaning |
|---|---|---|
| `<country>_1990-2025.csv` | 168 | One combined file per country (all years). 163 countries have one; usa, south_africa, south_korea, central_african_republic and south_africa_airports have per-year files only. |
| `<country>/<country>_<year>_all.csv` | 2,549 | One file per country-year, all languages. |
| `<country>/<country>_<year>_english.csv` | 2,500 | Same query restricted to English. In 1,686 of 1,994 pairs the `_all` and `_english` files are byte-identical in size; the rest differ by a handful of rows. |

The combined file is the concatenation of that country's per-year files, so the per-year and combined layouts hold the same documents. Per-year files exist only for years with hits (median 14 year-files per country).

## 3. Countries

Coverage is extremely uneven. The ten largest folders hold 63% of all rows.

| Documents per country | Countries |
|---|---|
| ≥ 2,000 | 7 |
| 500 – 1,999 | 21 |
| 100 – 499 | 37 |
| 10 – 99 | 69 |
| < 10 | 34 |

| Rank | Country folder | Documents |
|---|---|---|
| 1 | usa | 8,067 |
| 2 | central_african_republic | 6,656 |
| 3 | south_korea | 6,346 |
| 4 | hong_kong | 5,133 |
| 5 | uk | 3,916 |
| 6 | south_africa | 3,485 |
| 7 | north_korea | 3,334 |
| 8 | israel | 1,665 |
| 9 | macao | 1,456 |
| 10 | malaysia | 1,219 |
| 11 | sri_lanka | 1,099 |
| 12 | canada | 1,084 |
| 13 | philippines | 1,061 |
| 14 | australia | 1,031 |
| 15 | costa_rica | 780 |

The country folder reflects the search query, not necessarily the article's subject. LexisNexis geography tags show the United States in 56% of rows, China in 20%, the United Kingdom in 14%, so the corpus is US-centric regardless of folder.

Folders that look inflated by loose query matching and deserve a spot check: central_african_republic (6,656), vatican (571), micronesia (376), western_sahara (335), saint_vincent (264).

The full per-country table is in the appendix.

## 4. Years

| Period | Unique documents | Country × document rows |
|---|---|---|
| 1990–1994 | 147 | 349 |
| 1995–1999 | 568 | 1,449 |
| 2000–2004 | 2,892 | 5,490 |
| 2005–2009 | 6,770 | 11,683 |
| 2010–2014 | 4,882 | 9,899 |
| 2015–2019 | 7,245 | 16,268 |
| 2020–2025 | 10,308 | 20,480 |

Volume is thin before 2001, rises sharply after 2001 and again after 2016, and peaks in 2020 (2,013 unique documents, 4,170 rows). 2025 is a partial year (export date April 2026, but documents dated through December 2025 are present).

## 5. Topics

Topics below are LexisNexis subject index terms attached to each document, counted over the 65,618 country × document rows (a document carries many terms, so columns do not sum to 100%). The generic tag NEGATIVE NEWS is the most frequent (26,757 rows) and is not listed.

**Border control, customs & immigration**

| Subject term | Rows | Share |
|---|---|---|
| Border Control | 14,912 | 23% |
| Territorial & National Borders | 12,382 | 19% |
| Immigration | 8,408 | 13% |
| Excise & Customs | 7,580 | 12% |
| Passports & Visas | 4,864 | 7% |
| Smuggling | 4,743 | 7% |
| Illegal Immigrants | 3,853 | 6% |
| Refugees | 2,062 | 3% |

**Security, terrorism & defense**

| Subject term | Rows | Share |
|---|---|---|
| National Security | 16,722 | 25% |
| Terrorism & Counterterrorism | 12,825 | 20% |
| Weapons & Arms | 9,516 | 15% |
| Special Investigative Forces | 9,440 | 14% |
| Terrorist Attacks | 5,369 | 8% |
| Armies | 5,084 | 8% |
| Defense & Military Policy | 4,753 | 7% |
| Defense Industry | 3,846 | 6% |

**Surveillance & border technology**

| Subject term | Rows | Share |
|---|---|---|
| Surveillance | 6,664 | 10% |
| Biometrics | 5,157 | 8% |
| Surveillance Technology | 3,234 | 5% |
| Computer Software | 2,486 | 4% |
| Unmanned Aircraft | 2,242 | 3% |
| Defense Electronics | 2,061 | 3% |
| Information Security & Privacy | 1,784 | 3% |
| Military Surveillance | 1,702 | 3% |

**Crime, policing & drugs**

| Subject term | Rows | Share |
|---|---|---|
| Crime, Law Enforcement & Corrections | 10,473 | 16% |
| Controlled Substances Crime | 3,591 | 5% |
| Arrests | 3,502 | 5% |
| Drug Trafficking | 2,837 | 4% |
| Narcotics | 1,481 | 2% |
| Organized Crime | 1,109 | 2% |
| Money Laundering | 539 | 1% |

**Aviation, ports & travel**

| Subject term | Rows | Share |
|---|---|---|
| Aircraft | 5,296 | 8% |
| Traveler Safety & Security | 2,947 | 4% |
| Aviation Security | 2,447 | 4% |
| Harbors & Ports | 1,515 | 2% |

**Public health / COVID-19**

| Subject term | Rows | Share |
|---|---|---|
| COVID Coronavirus | 4,381 | 7% |
| COVID-19 Coronavirus | 4,284 | 7% |
| Infectious Disease | 3,591 | 5% |
| Epidemics | 2,064 | 3% |
| Pandemics | 1,384 | 2% |

**Politics, government & legislation**

| Subject term | Rows | Share |
|---|---|---|
| Government Advisors & Ministers | 8,508 | 13% |
| US Congress | 6,880 | 10% |
| US Republican Party | 4,980 | 8% |
| Prime Ministers | 4,674 | 7% |
| US Democratic Party | 4,424 | 7% |
| Public Policy | 4,116 | 6% |
| Elections & Politics | 3,525 | 5% |
| Legislation | 3,053 | 5% |

**International relations & EU**

| Subject term | Rows | Share |
|---|---|---|
| International Relations | 7,239 | 11% |
| Agreements | 6,736 | 10% |
| European Union Member States | 5,879 | 9% |
| European Union | 5,259 | 8% |
| United Nations | 3,802 | 6% |
| Foreign Relations | 3,327 | 5% |

**Economy & trade**

| Subject term | Rows | Share |
|---|---|---|
| Economy & Economic Indicators | 4,631 | 7% |
| Budgets | 4,080 | 6% |
| Business News | 3,506 | 5% |
| Manufacturing | 3,340 | 5% |
| International Trade | 2,448 | 4% |

Reading: the corpus is framed around border control and national security. Technology-specific terms (surveillance, biometrics, drones, identification technologies, AI, RFID, radar, scanners) each appear in only 1 to 10% of rows, so most documents discuss borders, migration, terrorism or customs with technology as one strand rather than the main subject. A COVID-19 cluster (2020 – 2022) is substantial.

## 6. Sources and document types

1,456 distinct sources. Grouped by source name (approximate):

| Source category | Rows | Share of rows | Unique documents |
|---|---|---|---|
| News media (newspapers, broadcasters, agencies, monitoring) | 28,725 | 44% | 16,679 |
| US government transcripts & documents | 17,425 | 27% | 8,891 |
| Industry / financial briefs & databases | 13,699 | 21% | 4,473 |
| Press releases / newswires | 2,960 | 5% | 1,889 |
| Blogs / aggregators | 2,809 | 4% | 880 |

| Top sources | Rows |
|---|---|
| Industry SnapShot | 5,975 |
| Briefing.com | 4,134 |
| VIQ Political Wire | 2,952 |
| Federal News Service | 2,865 |
| CQ Congressional Testimony | 2,328 |
| Gates of Vienna | 2,318 |
| CQ Transcriptions | 2,309 |
| States News Service | 1,796 |
| CountryWatch Reviews | 1,775 |
| Congressional Documents and Publications (Federal Information & News Dispatch, Inc.) | 1,456 |
| Targeted News Service | 1,312 |
| Impact News Service | 1,244 |

Notes: US congressional hearing testimony and transcripts (Federal News Service, CQ, States News Service, VIQ Political Wire) are a large block. Industry SnapShot, Briefing.com, CountryWatch and similar financial or country-risk briefs are templated reports rather than journalism and are the main reason some documents run to tens of thousands of words. Gates of Vienna and Newstex are blog aggregators. The `Section` column is blank in 64% of rows.

## 7. Duplicates and redundancy

| Kind of duplication | Count |
|---|---|
| Rows that repeat a document already present under another country | 32,806 of 65,618 rows (50%) |
| Unique documents appearing in 2 or more country folders | 14,542 of 32,812 (44%) |
| … in exactly 1 / 2 / 3 / 4 / 5+ folders | 18,270 / 7,383 / 3,210 / 1,801 / 2,148 |
| Most folders a single document appears in | 41 |
| Duplicate rows inside one country folder | 501 (all in central_african_republic); none elsewhere |
| Rows with `WordLength` = 0 but text present | 4,371 |
| Rows with empty `FullText` | 25 |
| File paths present in both download batches | 189 (France, Germany, Greece, Italy, Poland, Spain) |

**Structural redundancy.** Every document is stored up to four times: in the combined file and the per-year file, each in an `_all` and an `_english` version. The unique content is therefore roughly a quarter of the 21.5 GB on disk.

**Cross-batch consistency.** For France, Italy, Poland, Spain and Germany the 30 April batch contains the same documents as the 27 April batch (identical or a subset, e.g. France 528 of 644, Italy 445 of 576); file sizes differ only because of the retrieval timestamp inside `FullText`. Greece is different: the 27 April per-year files hold 893 documents covering 1990 – 2013, the 30 April files hold 386 (combined file 602) covering 1995 – 2025, and only about 100 documents are shared. The Greece query was evidently changed between runs, and one version should be chosen deliberately.

## 8. Practical recommendations

- Work from one layout only (the combined files, or the per-year `_all` files) and ignore `_english`.
- De-duplicate on `ResultId` for corpus-level counts; keep the country assignment as a separate many-to-many table.
- Decide whether to keep financial briefs (Industry SnapShot, Briefing.com, CountryWatch) and blog aggregators; together they are about a quarter of rows.
- Strip the LexisNexis index block from the end of `FullText` before any text analysis.
- Resolve the two Greece versions, and spot-check the inflated small-country folders listed in section 3.

## Appendix: documents per country folder (unique within folder)

| Country | Docs | Country | Docs | Country | Docs | Country | Docs |
|---|---|---|---|---|---|---|---|
| usa | 8,067 | new_zealand | 220 | cambodia | 41 | slovenia | 12 |
| central_african_republic | 6,656 | egypt | 220 | bulgaria | 40 | guyana | 11 |
| south_korea | 6,346 | cape_verde | 215 | austria | 40 | haiti | 11 |
| hong_kong | 5,133 | colombia | 200 | spain | 38 | ethiopia | 11 |
| uk | 3,916 | guinea_bissau | 192 | iceland | 37 | belize | 10 |
| south_africa | 3,485 | ukraine | 181 | belarus | 37 | bahrain | 10 |
| north_korea | 3,334 | lebanon | 171 | niger | 36 | serbia | 10 |
| israel | 1,665 | equatorial_guinea | 169 | mozambique | 36 | luxembourg | 10 |
| macao | 1,456 | oman | 148 | morocco | 34 | mauritius | 9 |
| malaysia | 1,219 | finland | 146 | chile | 33 | north_macedonia | 9 |
| sri_lanka | 1,099 | libya | 141 | fiji | 32 | mauritania | 9 |
| canada | 1,084 | lithuania | 138 | romania | 32 | brunei | 9 |
| philippines | 1,061 | azerbaijan | 131 | seychelles | 29 | benin | 8 |
| australia | 1,031 | indonesia | 131 | jamaica | 28 | namibia | 8 |
| costa_rica | 780 | saint_lucia | 129 | denmark | 27 | eritrea | 7 |
| india | 776 | armenia | 126 | tunisia | 27 | zambia | 6 |
| afghanistan | 719 | cuba | 125 | myanmar | 27 | laos | 6 |
| palestine | 658 | poland | 124 | cameroon | 25 | mali | 6 |
| france | 644 | norway | 114 | peru | 24 | barbados | 5 |
| papua_new_guinea | 629 | portugal | 113 | chad | 21 | paraguay | 5 |
| taiwan | 619 | nicaragua | 110 | venezuela | 21 | marshall_islands | 5 |
| greece | 602 | kosovo | 107 | lesotho | 20 | honduras | 4 |
| italy | 576 | saint_kitts_nevis | 105 | qatar | 19 | bosnia | 4 |
| vatican | 571 | uganda | 96 | mongolia | 19 | dominica | 4 |
| south_sudan | 545 | hungary | 89 | algeria | 18 | suriname | 3 |
| singapore | 539 | estonia | 88 | tajikistan | 17 | slovakia | 3 |
| japan | 514 | panama | 78 | madagascar | 16 | ivory_coast | 2 |
| iraq | 511 | malta | 77 | georgia | 16 | eswatini | 2 |
| sierra_leone | 484 | djibouti | 77 | kazakhstan | 16 | el_salvador | 2 |
| south_africa_airports | 478 | turkey | 70 | argentina | 16 | czech_republic | 2 |
| china | 467 | nepal | 68 | samoa | 16 | senegal | 2 |
| congo_republic | 465 | dominican_republic | 65 | germany | 16 | vanuatu | 2 |
| netherlands | 430 | croatia | 63 | tanzania | 15 | uruguay | 2 |
| micronesia | 376 | drc | 61 | botswana | 15 | timor_leste | 2 |
| iran | 344 | kenya | 61 | sudan | 15 | andorra | 1 |
| western_sahara | 335 | liberia | 61 | bhutan | 14 | uzbekistan | 1 |
| ireland | 283 | ghana | 60 | kuwait | 14 | gambia | 1 |
| pakistan | 276 | maldives | 57 | ecuador | 14 | angola | 1 |
| bangladesh | 264 | jordan | 55 | thailand | 14 | albania | 1 |
| saint_vincent | 264 | sao_tome_principe | 53 | moldova | 13 | kyrgyzstan | 1 |
| somalia | 255 | rwanda | 47 | latvia | 13 | grenada | 1 |
| mexico | 223 | guatemala | 44 | cyprus | 12 | kiribati | 1 |
