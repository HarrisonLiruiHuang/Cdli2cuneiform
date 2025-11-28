# Crosslist Codebook

This repository contains code and a Jupyter notebook for building and checking a **crosslist codebook** that aligns cuneiform signs across multiple sign lists.

## Overview

The project takes several published sign lists (e.g., OSL and others), matches their entries, and produces a single, consolidated **codebook**.  
The codebook serves as a master dictionary that assigns stable IDs to signs and records how each list refers to them.

## Why Useful?

Different projects and editions use different sign lists and numbering systems. This makes it hard to:

- Compare analyses across corpora  
- Merge datasets that rely on different sign conventions  
- Track disagreements or ambiguous mappings  

The codebook provides:

- A **unified ID (qid)** for each proposed sign entry  
- A row-wise alignment of how each sign appears in each list  
- Flags and notes for **conflicting or uncertain** matches  

This makes downstream work (databases, visualization, quantitative analysis) more consistent and reusable.

## What the Codebook Contains

- **Core identifiers**  
  - Stable internal ID / `qid`  
  - Per-list IDs (e.g., OSL number, other list numbers)  
  - Sign names and variant labels  

- **Crosslist mappings**  
  - Columns for each sign list, showing which entry is matched  
  - Indicators for missing entries (sign appears in one list but not another)  

- **Quality and conflict fields**  
  - Flags where lists disagree about a mapping  
  - Columns used to track alternative proposals  
  - Notes used during manual review  

In short, each row represents a proposed “same sign” across lists, and the codebook records both the matches and the places where things do not line up cleanly.

## Method

The notebook `Crosslist_comparison.ipynb` is structured as:

1. **Data Description and Setup**  
   - Loads raw sign-list files  
   - Documents original sources (with link back to the COMPASS notebook)

2. **Sign Lists Crosslist Dictionary**  
   - **Sign lists prepping**: cleaning columns, normalizing IDs, basic checks  
   - **Cross list sign matching & qid matching**: core matching logic  
     - Using one list (e.g., OSL) as the starting point  
     - Re-running matches with other lists as the starting point  
   - **Signlist proposal**: constructing the proposed master signlist/codebook  
   - **Conflict finding**: identifying values with different corresponding signs  

Running through these sections produces the final codebook and diagnostic tables.

## Key Output Files

- `cross_list_sign_comparison.csv` – main crosslist comparison of signs across all lists  
- `cross_list_value_comparison.csv` – comparison of specific values/attributes for matched signs  
- `proposed_signlist.csv` – final proposed unified signlist/codebook with stable IDs and mappings  
- “Signlist Statistics” stacked bar chart showing, for each sign list, the number of matches with OSL and the number of non-empty matches  

## Information

**Dataset Sources:**  
OSL (ogsl): https://raw.githubusercontent.com/oracc/osl/master/00lib/osl.asl  

Nuolenna: https://github.com/tosaja/Nuolenna/blob/master/sign_list.txt  

Akkademia: https://github.com/gaigutherz/Akkademia/blob/master/cuneiform_to_unicode_fixed.csv  

TextFabric: https://github.com/Nino-cunei/oldbabylonian/blob/master/sources/writing/GeneratedSignList.json  

CuneiML: https://github.com/taineleau/CuneiML/blob/main/cuneiform_unicode/cuneiform_vocab.txt  

**Acknowledgments:**  
Special thanks to Dr. Adam Anderson at FactGrid for their guidance and support throughout this project!
