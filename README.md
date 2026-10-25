# Rocket: Modern VistA Electronic Health Record Client

**[▶ View as online slide show](https://rafael5.github.io/rocket/)** &nbsp;|&nbsp; **[📄 Download PDF slide deck](rocket-slides.pdf)**

Rocket is a modern, open-source desktop EHR client for the U.S. Department of Veterans Affairs VistA (Veterans Health Information Systems and Technology Architecture) system. It reimagines the 25-year-old CPRS (Computerized Patient Record System) using today's technology, while keeping full compatibility with the existing VistA RPC Broker infrastructure.

Rocket is a replacement for CPRS that focuses on **SI (Super Intelligence)**, modularity, and performance. It is the brainchild of **Daniel Breznau**.

**Project page author:** Frank S. Drescher, Physician (VA SI Resources SharePoint site)

**Status:** Active development (Stage 4: Clinical Pages)

- Source is embedded in ADOS (`Rocket / README.md`).
- A compiled executable is available on the VA SI Resources SharePoint site, under Wiki → Downloads.
- Screenshots of the UI are not yet available, because the UI is under active development. The images below are the project's SharePoint documentation pages.

## Tech stack

| Layer | Technology |
|---|---|
| Desktop shell | Tauri 2 (Rust) |
| UI framework | React 19 + TypeScript |
| State management | Zustand |
| Styling | Tailwind CSS 4 |
| Routing | React Router 7 |
| RPC transport | Rust (tokio, native-tls), XWB protocol over TCP |
| SI integration | Rust → AWS Bedrock (Claude) |
| Runtime | Bun |
| Build | Vite 6 |
| Icons | Lucide React |

## Features

### Implemented

- **VistA RPC Broker:** full XWB protocol implementation in Rust (TCP + TLS)
- **PIV / SSOi authentication:** smart card login via IAM STS SAML tokens
- **Multi-patient tabs:** browser-style tab bar for multiple patients
- **Cover Sheet:** dashboard with allergies, problems, meds, vitals, labs, reminders
- **Clinical pages:** Notes, Problems, Medications, Orders, Labs, Consults, Reports, Vitals, Surgery, D/C Summaries, Imaging
- **SI panel:** integrated SI analysis (Assessment & Plan, Dx List, Safety Checks, etc.) via AWS Bedrock
- **Medical references:** point-of-care clinical decision support built into the SI agent (see below)
- **Command palette:** Ctrl+K quick navigation and order search
- **Dark / Light / Auto theme:** follows the Windows system preference
- **Plugin system:** extensible architecture for custom pages, widgets, and SI prompts
- **Auto-update:** network share-based shadow copy updater
- **Site auto-detection:** reads the machine hostname to auto-select the VistA server

### Planned

- Order entry dialogs (complex orders, order sets)
- Note authoring with a template system
- CCOW patient context sharing
- Patient timeline (unified chronological view)
- 508 accessibility compliance

## Medical references (point-of-care)

Rocket's SI agent includes built-in access to medical reference data, enabling evidence-based clinical decision support without any local databases or commercial subscriptions. All data is fetched on demand from free public APIs.

### Clinical calculators (40+)

Compiled directly into the Rust binary: no API calls, instant results. Each returns an exact score, a clinical interpretation, and a literature citation.

| Category | Calculators |
|---|---|
| Cardiovascular | Wells DVT, Wells PE, CHA2DS2-VASc, HAS-BLED, HEART, TIMI NSTEMI/STEMI, GRACE, ASCVD Risk, MAP, QTc (Bazett) |
| Pulmonary | CURB-65, PERC Rule |
| Critical care | qSOFA, SOFA, APACHE II |
| Renal / metabolic | Cockcroft-Gault, CKD-EPI 2021 eGFR, Corrected Calcium, Anion Gap, FENa, Winter's Formula, BMI |
| GI / hepatology | MELD-Na, Child-Pugh, FIB-4, Alvarado, Maddrey DF, West Haven |
| VTE prophylaxis | Padua VTE Risk, Caprini |
| Neurology | GCS, NIHSS, ABCD2 |
| Psychiatry | PHQ-9, GAD-7, AUDIT-C, CAGE, C-SSRS, MoCA/MMSE, 4AT Delirium |
| ENT | Modified Centor |
| Conversions | Steroid equivalence, Opioid MME |

### Drug reference APIs

| Source | Data provided | API |
|---|---|---|
| DailyMed (NLM) | Full FDA drug labels: indications, dosing, contraindications, black box warnings, adverse reactions | dailymed.nlm.nih.gov |
| RxNorm (NLM) | Drug name normalization: brand ↔ generic ↔ ingredient mapping | rxnav.nlm.nih.gov |
| MED-RT / RxClass (NLM) | VA drug classes, mechanism of action, pharmacologic class | rxnav.nlm.nih.gov |
| RxNorm Interactions (NLM) | Drug-drug interaction checking with severity ratings | rxnav.nlm.nih.gov |
| OpenFDA (FDA) | Post-market adverse event data (FAERS) | api.fda.gov |
| PubMed (NLM) | Systematic reviews, meta-analyses, clinical trials | eutils.ncbi.nlm.nih.gov |

All APIs are free, require no authentication, and are provided by NIH/NLM/FDA as public health resources.

## Slide gallery

Source slides for this summary are `rocket-001.png` to `rocket-010.png`. Click any thumbnail to view it full size.

<table>
  <tr>
    <td align="center"><a href="rocket-001.png"><img src="rocket-001.png" width="220" alt="rocket-001.png"></a><br><sub>rocket-001.png</sub></td>
    <td align="center"><a href="rocket-002.png"><img src="rocket-002.png" width="220" alt="rocket-002.png"></a><br><sub>rocket-002.png</sub></td>
    <td align="center"><a href="rocket-003.png"><img src="rocket-003.png" width="220" alt="rocket-003.png"></a><br><sub>rocket-003.png</sub></td>
    <td align="center"><a href="rocket-004.png"><img src="rocket-004.png" width="220" alt="rocket-004.png"></a><br><sub>rocket-004.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-005.png"><img src="rocket-005.png" width="220" alt="rocket-005.png"></a><br><sub>rocket-005.png</sub></td>
    <td align="center"><a href="rocket-006.png"><img src="rocket-006.png" width="220" alt="rocket-006.png"></a><br><sub>rocket-006.png</sub></td>
    <td align="center"><a href="rocket-007.png"><img src="rocket-007.png" width="220" alt="rocket-007.png"></a><br><sub>rocket-007.png</sub></td>
    <td align="center"><a href="rocket-008.png"><img src="rocket-008.png" width="220" alt="rocket-008.png"></a><br><sub>rocket-008.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-009.png"><img src="rocket-009.png" width="220" alt="rocket-009.png"></a><br><sub>rocket-009.png</sub></td>
    <td align="center"><a href="rocket-010.png"><img src="rocket-010.png" width="220" alt="rocket-010.png"></a><br><sub>rocket-010.png</sub></td>
    <td align="center"><a href="rocket-011.png"><img src="rocket-011.png" width="220" alt="rocket-011.png"></a><br><sub>rocket-011.png</sub></td>
    <td align="center"><a href="rocket-012.png"><img src="rocket-012.png" width="220" alt="rocket-012.png"></a><br><sub>rocket-012.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-013.png"><img src="rocket-013.png" width="220" alt="rocket-013.png"></a><br><sub>rocket-013.png</sub></td>
    <td align="center"><a href="rocket-014.png"><img src="rocket-014.png" width="220" alt="rocket-014.png"></a><br><sub>rocket-014.png</sub></td>
    <td align="center"><a href="rocket-015.png"><img src="rocket-015.png" width="220" alt="rocket-015.png"></a><br><sub>rocket-015.png</sub></td>
    <td align="center"><a href="rocket-016.png"><img src="rocket-016.png" width="220" alt="rocket-016.png"></a><br><sub>rocket-016.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-017.png"><img src="rocket-017.png" width="220" alt="rocket-017.png"></a><br><sub>rocket-017.png</sub></td>
    <td align="center"><a href="rocket-018.png"><img src="rocket-018.png" width="220" alt="rocket-018.png"></a><br><sub>rocket-018.png</sub></td>
    <td align="center"><a href="rocket-019.png"><img src="rocket-019.png" width="220" alt="rocket-019.png"></a><br><sub>rocket-019.png</sub></td>
    <td align="center"><a href="rocket-020.png"><img src="rocket-020.png" width="220" alt="rocket-020.png"></a><br><sub>rocket-020.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-021.png"><img src="rocket-021.png" width="220" alt="rocket-021.png"></a><br><sub>rocket-021.png</sub></td>
    <td align="center"><a href="rocket-022.png"><img src="rocket-022.png" width="220" alt="rocket-022.png"></a><br><sub>rocket-022.png</sub></td>
    <td align="center"><a href="rocket-023.png"><img src="rocket-023.png" width="220" alt="rocket-023.png"></a><br><sub>rocket-023.png</sub></td>
    <td align="center"><a href="rocket-024.png"><img src="rocket-024.png" width="220" alt="rocket-024.png"></a><br><sub>rocket-024.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-025.png"><img src="rocket-025.png" width="220" alt="rocket-025.png"></a><br><sub>rocket-025.png</sub></td>
    <td align="center"><a href="rocket-026.png"><img src="rocket-026.png" width="220" alt="rocket-026.png"></a><br><sub>rocket-026.png</sub></td>
    <td align="center"><a href="rocket-027.png"><img src="rocket-027.png" width="220" alt="rocket-027.png"></a><br><sub>rocket-027.png</sub></td>
    <td align="center"><a href="rocket-028.png"><img src="rocket-028.png" width="220" alt="rocket-028.png"></a><br><sub>rocket-028.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-029.png"><img src="rocket-029.png" width="220" alt="rocket-029.png"></a><br><sub>rocket-029.png</sub></td>
    <td align="center"><a href="rocket-030.png"><img src="rocket-030.png" width="220" alt="rocket-030.png"></a><br><sub>rocket-030.png</sub></td>
    <td align="center"><a href="rocket-031.png"><img src="rocket-031.png" width="220" alt="rocket-031.png"></a><br><sub>rocket-031.png</sub></td>
    <td align="center"><a href="rocket-032.png"><img src="rocket-032.png" width="220" alt="rocket-032.png"></a><br><sub>rocket-032.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-033.png"><img src="rocket-033.png" width="220" alt="rocket-033.png"></a><br><sub>rocket-033.png</sub></td>
    <td align="center"><a href="rocket-034.png"><img src="rocket-034.png" width="220" alt="rocket-034.png"></a><br><sub>rocket-034.png</sub></td>
    <td align="center"><a href="rocket-035.png"><img src="rocket-035.png" width="220" alt="rocket-035.png"></a><br><sub>rocket-035.png</sub></td>
    <td align="center"><a href="rocket-036.png"><img src="rocket-036.png" width="220" alt="rocket-036.png"></a><br><sub>rocket-036.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-037.png"><img src="rocket-037.png" width="220" alt="rocket-037.png"></a><br><sub>rocket-037.png</sub></td>
    <td align="center"><a href="rocket-038.png"><img src="rocket-038.png" width="220" alt="rocket-038.png"></a><br><sub>rocket-038.png</sub></td>
    <td align="center"><a href="rocket-039.png"><img src="rocket-039.png" width="220" alt="rocket-039.png"></a><br><sub>rocket-039.png</sub></td>
    <td align="center"><a href="rocket-040.png"><img src="rocket-040.png" width="220" alt="rocket-040.png"></a><br><sub>rocket-040.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-041.png"><img src="rocket-041.png" width="220" alt="rocket-041.png"></a><br><sub>rocket-041.png</sub></td>
    <td align="center"><a href="rocket-042.png"><img src="rocket-042.png" width="220" alt="rocket-042.png"></a><br><sub>rocket-042.png</sub></td>
    <td align="center"><a href="rocket-043.png"><img src="rocket-043.png" width="220" alt="rocket-043.png"></a><br><sub>rocket-043.png</sub></td>
    <td align="center"><a href="rocket-044.png"><img src="rocket-044.png" width="220" alt="rocket-044.png"></a><br><sub>rocket-044.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-045.png"><img src="rocket-045.png" width="220" alt="rocket-045.png"></a><br><sub>rocket-045.png</sub></td>
    <td align="center"><a href="rocket-046.png"><img src="rocket-046.png" width="220" alt="rocket-046.png"></a><br><sub>rocket-046.png</sub></td>
    <td align="center"><a href="rocket-047.png"><img src="rocket-047.png" width="220" alt="rocket-047.png"></a><br><sub>rocket-047.png</sub></td>
    <td align="center"><a href="rocket-048.png"><img src="rocket-048.png" width="220" alt="rocket-048.png"></a><br><sub>rocket-048.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-049.png"><img src="rocket-049.png" width="220" alt="rocket-049.png"></a><br><sub>rocket-049.png</sub></td>
    <td align="center"><a href="rocket-050.png"><img src="rocket-050.png" width="220" alt="rocket-050.png"></a><br><sub>rocket-050.png</sub></td>
    <td align="center"><a href="rocket-051.png"><img src="rocket-051.png" width="220" alt="rocket-051.png"></a><br><sub>rocket-051.png</sub></td>
    <td align="center"><a href="rocket-052.png"><img src="rocket-052.png" width="220" alt="rocket-052.png"></a><br><sub>rocket-052.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-053.png"><img src="rocket-053.png" width="220" alt="rocket-053.png"></a><br><sub>rocket-053.png</sub></td>
    <td align="center"><a href="rocket-054.png"><img src="rocket-054.png" width="220" alt="rocket-054.png"></a><br><sub>rocket-054.png</sub></td>
    <td align="center"><a href="rocket-055.png"><img src="rocket-055.png" width="220" alt="rocket-055.png"></a><br><sub>rocket-055.png</sub></td>
    <td align="center"><a href="rocket-056.png"><img src="rocket-056.png" width="220" alt="rocket-056.png"></a><br><sub>rocket-056.png</sub></td>
  </tr>
  <tr>
    <td align="center"><a href="rocket-057.png"><img src="rocket-057.png" width="220" alt="rocket-057.png"></a><br><sub>rocket-057.png</sub></td>
  </tr>
</table>
