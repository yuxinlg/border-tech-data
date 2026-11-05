# Border Tech Texts: English Keyword List

Prepared: 3 November 2026. Companion to `Border_Tech_Texts_Data_Report.md` (corpus inventory) and `Proposed_Pipeline_1.0.md` (section 2.4, query taxonomy).

## How this list was built

Two sources of evidence, both from the existing LexisNexis corpus:

1. **LexisNexis subject index terms** attached to each document, counted over all 65,618 country × document rows in the inventory report. Column "Tag rows" below. A document carries many tags, so shares do not sum to 100%.
2. **Full-text check** on a sample of 9,845 unique documents read directly from 12 combined country files (uk 3,915; israel 1,425; canada 988; australia 889; italy 470; japan 442; greece 377; china 343; singapore 319; pakistan 244; france 228; netherlands 205). The LexisNexis index block at the end of each `FullText` was stripped first so that tags do not count as text. Column "Sample docs" is the share of those 9,845 documents whose body text contains the keyword or one of its listed variants.

Read the two columns together: a high tag count with a low text share means LexisNexis indexes the concept more often than articles name it; a high text share with no tag means the term is in common use but has no index term of its own. The sample is UK- and Israel-heavy and contains no US per-year files, so US-only programme names (US-VISIT, SBInet, Secure Flight) are under-counted here relative to the full corpus.

Keywords are given in the form found in the texts. Variants in parentheses are spellings and synonyms that should be searched together.

## 1. Border control and migration (framing terms)

These define the domain. Technology keywords should be combined with at least one of these in any search.

| Keyword (variants) | Tag rows (share) | Sample docs |
|---|---|---|
| border control (border controls, border check, border security, border protection, border enforcement, border management) | BORDER CONTROL 14,912 (23%) | 61% |
| national border / territorial border (border crossing, border post, port of entry, checkpoint) | TERRITORIAL & NATIONAL BORDERS 12,382 (19%) | – |
| immigration (immigration control, immigration enforcement) | IMMIGRATION 8,408 (13%) | – |
| customs (excise, customs clearance, customs inspection) | EXCISE & CUSTOMS 7,580 (12%) | – |
| passport / visa (travel document) | PASSPORTS & VISAS 4,864 (7%) | – |
| smuggling (people smuggling, drug smuggling, contraband) | SMUGGLING 4,743 (7%) | – |
| illegal immigration (irregular migration, undocumented, unauthorised entry) | ILLEGAL IMMIGRANTS 3,853 (6%) | – |
| refugees / asylum (asylum seeker) | REFUGEES 2,062 (3%) | – |
| human trafficking | HUMAN TRAFFICKING 960 (1%) | – |
| deportation (removal) | DEPORTATION 594 (1%) | – |
| national security / counter-terrorism | NATIONAL SECURITY 16,722 (25%); TERRORISM & COUNTERTERRORISM 12,825 (20%) | – |
| aviation security / traveller security | AVIATION SECURITY 2,447 (4%); TRAVELER SAFETY & SECURITY 2,947 (4%) | – |
| ports and harbours (seaport, maritime border) | HARBORS & PORTS 1,515 (2%) | – |
| drug trafficking / narcotics | DRUG TRAFFICKING 2,837 (4%); NARCOTICS 1,481 (2%) | – |

## 2. Biometrics and identity documents

| Keyword (variants) | Tag rows (share) | Sample docs |
|---|---|---|
| biometric / biometrics (biometric data, biometric identification, multimodal biometric) | BIOMETRICS 5,157 (8%); IDENTIFICATION TECHNOLOGIES 1,655 (3%) | 29% |
| fingerprint (fingerprinting, fingerprint scanner, fingerprint identification) | FINGERPRINTING 1,394 (2%) | 13% |
| facial recognition (face recognition, facial biometrics) | PATTERN RECOGNITION 1,644 (3%) | 13% |
| iris scan (iris recognition) | – | 4% |
| voice recognition (voiceprint, speaker recognition) | – | 2% |
| DNA testing (DNA sampling, DNA database) | – | 2% |
| identity verification (identity check, identity management, background check) | – | 10% |
| national ID card (identity card, ID card, national ID) | – | 7% |
| digital identity (digital ID, e-ID) | – | 5% |
| smart card (chip card) | COMPUTER CHIPS 571 (1%) | 4% |
| e-passport (biometric passport, electronic passport, chip passport) | – | 9% |
| machine-readable passport (machine-readable travel document, MRTD, MRZ) | – | 0.5% |
| passport reader / document reader (document scanner, document authentication, document verification, forged document, document fraud) | – | 4% |
| e-visa (electronic visa, online visa, visa on arrival) | – | 1% |
| visa waiver (ESTA) | – | 3% |
| electronic travel authorisation (eTA, ETA) | – | 3% |

