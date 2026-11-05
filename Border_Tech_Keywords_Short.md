# Border-control technology: short keyword list for headline + first 50 words

Purpose: estimate how many articles in a media database are about technology used in border control, when only the headline and the first 50 words of each article are available.

## Rule

An article counts if it contains **at least one Border term (A) AND at least one Technology term (B)**, OR **any Named system (D)**.
Block C (generic technology words) is optional: adding it to B raises coverage but lets in more noise. Match case-insensitively on headline + first 50 words, whole words only, except the short acronyms marked (cs), which should be matched case-sensitively.

## A. Border terms (need one)

border, borders, frontier, customs, immigration, immigrant(s), migrant(s), migration, asylum, refugee(s), visa(s), passport(s), checkpoint(s), port of entry, airport(s), seaport(s), port security, border patrol / border force / border guard / border police / border agency / border agents / border officers, coast guard, Frontex, CBP (cs), DHS (cs), homeland security, smuggling / smuggler(s), trafficking / trafficker(s), traveller(s) / traveler(s), passenger(s), aviation security, deportation / deported

Note: airport, passenger and aviation security pull in airport passenger screening (body scanners, X-ray). Drop them if airport security should not count as border control.

## B. Technology terms (need one), ordered by how often they appear in the first 50 words

1. biometric, biometrics
2. surveillance
3. facial recognition, face recognition
4. drone(s), UAV (cs), UAS (cs), unmanned
5. scanner(s), scanning, scanned, scan(s)
6. e-gate(s), eGate(s), automated gate(s), smart gate(s), SmartGate, automated border control, automated passport control, self-service gate / kiosk
7. camera(s), CCTV (cs), closed-circuit
8. detector(s), detection
9. e-passport(s), biometric passport(s), electronic passport(s), chip passport(s)
10. radar(s)
11. fingerprint(s), fingerprinting, palm print(s)
12. artificial intelligence, AI (cs), machine learning
13. iris, retina / retinal
14. sensor(s)
15. tower(s)
16. ID card(s), identity card(s), smart card(s), national ID card(s)
17. screening, screener(s)
18. smart border(s), e-border(s), e-Borders, digital border(s)
19. thermal, infrared, night vision
20. kiosk(s)
21. app(s)
22. database(s)
23. tracking, GPS (cs)
24. RFID (cs), chip(s), microchip(s)
25. X-ray(s)
26. watch list, watchlist, no-fly
27. e-visa(s), online visa(s)
28. health code, contact tracing, vaccine passport(s), QR code(s), health pass / health certificate
29. satellite(s)
30. metal detector(s), explosives detection, explosive trace
31. licence plate / license plate / number plate, ANPR (cs)
32. virtual fence, virtual wall, smart wall, smart fence, electronic fence
33. identification, identity verification, authenticate / authentication
34. imaging
35. registered traveller / registered traveler, trusted traveller / trusted traveler
36. PNR (cs), passenger name record, passenger data
37. algorithm(s)
38. software
39. cyber, cybersecurity

## C. Generic technology words (optional booster)

technology / technologies / technological, high-tech, tech, automated / automation / automatic, digital / digitisation / digitization, electronic, computerised / computerized, computer, smart, monitoring, equipment, device(s)

Broad variant (upper bound only, noisy): also add security, system(s), data.

## D. Named systems and programmes (count on their own, no border term needed)

Frontex, Eurosur, Entry/Exit System, EES (cs), ETIAS, Eurodac, Schengen Information System, SIS II, Visa Information System, Smart Borders, eu-LISA, e-Borders, US-VISIT, IDENT (cs), SBInet, Secure Border Initiative, Integrated Fixed Towers, Automated Targeting System, Secure Flight, E-Verify, Global Entry, NEXUS (cs), SENTRI, ESTA (cs), CBP One, Container Security Initiative, C-TPAT, SIVE (cs), PISCES (cs), MIDAS (cs)

## E. Vendors (optional, for procurement stories; count with a border term)

Elbit, Israel Aerospace Industries, Magal, Thales, IDEMIA, Morpho, Safran, Gemalto, Veridos, NEC, Vision-Box, SITA, Cognitec, FLIR, Rapiscan, Smiths Detection, OSI Systems, Securiport, Huawei, Hikvision, Dahua, Nuctech, Palantir, Anduril, BAE Systems, Airbus, Leonardo, Indra, Accenture, Unisys, L3Harris, Leidos, Raytheon, Lockheed Martin, Northrop Grumman, General Dynamics

