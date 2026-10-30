# FATE, Echo & TEE Report

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)

Browser-based reporting templates for **Focus Assessed Transthoracic Echo (FATE)** and **basic intra-operative transoesophageal echocardiography (TEE)**. Fill them in on screen, and they print (or save to PDF) as clean A4 pages with reference ranges, graded findings and a findings summary.

Built for the Department of Anaesthesia, New Somerset Hospital (Western Cape Government: Health). The header is editable, so other departments can use it as-is.

---

## Quick start

1. Download `index.html` (FATE) and `tee.html` (TEE) into the same folder.
2. Open either file in a modern browser (Chrome, Edge, Firefox or Safari).
3. Pick a view, enter the study, then click **Print / Save PDF**.

There is nothing to install and no server. Everything runs in the page. The **TEE** button on the FATE page and the **FATE** button on the TEE page link the two files.

> **Tip:** Click **Load example** to see a fully populated report.

---

## Files

| File | Purpose |
|---|---|
| `index.html` | FATE report: Basic FATE, Advanced FATE and FATE Card views |
| `tee.html` | Intra-operative TEE report and TEE reference guide |
| `Archive/Echocardiogram_Report.html` | The former full TTE *Echocardiogram Report* view, archived on 30/10/2026. Still works, but is no longer maintained |

---

## FATE page (`index.html`)

| Tab | Purpose | Pages |
|---|---|---|
| **Basic FATE** | The six-step FATE sequence: views obtained, obvious pathology, dimensions, biventricular function, pleura, clinical context, IVC | 1 |
| **Advanced FATE** | Basic FATE plus selectable extended sections (diastolic function, RV/PA pressure, aorta, flow and output, AS, MS, valve regurgitation). Unticked sections are left out and pages re-flow automatically | 1+ |
| **FATE Card** | One-page quick reference transcribed from the FATE card (USabcd, 2020) | 1 |
| **TEE** | Link to the TEE page | — |

Shared fields (patient details, measurements, conclusion) sync across the FATE views.

**Measurement grading**
- Each measurement shows its unit, sex-specific reference range, source and a colour-coded finding (normal, mild, moderate, severe, below reference).
- Indexed values (LAVI, SVi, CI, AVAi) are calculated from BSA; a warning appears if height or weight is missing.
- BSA formula selectable: DuBois (default) or Mosteller.

**Automatic calculations**
- FS, EF (≈ 2 × FS)
- E/A, E/e′ (septal, lateral or average, with the matching threshold)
- IVC collapse and RAP estimate (ASE 2025 scheme, including secondary signs and the 20 mmHg category)
- RVSP, TAPSE/sPAP
- SV, SVi, CO, CI (LVOT method)
- AV peak gradient, AVA (continuity), AVAi, dimensionless index; MVA (220/PHT)

**Interpretation**
- **Diastolic function** graded by the 2025 ASE algorithm, with handling for AF, moderate-or-worse MAC, severe primary MR and other confounders, plus a written basis for the grade.
- **Aortic stenosis** summary with discordance detection and low-flow / low-gradient prompts.
- **Regurgitation** by vena contracta (ESC/EACTS 2025), including the 5-grade TR scale and MR mechanism (primary vs secondary).
- EPSS (> 7 mm) and MAPSE are shown as binary flags, not graded.
- RAP and RVSP are suppressed when the patient is on positive-pressure ventilation.

**Workflow**
- **Eyeball assessment** checklist with measurement-based suggestions ("Tick these").
- **Add findings to conclusion** compiles abnormal results into a numbered list.
- **Set all to Good** for view quality.
- Report IDs generated from the study date and time (e.g. `FATE-20261020-1145`).

---

## TEE page (`tee.html`)

| Tab | Purpose | Pages |
|---|---|---|
| **FATE** | Link back to the FATE page | — |
| **TEE Report** | Basic intra-operative TEE report covering the EACTA intra-operative TEE dataset | 3 |
| **Reference Guide** | Basic perioperative views and angles, 17-segment model with coronary territories and TEE view mapping, wall motion scoring, valve grading tables, formulas and intra-operative points | 1 |

**Report contents**
- Patient strip: OR/ICU, elective/emergency, ECG rhythm, probe insertion, image quality, previous echo, CVP, surgery.
- Views obtained: the 11 ASE/SCA basic perioperative views plus extended views (commissural, TG basal SAX, deep TG, UE arch, epiaortic).
- LV and RV: morphology (n/h/d), volume status, global function (1–4), LVIDd/s, LVEF, wall thickness, RV basal diameter, TAPSE, RV FAC.
- **Regional wall motion:** clickable 17-segment bullseye and ME 4C, ME 2C, ME LAX and TG mid SAX diagrams, all linked to a segment table. Scores 1–4 or X (not seen). The page calculates the wall motion score index and lists abnormal segments by coronary territory.
- Atria and LAA (size, spontaneous echo contrast, thrombus, mass, device; LAA emptying velocity), septa and shunts, pericardial and pleural effusions.
- Mitral, aortic, tricuspid and pulmonary valves with stenosis and regurgitation measurements, a per-valve "parameters suggest" line (with discordance detection), and manual integrated grades.
- Thoracic aorta: status, diameter, plaque thickness and mobility (≥4 mm or mobile flagged as complex), dissection.
- Summary of findings (with **Add findings to summary**), structured post-procedure examination and adverse events, signatures.

**Calculations:** LVEF (Teichholz), RV FAC, AL/PL ratio and C-sept (SAM risk), MVA (220/PHT), PISA EROA and regurgitant volume, SV and CO, AV peak gradient, AVA (continuity), AVAi, velocity ratio, AR jet/LVOT %, TV annulus index, SPAP (4V² + CVP), PV peak gradient, PR jet/RVOT %, BSE height-indexed aortic dimensions.