## 3. Automated border crossing and traveller programmes

| Keyword (variants) | Tag rows (share) | Sample docs |
|---|---|---|
| e-gate (eGate, automated gate, automatic gate, smart gate, SmartGate, automated border control, ABC gate, automated passport control, biometric gate, self-service gate) | – | 11% |
| kiosk (self-service kiosk, automated passport control kiosk) | – | 6% |
| trusted traveller programme (registered traveller, Global Entry, NEXUS, SENTRI, Privium, frequent traveller) | – | 6% |
| entry-exit system (entry/exit, biometric exit, exit control) | – | 4% |

## 4. Data systems, screening lists and named programmes

| Keyword (variants) | Tag rows (share) | Sample docs |
|---|---|---|
| database (shared database, central database) | – | 16% |
| information sharing (data sharing, interoperability, data exchange) | – | 18% |
| border management system (border management information system, integrated border management, border control system, immigration management system, customs management system, e-customs, single window, ASYCUDA) | – | 10% |
| watch list (watchlist, no-fly list, terrorist screening database) | – | 7% |
| advance passenger information (API, advance passenger processing, passenger data) | – | 2% |
| passenger name record (PNR) | – | 1% |
| Automated Targeting System (targeting centre) | – | 2% |
| US-VISIT | – | 1% |
| IDENT | – | 1% |
| Secure Flight (CAPPS) | – | 1% |
| E-Verify / SEVIS | – | 1% |
| Frontex | – | 6% |
| Smart Borders package / eu-LISA | – | 3% |
| EU Entry/Exit System (EES) | – | 2% |
| Eurosur | – | 1% |
| ETIAS | – | 1% |
| Schengen Information System (SIS, SIS II) | – | 1% |
| Eurodac | – | 0.4% |
| Visa Information System (VIS) | – | 0.3% |
| SIVE (Spain) | – | 0% |
| PISCES / MIDAS (IOM) | – | 0.1% |
| Securiport | – | 0.1% |

The named EU, US and IOM systems are rare in the existing corpus because the original queries were country-name based. They are the terms most likely to add new documents if searched directly.

## 5. Surveillance and detection hardware

| Keyword (variants) | Tag rows (share) | Sample docs |
|---|---|---|
| surveillance (generic) | SURVEILLANCE 6,664 (10%); SURVEILLANCE TECHNOLOGY 3,234 (5%); MILITARY SURVEILLANCE 1,702 (3%) | 45% |
| border surveillance (border monitoring) | – | 7% |
| maritime surveillance (coastal surveillance, maritime domain awareness, maritime security) | – | 17% |
| aerial surveillance (air surveillance, airborne surveillance) | SURVEILLANCE & RECONNAISSANCE AIRCRAFT 980 (1%) | 6% |
| CCTV (closed-circuit television, surveillance camera, security camera, video surveillance, camera) | CAMERAS 1,635 (2%) | 40% |
| drone (UAV, UAS, unmanned aerial vehicle, unmanned aircraft, remotely piloted aircraft) | UNMANNED AIRCRAFT 2,242 (3%); UNMANNED MILITARY AIRCRAFT 1,737 (3%) | 28% |
| Predator / Reaper (MQ-9, Global Hawk, Heron, Hermes 450/900) | – | 6% |
| helicopter / patrol aircraft (surveillance aircraft, P-3 Orion) | AIRCRAFT 5,296 (8%) | 24% |
| aerostat (blimp, tethered balloon, surveillance balloon) | – | 2% |
| radar (coastal radar, ground radar, ground-penetrating radar) | RADAR SYSTEMS 996 (2%) | 19% |
| satellite (satellite imagery, satellite surveillance) | SATELLITE INDUSTRY 512 (1%) | 20% |
| sensor (generic) | – | 22% |
| ground sensor (motion sensor, motion detector, seismic sensor, unattended ground sensor, buried sensor) | – | 3% |
| thermal imaging (thermal camera, infrared, night vision, heat-sensing) | – | 14% |
| surveillance tower (watchtower, integrated fixed tower, remote video surveillance, mobile surveillance system, autonomous surveillance tower) | – | 3% |
| virtual fence (smart wall, smart fence, SBInet, Secure Border Initiative, electronic fence, technological barrier) | – | 2% |
| smart border (e-border, e-Borders, intelligent border) | – | 8% |
| border wall / border fence (security barrier, separation barrier, razor wire) | – | 5% |
| licence plate reader (license plate recognition, automatic number plate recognition, ANPR, ALPR) | – | 4% |
| tunnel detection (ground-penetrating radar, underground sensor) | – | 0.4% |
| patrol boat / vessel tracking (automatic identification system, patrol vessel) | – | 15% |
| GPS tracking (tracking device, geolocation) | – | 11% |
| electronic monitoring (ankle monitor, GPS monitoring) | – | 1% |
| radio / communications system (tactical communications, encrypted) | TELECOMMUNICATIONS 1,409 (2%); TELECOMMUNICATIONS EQUIPMENT 537 (1%) | 10% |

