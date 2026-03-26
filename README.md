# semantic_loans

**Semantic Loans from English in Brazilian Portuguese: A Corpus Study**

This repository contains data collection scripts, annotated corpora, and analysis notebooks for a corpus-based investigation of English-induced semantic loans in Brazilian Portuguese (BP). The project focuses on cases where existing Portuguese words acquire new meanings under pressure from formally similar English cognates, displacing established native equivalents.

---

## Research Overview

### The phenomenon

A semantic loan occurs when an existing word in one language adopts a new meaning from a formally similar word in another language, without borrowing its phonetic form. This project investigates a specific subset of this phenomenon: cases where BP already has a native equivalent for the target meaning, yet speakers increasingly prefer a cognate form whose extended meaning is borrowed from English.

The central hypothesis is that high-volume translation — particularly machine translation in media and user-generated content — functions as a diffusion vector for these loans, accelerating their adoption beyond communities of bilingual speakers.

### Terms under investigation

| English source | Semantic loan (BP) | Native equivalent (BP) | Notes |
|---|---|---|---|
| *apply* (for a position) | *aplicar* | *candidatar-se*, *inscrever-se* | Core case study; see annotation guidelines below |
| *realize* (perceive, become aware) | *realizar* | *perceber*, *notar*, *dar-se conta* | Existing BP meaning: to carry out, to execute |
| *assume* (presuppose) | *assumir* | *presumir*, *supor*, *pressupor* | Existing BP meaning: to take on, to accept responsibility |
| *address* (a matter) | *endereçar* | *abordar*, *tratar* | Existing BP meaning: to put an address in, to send (a communication), to speak with|
| *massive* | *massivo* | *enorme*, *imenso*, *gigantesco* | Shift in frequency and register |
| *nominee* | *nomeado* | *indicado* | Existing BP meaning: to be called by, to be assigned to (a position) |

---

## Data Collection

Data was collected from Brazilian Portuguese subreddits via the [Arctic Shift](https://arctic-shift.photon-reddit.com) API, which provides access to Reddit comments archived between 2008 and 2022. Queries target both the loan form and its native equivalent(s) for each term, enabling proportional analysis over time.

### Subreddits

- r/brdev — software development community; high incidence of professional and technical language
- r/brasil — general Brazilian Portuguese community
- r/brasildob — Brazilian community with predominantly political content
- r/desabafos — informal register; personal narratives

### File structure

```
data/
  raw/
    apply_1.csv       # collected by date range
    apply_2.csv
    ...
  curated/
    apply_curated.csv
notebooks/
  curadoria_calques.ipynb
scripts/
  arctic_collector.py
  calque_analyzer.py       # TMX corpus analysis (COMPARA, OpenSubtitles)
  reddit_calque_analyzer.py
```

Raw files are organized by date range. A pre-filtering is performed to help on the classification via manual curation.

### Parallel corpora

In addition to Reddit data, the project uses parallel corpora to examine how translators handle the English source terms:

- **COMPARA** (Linguateca) — literary translations EN↔PT-BR, human-translated
- **OpenSubtitles** (OPUS) — subtitle translations, higher volume
- **Linguee** — institutional and corporate translations

The contrast between literary translation (COMPARA) and subtitle/institutional translation is itself analytically relevant: preliminary results suggest that human literary translators resist the loan forms more consistently than high-volume translation contexts.

---

## Annotation Guidelines

### General principles

Each data point is a Reddit comment containing at least one query term. Manual annotation assigns one of four categories:

| Category | Description |
|---|---|
| `relevant` | The comment uses the term in the target sense under investigation |
| `irrelevant` | The term is used in a different sense, outside the scope of this study |
| `ambiguous` | Context is insufficient to determine the sense |
| `excluded` | Duplicate, bot content, or unintelligible text |

Annotation is performed on the `body` field. The `permalink` field links to the original Reddit thread for cases where surrounding context is needed.

---

### Term-specific guidelines: *apply / aplicar / candidatar-se / inscrever-se*

#### Target sense

The target sense is the submission of an application to a job posting, internship, or formal professional selection process (*processo seletivo*). This corresponds to the English *to apply for a position*, for which BP has no single-word native equivalent in common use beyond *candidatar-se*.

#### Lexicographic basis

The *Dicionário Houaiss da Língua Portuguesa* lists the following senses for the three relevant verbs:

**aplicar** — (1) to place upon, to affix; (2) to impose, to inflict; (3) to strike physically; (4) to concentrate, to direct (attention, effort); (5) to assign, to confer; (6) to employ, to make use of; (7) to devote oneself to; (8) to inject (medication); (9) to invest (capital); (10) to prescribe (medication). 
*No acceptation related to submitting an application for a professional position.*

**inscrever** — (1) to engrave; (2) to register, to enter one's name in a list or competition; (3) to place oneself among others of the same kind; (4) to write, to annotate.
*Sense 2 covers enrollment in competitions and waiting lists but does not specifically denote professional job applications.*

**candidatar** — (1) to present or indicate someone as a candidate; (2) to become or declare oneself a candidate. 
*This is the only verb whose definition directly covers the target sense.*

The absence of the target sense from all Houaiss entries for *aplicar* constitutes the lexicographic evidence for the semantic loan: the form exists in Portuguese, but the meaning is borrowed from English *apply*.

#### Annotation decisions for *apply*

**Mark as `relevant`** when the comment describes submitting an application to a job posting, trainee program, internship, or formal selection process such as an university programme, regardless of which verb is used (*apliquei*, *me candidatei*, *me inscrevi*). The criterion is functional: the action described should be aligned to that of *candidatar-se*.

Examples of relevant contexts: mention of *vaga*, *processo seletivo*, *entrevista*, *empresa*, *LinkedIn*, *currículo*, *recrutamento*, *júnior/pleno/sênior*, *job*.

**Mark as `irrelevant`** when:

- *aplicar* is used in any Houaiss-attested sense: applying a formula, patch, fine, injection, investment, method, or physical force (*apliquei a fórmula*, *aplicou o patch*, *aplicou uma multa*)
- *candidatar-se* refers to political candidacy (*candidatou-se a vereador*, *candidatura ao governo*)
- *inscrever-se* refers to subscribing to a YouTube channel, newsletter, or online community (*se inscreva no canal*, *me inscrevi no sub*) — this reflects the English *subscribe*, not *apply*
- The comment is about exam enrollment

**Mark as `ambiguous`** when the verb appears without sufficient context to determine whether a job application or another sense is intended.

**Mark as `excluded`** when an already collected data point is referred and the verb is not used again by the author of the comment.

---

## Status

- [x] Data collection scripts (Arctic Shift API, TMX corpora)
- [x] Colab notebook for pre-filtering and diachronic analysis
- [x] Raw data collected for *apply* (multiple date ranges)
- [ ] Manual curation in progress (*apply*)
- [ ] Data collection for remaining terms
- [ ] Diachronic analysis and visualization
- [ ] Write-up

---

## Tools and dependencies

```
pip install requests
```

The analysis notebook runs in Google Colab without additional installation. TMX corpus scripts require Python 3.10+ (standard library only).

---

## References

- Houaiss, A. & Villar, M. de S. (2001). *Dicionário Houaiss da Língua Portuguesa*. Objetiva.
- Arctic Shift. (n.d.). Reddit data archive and API. https://arctic-shift.photon-reddit.com
- Linguateca. (n.d.). COMPARA: Portuguese-English parallel corpus. https://www.linguateca.pt/COMPARA
