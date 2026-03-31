# 🦉 OFreq

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux%20%2F%20Windows-informational?style=flat-square&logo=linux&logoColor=white&color=0a0c10"/>
  <img src="https://img.shields.io/badge/Category-OCipher%20%2F%20Cryptanalysis-cyan?style=flat-square"/>
  <img src="https://img.shields.io/badge/No%20Dependencies-Stdlib%20Only-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-1.0-cyan?style=flat-square"/>
</p>

> **OFreq** is a frequency analysis and cryptanalysis tool — letter frequency tables, Index of Coincidence, chi-squared fitness, Kasiski examination, N-gram analysis, and Caesar brute-force with English scoring, to aid breaking classical ciphers.

---

## 📌 Overview

OFreq applies statistical cryptanalysis to ciphertext, helping identify the cipher type and providing actionable hints for manual breaking. Each module accepts typed/pasted text or a file and outputs results with colour-coded bars, reference comparisons, and JSON reports.

---

## 🖥️ Modules

| # | Module | Description |
|---|--------|-------------|
| **[1] Full Analysis** | Letter frequency table vs English · IC · Chi-squared · top-10 bigrams · top-8 trigrams · substitution mapping hint |
| **[2] Kasiski Test** | Find repeated 3–6 letter sequences and compute GCD spacings to estimate Vigenère key length · IC-based column analysis for key lengths 1–20 |
| **[3] Caesar Brute Force** | Try all 25 shifts, score each with chi-squared vs English, rank by fitness — best candidate shown with decrypted preview |
| **[4] N-gram Analysis** | Top-15 bigrams, trigrams, and tetragrams with ★ markers for known English patterns |
| **[5] IC Quick Check** | Index of Coincidence with interpretation, language detection, and per-column IC for key lengths 1–8 |

---

## 📊 Key Metrics

| Metric | Value | Interpretation |
|--------|-------|----------------|
| **IC** | ≥ 0.065 | English plaintext or monoalphabetic cipher (Caesar, simple substitution) |
| **IC** | ≈ 0.050 | Vigenère with short key (2–3) or weak encryption |
| **IC** | ≈ 0.040 | Polyalphabetic (Vigenère) with moderate key length |
| **IC** | ≈ 0.038 | Near-random — OTP, stream cipher, or transposition |
| **Chi²** | < 50 | Good English fitness |
| **Chi²** | 50–200 | Partial match |
| **Chi²** | > 200 | Poor English match |

---

## 🌍 Language IC Reference

OFreq compares the observed IC against 6 language profiles to suggest the most likely source language:

| Language | Expected IC |
|----------|------------|
| German | 0.0762 |
| French | 0.0778 |
| Spanish | 0.0752 |
| Italian | 0.0738 |
| English | 0.0667 |
| Random | 0.0385 |

---

## 🔍 Reference Data

OFreq uses the following built-in English reference tables:

- **Letter frequencies** — 26 letters with standard English % (E=12.70%, T=9.06%, A=8.17% … Z=0.07%)
- **Common bigrams** — 24 English bigrams (TH, HE, IN, ER, AN, RE, ON …)
- **Common trigrams** — 14 English trigrams (THE, AND, ING, ION, ENT …)

Bigrams and trigrams found in the ciphertext are flagged with ★ in the output.

---

## 💡 Substitution Hint

Module [1] outputs a frequency-rank substitution mapping — the most frequent ciphertext letter is mapped to E, second to T, and so on. This provides a starting point for manual substitution cipher breaking.

---

## 📋 Workflow — Breaking a Classical Cipher

```
1. Run Full Analysis    → check IC value
2. IC ≈ 0.067          → monoalphabetic → use substitution hint + bigrams
3. IC ≈ 0.050          → polyalphabetic → run Kasiski Test
4. Get key length      → analyse each column separately
5. Confirm with        → N-gram Analysis (match ★ bigrams/trigrams)
```

---

## 📤 Output

JSON reports saved to `ofreq_output/`:

```
ofreq_output/ofreq_full_YYYYMMDD_HHMMSS.json
```

Each report contains: text length, IC, chi-squared, language, per-letter frequencies, substitution hint mapping, top-10 bigrams, top-8 trigrams.

---

## ⚙️ Requirements

- **Linux or Windows**
- **No Python installation needed** — runs as a standalone executable
- **No external dependencies** — stdlib only

---

## 🚀 Usage

```bash
./OFreq
```

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 300+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

MIT License — © Khaled S. Haddad

*Tools are distributed as pre-built executables. Source code is proprietary.*