## 6. Screening and inspection

| Keyword (variants) | Tag rows (share) | Sample docs |
|---|---|---|
| security screening (passenger screening, people screening, vehicle screening, baggage screening, pre-screening) | – | 9% |
| scanner (generic: scanning equipment, scanning technology) | COMPUTER SCANNERS 701 (1%) | 12% |
| X-ray (X-ray machine, X-ray screening) | – | 9% |
| body scanner (full-body scanner, millimetre wave, backscatter, advanced imaging technology, whole body imaging) | AIRPORT BODY SCANS & PAT DOWNS 589 (1%) | 6% |
| metal detector (magnetometer) | – | 5% |
| explosive detection (explosives trace detection, ETD, bomb detection, ion mobility) | – | 6% |
| radiation detector (radiation portal monitor, nuclear detection, radiological, dirty bomb) | RADIATION DETECTORS 477 (1%) | 7% |
| container scanning (cargo screening, cargo scanning, non-intrusive inspection, NII, gamma-ray, 100 percent scanning, Megaports) | – | 5% |
| Container Security Initiative (C-TPAT, Secure Freight Initiative, SAFE Port Act) | – | 1% |
| detection system (detection technology, detection equipment) | – | 10% |
| sniffer dog (canine unit, detection dog, K-9) | – | 3% |

## 7. Digital infrastructure, data and AI

| Keyword (variants) | Tag rows (share) | Sample docs |
|---|---|---|
| artificial intelligence (AI, machine learning, deep learning, neural network) | ARTIFICIAL INTELLIGENCE 1,348 (2%); EMERGING TECHNOLOGY 882 (1%) | 14% |
| algorithm (algorithmic) | – | 5% |
| big data / data analytics (data mining, predictive analytics, risk analysis, risk assessment, risk-based) | DATA ANALYTICS 865 (1%) | 19% |
| video analytics (computer vision, image recognition, object recognition, pattern recognition, automatic detection) | PATTERN RECOGNITION 1,644 (3%) | 10% |
| digitisation (digitization, digital border, automation, modernisation, paperless, e-government) | COMPUTING & INFORMATION TECHNOLOGY 1,866 (3%) | 25% |
| software (computer software, management software) | COMPUTER SOFTWARE 2,486 (4%); SOFTWARE SERVICES & APPLICATIONS 1,263 (2%) | – |
| RFID (radio frequency identification) | RADIO FREQUENCY IDENTIFICATION 1,208 (2%) | 5% |
| mobile app (smartphone app, mobile application, CBP One) | – | 16% |
| mobile phone / cell phone (cellular, phone tracking) | MOBILE & CELLULAR TELEPHONES 1,115 (2%) | 16% |
| social media (social media monitoring) | INTERNET SOCIAL NETWORKING 702 (1%) | 16% |
| cybersecurity (cyber, hacking, data breach) | CYBERCRIME 1,314 (2%); INFORMATION SECURITY & PRIVACY 1,784 (3%) | 25% |
| cloud computing (cloud-based) | – | 6% |
| 5G | 5G WIRELESS 572 (1%) | 4% |
| blockchain | – | 1% |
| computer network | COMPUTER NETWORKS 1,029 (2%) | – |

