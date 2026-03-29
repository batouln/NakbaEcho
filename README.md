# NakbaEcho Dataset

**From Oral Testimonies to a Transcribed Arabic History Corpus**

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Paper](https://img.shields.io/badge/Paper-LREC%202026-blue.svg)](#citation)

NakbaEcho is a large-scale transcribed dataset of Palestinian oral history interviews documenting the 1948 Nakba. The resource is constructed from over **2,180 hours** of recorded testimonies gathered through the [Palestine Remembered](https://www.palestineremembered.com/index.html) oral history index and linked to multiple repositories.

---

## Dataset Overview

| Statistic | Value |
|---|---|
| Total interviews | 708 |
| Total duration | ~2,180 hours |
| Total tokens | 12.85M |
| Total segments (exchanges) | 1,051,160 |
| Named entities extracted | 747,632 |
| Villages covered | 239 |
| Historical districts | 14 |
| Narrators | 719 |
| Median narrator birth year | 1929 |
| Micro-averaged WER | 7.00% |

### Sources

| Source | Interviews | Duration (mins) | Recording Period |
|---|---|---|---|
| POHA | 349 | 25,852 | 1994–2009 |
| YouTube / PalRemembered | 323 | 104,927 | 2003–present |
| Zochrot | 36 | — | 2002–present |
| **Total** | **708** | **130,779** | |

### Narrator Demographics

- **Gender:** 74.5% male / 25.5% female (at narrator level)
- **Birth years:** 1897–1962 (median 1929; 83.8% born 1920–1939)
- Gender labels validated via cross-method agreement (name-based vs. voice-based): **98.6% agreement**

---

## Repository Structure

```
NakbaStory/
├── README.md
├── LICENSE
├── paper/                     # LaTeX source and figures
│   ├── nakbaecho.tex
│   ├── lrec2026-example.bib
│   └── figures/
├── data/
│   ├── transcripts/           # 708 transcript .txt files
│   └── metadata/              # Narrator and interview metadata CSVs
├── scripts/                   # Analysis and processing scripts
│   ├── nakba_analysis_v3.py
│   ├── extract_clips.py
│   ├── wer_final.py
│   └── corpus_wer_report.py
└── .gitignore
```

---

## Transcript Format

Each transcript file contains structured segments with the following fields:

```
# GLOBAL SPEAKERS
SPEAKER_01 | Male | neutral | "elderly male, clear voice"
SPEAKER_02 | Female | sad | "elderly female, soft voice, slow pace"

# TRANSCRIPT
[00:01:31.000 → 00:01:37.000] SPEAKER_01 [EMO:neutral]
عمي تسمح لنا نباشر بأسئلة القسم الأول؟

[00:12:13.000 → 00:12:17.000] SPEAKER_02 [EMO:happy]
طيب. يا سيدي الله يديم عليك الصحة والعافية إن شاء الله.
```

Each segment includes:
- **Timestamps** — absolute position in `HH:MM:SS.mmm` format
- **Speaker label** — diarized speaker ID with gender
- **Emotion** — model-inferred label (neutral, sad, happy, angry, fear, tired)
- **Thematic flags** — boolean indicators for Nakba, Jews/Israel, and British Mandate mentions

---

## Annotations

All annotations are **automatically generated** and should be treated as exploratory:

- **Emotion labels** — assigned per segment by the transcription model
- **Named entities** — extracted via CAMeL-Lab Arabic BERT (LOC, PERS, ORG, MISC)
- **Thematic mention flags** — Nakba, Jews/Israel, British Mandate
- **Speaker metadata** — gender, voice signature

> ⚠️ These are not manually validated ground-truth labels. See the paper for detailed discussion of limitations.

---

## Transcription Pipeline

Transcription was performed using the **Gemini 2.5 Pro API** configured for dialectal Palestinian Arabic with the following constraints:

- No content invention; unintelligible speech marked as `[inaudible]`
- Dialect preserved as spoken (no MSA normalization)
- Proper nouns retained without correction
- Absolute timestamps required for each segment

See [Appendix E](paper/) in the paper for the full prompt and output schema.

---

## Ethical Considerations

This dataset is derived from oral testimonies documenting lived experiences of displacement and loss. The original language used by narrators—including historically situated terminology—is preserved as documentary evidence. Expressions such as اليهود reflect the context of the testimonies and should not be interpreted as generalized or decontextualized labels.

We encourage responsible use of this resource with attention to historical context and the limitations of automated processing.

---

## Citation

If you use this dataset, please cite:

```bibtex
@inproceedings{nakbaecho2026,
  title     = {The {NakbaEcho} Dataset: From Oral Testimonies to a Transcribed {Arabic} History Corpus},
  author    = {Author1 and Author2 and Author3},
  booktitle = {Proceedings of the 2026 Language Resources and Evaluation Conference (LREC)},
  year      = {2026},
  note      = {To appear}
}
```

---

## License

This work is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License](https://creativecommons.org/licenses/by-nc/4.0/).

You are free to share and adapt the material for non-commercial purposes, provided you give appropriate credit.

---

## Contact

For questions, feedback, or collaboration inquiries, please open an issue or contact the authors.
