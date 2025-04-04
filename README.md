# Rewriting Stories with LLMs: Gender Bias in Generated Portuguese-language Narratives

This repository contains the corpus used in the Journal of the Brazilian Computer Society (JBCS 2025) article: *"Rewriting Stories with LLMs: Gender Bias in Generated Portuguese-language Narratives"*. The curated corpus of Portuguese-language literary works is designed for studying gender bias in character-driven narratives. The corpus is constructed from multiple public-domain sources, ensuring diversity in historical periods and literary styles.

## 📚 Corpus Construction

To build a representative dataset of Portuguese literary works, we selected four publicly available corpora that include novels, short stories, and other narrative texts written in both Brazilian and European Portuguese:

- **Colonia** ([Zampieri et al., 2013](https://aclanthology.org/Q17-1010/))  
- **ELTeC-por** ([ELTeC Project](https://doi.org/10.5281/zenodo.4288235))  
- **OBras (Obras Brasileiras)** ([Santos et al., 2018](http://hdl.handle.net/10400.26/31830))  
- **PPORTAL** ([Silva et al., 2022](https://sol.sbc.org.br/index.php/jidm/article/view/19483))

These corpora cover different historical periods, as shown below:

| Corpus       | Period       | # Works |
|--------------|--------------|---------|
| Colonia      | 1844–1948    | 35      |
| ELTeC-por    | 1844–1973    | 37      |
| OBras        | 1855–1984    | 23      |
| PPORTAL      | 1804–1998    | 497     |
| **Total**    | **1804–1998**| **592** |

Initially, we extracted **840** literary works. After filtering out non-narrative genres (e.g., poetry and plays), we retained **592** works composed of character-driven narratives.

## 🛠️ Preprocessing Pipeline

We applied the preprocessing pipeline proposed by [Silva et al., 2024](https://github.com/marianaossilva/gender_pipeline) to each text:

1. **Text Cleaning and Sentence Segmentation**
2. **Entity Recognition:** Detection of `PERSON` entities (i.e., any character explicitly mentioned in the narrative).
3. **Gender Labeling:** Gender inference for each `PERSON` entity.

The result is a structured version of each text with sentences annotated for named entities and gender.

## 🔎 Sentence Filtering for LLM Evaluation

To prepare data for language model probing and generation tasks, we applied the following filters:

- Removed **short sentences** (fewer than 5 tokens).
- Retained only sentences where the `PERSON` entity:
  - Is a **proper noun** (`PROPN`)
  - Functions as a **nominal subject** or **direct object**
- Removed sentences with **explicit gender markers**, such as:
  - Pronouns (`ele`, `ela`)
  - Possessives (`dele`, `dela`)

These criteria help ensure sentences are semantically rich and suitable for gender inference by large language models without biasing linguistic cues.

## 📊 Final Corpus Stats

- **Works:** 592  
- **Sentences (filtered):** 28,317  
- **Tokens:** 774,516  

Each literary work contributes up to **100 sentences**, ensuring a balanced distribution while keeping the corpus computationally manageable.

## 📁 Folder Structure

```
llm_gender
┣ 📂raw_texts/ # Original texts from each corpus 
┣ 📂processed/ # Preprocessed and sentence-segmented versions  
┣ 📜metadata.csv # Metadata for each literary work 
┗ 📜README.md # This file
```