**Reference display:** ASE/EACVI limits grade each finding; BSE 2020 limits are shown on a second line, with a note when the BSE grade differs.

The TEE page saves its drafts separately from the FATE page.

---

## Printing (both pages)

- True A4 portrait layout with headers, page numbers, references and disclaimers on every sheet.
- Print the current view or all views.
- Form controls are replaced with plain text in print for consistent output across browsers.
- Dates are shown as dd/mm/yyyy, and each page carries a generation timestamp with UTC offset.

---

## Data and privacy

- **No data leaves the device.** There are no network calls apart from loading Google Fonts.
- Drafts autosave to the browser's `localStorage` on that machine only. Use **Clear** after each patient on shared computers.
- Do not commit completed reports or patient data to this repository.

---

## Reference sources

| Key | Source | Used for |
|---|---|---|
| **L** | Lang RM et al. *J Am Soc Echocardiogr* 2015;28:1–39 / *Eur Heart J Cardiovasc Imaging* 2015;16:233–71 | Chamber quantification limits (sex-specific, BSA-indexed) |
| **B** | Harkness A et al. *Echo Res Pract* 2020;7:G1–G18 (BSE) | Second-line normal ranges on the TEE page; height-indexed aorta |
| **A** | Mukherjee M et al. *J Am Soc Echocardiogr* 2025;38:141–86 | TAPSE, RV basal diameter, TAPSE/sPAP, IVC/RAP |
| **A** | Nagueh SF et al. *J Am Soc Echocardiogr* 2025;38:537–69 | Diastolic function grading |
| **A** | Baumgartner H et al. *J Am Soc Echocardiogr* 2017;30:372–92 and 2009;22:1–23 | Aortic, mitral, tricuspid and pulmonary stenosis |
| **E** | Praz F et al. 2025 ESC/EACTS VHD guidelines. *Eur Heart J* 2025;46:4635–736 | Regurgitation (vena contracta); TV annulus at left-sided surgery |
| | Hahn RT, Zamorano JL. *Eur Heart J Cardiovasc Imaging* 2017;18:1342–3 | 5-grade TR scale |
| **Z** | Zoghbi WA et al. *J Am Soc Echocardiogr* 2017;30:303–71 | EROA, regurgitant volume, AR jet/LVOT and PHT (TEE page) |
| **V** | Lancellotti P et al. *Eur Heart J Cardiovasc Imaging* 2013;14:611–44 | Pulmonary regurgitation (TEE page) |
| **T** | Reeves ST et al. *J Am Soc Echocardiogr* 2013;26:443–56 · Hahn RT et al. *J Am Soc Echocardiogr* 2013;26:921–64 · Wheeler R et al. *Echo Res Pract* 2015;2:G29–45 | Basic and comprehensive TEE examination; BSE TOE minimum dataset |
| **S** | Cerqueira MD et al. *Circulation* 2002;105:539–42 | 17-segment model and coronary territories |
| **M** | Maslow AD et al. *J Am Coll Cardiol* 1999;34:2096–104 | SAM risk before mitral repair |
| **K** | Katz ES et al. *J Am Coll Cardiol* 1992;20:70–7 · Amarenco P et al. *N Engl J Med* 1994;331:1474–9 | Aortic atheroma; plaque ≥4 mm |
| | Humbert M et al. 2022 ESC/ERS PH guidelines. *Eur Heart J* 2022;43:3618–731 | TR velocity, PH probability (FATE) |
| **F** | FATE card 2020, USabcd; Jensen MB et al. *Eur J Anaesthesiol* 2004;21:700–7 | FATE protocol; values where ASE has none |
| **P** | McKaigney CJ et al. *Am J Emerg Med* 2014;32:493–7 | EPSS |

**Hierarchy:** ASE/EACVI limits are used wherever they exist; FATE card values are used only where ASE gives none. On the TEE page, BSE ranges are shown alongside but do not set the primary grade.

---

## Attribution

The FATE Card view is transcribed and adapted from the **FATE card (2020)** published by [USabcd](https://usabcd.org/wp-content/uploads/FATEmedia/FATEcard2020.pdf). The card's images and pathology examples are not reproduced; see the original for the authoritative version. The card's authors accept no responsibility for its use.

The TEE report's field set follows the **EACTA intra-operative TEE report form** (European Association of Cardiothoracic Anaesthesiology). Its layout, diagrams and wording are original; the EACTA form, name and logo are not reproduced.

---

## Disclaimer

This is a documentation and teaching aid, not a medical device. Automated grades and interpretations support, but do not replace, clinical judgement. A focused point-of-care study answers a clinical question and does not replace a comprehensive echocardiogram. Intra-operative findings depend on loading conditions under anaesthesia. Always check values against image quality, the clinical picture and current guidelines.

---

## Licence

The original code and text in this repository are © 2026 Michael-Jon Rosslee, licensed under [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/).

You may use, share and adapt this work for **non-commercial** purposes, including clinical, teaching and research use in hospitals and universities, as long as you give appropriate credit and indicate any changes. Commercial use requires the author's permission.

**Not covered by this licence:** content on the **FATE Card** view that is transcribed or adapted from the FATE card (2020) remains the copyright of USabcd. It is included for teaching reference with attribution and is not licensed under CC BY-NC 4.0. Contact USabcd for permission to reuse it.

Cited guidelines and publications remain the copyright of their respective publishers. See [`LICENSE.md`](LICENSE.md) for details.

---

## Author

Dr Michael-Jon Rosslee — Department of Anaesthesia, New Somerset Hospital / Department of Anaesthesia and Perioperative Medicine, University of Cape Town
