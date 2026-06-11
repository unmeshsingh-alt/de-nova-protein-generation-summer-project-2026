# De Novo Protein Design with FoldArchitect

This repository contains scripts, XML protocols, and study materials for designing novel protein topologies *de novo* using Rosetta's FoldArchitect framework. The project focuses on learning the framework through a literature review, recreating a Ferredoxin fold, and independently designing massive, multi-subunit helical bundles.

## Project Workflow & Structure

### Phase 1: Literature Review & Study Guides
Before writing code, we conducted a deep dive into the 2022 FoldArchitect paper from the Baker Lab.
- **Key Resources**: 
  - `FoldArchitect_Baker.pdf`: The foundational paper.
  - `FoldArchitect_paper_and_code_study_guide.docx`: Comprehensive study guide breaking down the terminology and Bayesian modeling.
  - `ferodoxin_explanation.txt`: A detailed line-by-line explanation of the XML framework, including the biophysical logic behind constraint distances, loop entropies, and secondary structure packings.

### Phase 2: Ferredoxin Fold Generation
Designing a classic α/β sandwich (4-stranded beta-sheet packed against 2 alpha-helices).
- **Backbone Generation**: `ferodoxin.xml` uses the `DivideAndConqueror` algorithm to fold the topology dynamically.
- **Sequence Design**: `ferredoxin-sequence-design.xml` and `run_ferredoxin_seq_design.sh` are used to pack the hydrophobic core and design the amino acid sequence onto the generated backbone using `LayerDesign`.

### Phase 3: Multi-Subunit Helical Bundles
Scaling up a custom 2-helix hairpin subunit into massive arrays. 
- **The Prototype**: `2helix-large-11A-bb-generation.xml` (A single 2-helix hairpin packed at 11.0 Å).
- **The Linker Test**: `4helix-2subunit-bb-generation.xml` (Testing the inter-subunit linking loops and packing).
- **The Final Array**: `12helix-6subunit-bb-generation.xml` (A massive 300-residue, 6-subunit array utilizing single-digit constraint indexing to bypass XML schema limitations).
- **Sequence Design**: `2helix-sequence-design.xml` and `run_sequence_design.sh`.

### Phase 4: Outputs and Analysis
- **PDBs**: Generated backbones are saved as `S_000*.pdb`.
- **Scripts**: `extract_sequences.py` is used to pull FASTA sequences from the final designed PDBs.

---

## How to Run
All `.xml` files are designed to be run using `rosetta_scripts`. 
Example command for backbone generation:
```bash
rosetta_scripts.default.linuxgccrelease -parser:protocol <filename>.xml -nstruct 100 -out:prefix S_
```