## Expected coverage

Tested on 9,845 LexisNexis border-technology articles (12 countries, 1990 – 2025), using headline + first 50 words. "Tagged" means LexisNexis indexed the article with both a border subject and a technology subject.

| Setting | Share of all articles matched | Recall on tagged articles | Share of matches that are tagged |
|---|---|---|---|
| A and B, or D (strict) | 16% | 46% | 77% |
| A and (B or C), or D (recommended) | 19% | 52% | 74% |
| Broad variant of C added (security, system, data) | 34% | 66% | 55% |
| Headline only, A and B | 7% | 22% | – |

Reading: about half of the articles that are really about border technology name a technology in the first 50 words, so counts from this rule are a lower bound. Roughly three in four matched articles are on topic. Headline-only matching finds less than a quarter.

## Paste-ready regular expressions (Python, apply to headline + first 50 words)

```python
import re
A = re.compile(r"\b(borders?|frontiers?|customs|immigration|immigrants?|migrants?|migration|asylum|refugees?|visas?|passports?|checkpoints?|ports? of entry|airports?|seaports?|port security|border (patrol|force|guards?|police|agency|agents?|officers?|officials?)|coast ?guard|frontex|homeland security|smuggl\w*|traffick\w*|travell?ers?|passengers?|aviation security|deport\w*)\b", re.I)
A_cs = re.compile(r"\b(CBP|DHS)\b")
B = re.compile(r"\b(biometrics?|surveillance|fac(e|ial)[- ]recognition|drones?|unmanned|scanners?|scann(ing|ed)|scans?|e-?gates?|automated (border|passport|gates?)|smart ?gates?|automatic gates?|self-service (gates?|kiosks?)|cameras?|closed[- ]circuit|detectors?|detection|e-?passports?|(biometric|electronic|chip(ped)?) passports?|radars?|finger ?prints?|finger ?printing|palm ?prints?|iris|retina\w*|artificial intelligence|machine learning|sensors?|towers?|(id|identity|smart|national id) cards?|screening|screeners?|smart[- ]borders?|e-?borders?|digital borders?|thermal|infra-?red|night[- ]vision|kiosks?|apps?|databases?|tracking|microchips?|chips?|x-?rays?|watch ?lists?|no[- ]?fly|e-?visas?|online visas?|health codes?|contact[- ]tracing|vaccine passports?|QR codes?|health (pass|passes|certificates?)|satellites?|metal detectors?|explosives? (detection|trace)|licen[cs]e plates?|number plates?|virtual (fence|wall)|smart (wall|fence)|electronic fence|identification|identity verification|authenticat\w*|imaging|(registered|trusted)[- ]travell?ers?|passenger (name records?|data)|algorithms?|software|cyber\w*)\b", re.I)
B_cs = re.compile(r"\b(AI|UAVs?|UAS|CCTV|GPS|RFID|ANPR|PNR)\b")
C = re.compile(r"\b(technolog\w*|high-?tech|hi-tech|tech|automat\w*|digit(al|i[sz])\w*|electronic\w*|computeri[sz]ed|computer|smart|monitoring|equipment|devices?)\b", re.I)
D = re.compile(r"\b(Frontex|Eurosur|Entry[/-]Exit System|ETIAS|Eurodac|Schengen Information System|SIS II|Visa Information System|Smart Borders|eu[- ]?LISA|e-?Borders|US[- ]?VISIT|SBI-?net|Secure Border Initiative|Integrated Fixed Towers?|Automated Targeting System|Secure Flight|E-?Verify|Global Entry|SENTRI|CBP One|Container Security Initiative|C-TPAT)\b", re.I)
D_cs = re.compile(r"\b(EES|IDENT|NEXUS|ESTA|SIVE|PISCES|MIDAS)\b")

def is_border_tech(text, use_generic=True):
    a = A.search(text) or A_cs.search(text)
    b = B.search(text) or B_cs.search(text) or (use_generic and C.search(text))
    d = D.search(text) or D_cs.search(text)
    return bool((a and b) or d)
```

Machine-readable versions of this list: `border_tech_keywords.json` (term lists per block, case-sensitive acronyms separated, the same regexes, and the coverage figures) and `border_tech_keywords.txt` (one term per line, blocks separated by `## ` headers).

Source: terms were taken from the LexisNexis subject index of the existing corpus and from a full-text scan of 9,845 articles, then kept only if they appear in the first 50 words of on-topic articles. Full list with corpus counts: `Border_Tech_Keyword_List.md`.