## 8. Public-health border technology (COVID-19 cluster, 2020 – 2022)

| Keyword (variants) | Tag rows (share) | Sample docs |
|---|---|---|
| COVID-19 (coronavirus, pandemic, epidemic, infectious disease) | COVID-19 CORONAVIRUS 4,284 (7%); COVID CORONAVIRUS 4,381 (7%); INFECTIOUS DISEASE 3,591 (5%); EPIDEMICS 2,064 (3%); PANDEMICS 1,384 (2%) | – |
| PCR test / testing on arrival (nucleic acid test, rapid antigen test) | – | 4% |
| health code / contact tracing (QR code, tracing app, quarantine app, LeaveHomeSafe, TraceTogether) | – | 2% |
| vaccine passport (vaccination certificate, digital health certificate, health pass, green pass, COVID pass, travel bubble) | – | 2% |
| temperature screening (thermal screening, fever screening, thermal scanner) | – | 1% |
| health screening (quarantine) | – | – |

## 9. Vendors and industry

Company names are the most reliable way to catch procurement and deployment stories. Counts are for the company group; general IT vendors are listed because they appear as integrators in border contracts.

| Vendor group | Sample docs |
|---|---|
| Boeing, Raytheon, Lockheed Martin, Northrop Grumman, General Dynamics | 19% |
| Motorola, Siemens, Honeywell, Cisco | 18% |
| Microsoft, Oracle, Google, Amazon, HP, Dell | 20% |
| Accenture, Unisys, IBM, Deloitte | 13% |
| NEC | 13% |
| Elbit Systems, Israel Aerospace Industries, Magal, Rafael, Controp | 12% |
| L-3 / L3Harris, Leidos, SAIC | 11% |
| BAE Systems | 9% |
| IDEMIA (Morpho, MorphoTrust, Safran, Sagem, Oberthur) | 9% |
| Thales | 9% |
| FLIR, Axis Communications, Teledyne, Cubic, DRS Technologies, Getac, Vigilant | 9% |
| Huawei, Hikvision, Dahua, ZTE, Nuctech | 6% |
| Cognitec, Vision-Box, SITA, Amadeus, Zebra Technologies | 6% |
| Rapiscan, OSI Systems, Smiths Detection, American Science & Engineering | 4% |
| CEIA, Garrett, Cross Match, Aware | 3% |
| Gemalto, Giesecke+Devrient, Veridos | 3% |
| Palantir, Anduril | 1% |
| Securiport | 0.1% |

Also seen in the text but not counted separately: Airbus, Leonardo (Finmeccanica, Selex), Indra, Saab, United Technologies.

## 10. Deployment, procurement and evaluation (status terms)

These are the words that signal a deployment record (planned, tendered, deployed, operational, cancelled) and are needed for the STATUS_PHRASE label in the pipeline.

| Keyword (variants) | Sample docs |
|---|---|
| installed / deployed / operational / launched / commissioned / went live / rolled out | 67% |
| funding / budget / appropriation / grant / funded by / World Bank / European Commission / USAID / donor | 56% |
| audit / inspector general / GAO / National Audit Office / cost overrun / over budget / behind schedule / scrapped / cancelled | 33% |
| procurement / tender / contract award / awarded a contract / contract worth / request for proposal (RFP) | 24% |
| pilot project / pilot programme / pilot scheme / trial / phased in | 25% |

## 11. Issue framing (policy and rights debates)

| Keyword (variants) | Tag rows (share) | Sample docs |
|---|---|---|
| privacy / data protection (personal data) | PRIVACY RIGHTS 541 (1%); INFORMATION SECURITY & PRIVACY 1,784 (3%) | 22% |
| civil liberties / human rights / civil rights | – | 25% |
| racial profiling / discrimination / bias | – | 18% |
| legislation / public policy / regulation | LEGISLATION 3,053 (5%); PUBLIC POLICY 4,116 (6%) | – |
| international agreement / treaty / cooperation (EU, UN, bilateral) | AGREEMENTS 6,736 (10%); EUROPEAN UNION 5,259 (8%); UNITED NATIONS 3,802 (6%) | – |

## 12. Compact search string

A starting point for re-running LexisNexis, Factiva or similar databases in English. Technology block AND border block; adjust proximity operators to the database.

Technology block:

```
biometric* OR fingerprint* OR "facial recognition" OR "face recognition" OR "iris scan*" OR "e-passport*" OR "biometric passport*" OR "e-gate*" OR "automated border control" OR "smart gate*" OR "automated passport control" OR "trusted travel*" OR "entry-exit system" OR "entry/exit system" OR "watch list" OR watchlist OR "no-fly list" OR "passenger name record" OR PNR OR "advance passenger information" OR "border management system" OR "integrated border management" OR "single window" OR surveillance OR CCTV OR "surveillance camera*" OR drone* OR UAV* OR "unmanned aerial" OR aerostat* OR radar OR satellite OR "ground sensor*" OR "motion sensor*" OR "thermal imag*" OR infrared OR "night vision" OR "surveillance tower*" OR "virtual fence" OR "smart wall" OR "smart border*" OR "e-border*" OR "licen?e plate reader*" OR ANPR OR "x-ray" OR "body scanner*" OR "millimet* wave" OR "metal detector*" OR "explosive* detection" OR "radiation detect*" OR "radiation portal" OR "container scanning" OR "cargo screening" OR "non-intrusive inspection" OR "artificial intelligence" OR "machine learning" OR algorithm* OR "big data" OR "data analytics" OR "video analytics" OR RFID OR "mobile app*" OR "digital identit*" OR "identity card*" OR "smart card*" OR "health code" OR "contact tracing" OR "vaccine passport*" OR "temperature screening" OR "thermal screening"
```

Named systems block (search on their own, no border block needed):

```
"US-VISIT" OR IDENT OR SBInet OR "Secure Border Initiative" OR "Integrated Fixed Tower*" OR "Automated Targeting System" OR "Secure Flight" OR CAPPS OR "E-Verify" OR "Global Entry" OR NEXUS OR SENTRI OR ESTA OR "Schengen Information System" OR "SIS II" OR "Visa Information System" OR Eurodac OR "Entry/Exit System" OR EES OR ETIAS OR Eurosur OR Frontex OR "eu-LISA" OR "Smart Borders" OR SIVE OR PISCES OR MIDAS OR "Container Security Initiative" OR "C-TPAT" OR "Secure Freight Initiative" OR Megaports
```

Border block:

```
border* OR "port* of entry" OR checkpoint* OR customs OR immigration OR "passport control" OR visa* OR airport* OR seaport* OR frontier* OR Frontex OR "coast guard" OR "border patrol"
```

Vendor block (optional, for procurement stories):

```
Thales OR IDEMIA OR Morpho* OR Safran OR Gemalto OR Veridos OR "Giesecke" OR NEC OR Elbit OR "Israel Aerospace" OR Magal OR Rafael OR Huawei OR Hikvision OR Dahua OR Nuctech OR Securiport OR Accenture OR Unisys OR IBM OR Boeing OR Raytheon OR Lockheed OR Northrop OR "General Dynamics" OR "L-3" OR L3Harris OR Leidos OR SAIC OR Rapiscan OR "OSI Systems" OR "Smiths Detection" OR "BAE Systems" OR Airbus OR Leonardo OR Indra OR Saab OR FLIR OR Cognitec OR "Vision-Box" OR SITA OR Palantir OR Anduril OR Motorola OR Siemens OR Honeywell OR Cisco
```

## Caveats

- Full-text shares are from a 12-country sample, not the whole corpus; country files were chosen for regional spread and manageable size. The USA (8,067 documents, mostly congressional transcripts) is not in the sample.
- Generic words (surveillance, camera, sensor, satellite, database, installed, funding) are counted because they are useful as a filter, not as evidence of border technology on their own. Pair them with the border block.
- Matching is substring-based with word boundaries for acronyms; a few company names (Leonardo, Indra, Saab) share spellings with people and places and were not counted.
- The scan script is at `/private/tmp/claude-501/-Users-yuxin--claude-spares-spare-MR0U0V/d4311147-1ecd-4e44-be5d-fef8beee7aa9/scratchpad/scripts/scan_terms.py` for re-running on more files; the source zips were read without modification.
