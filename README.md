# Virtual Screening Molecule Generator Using Python and RDKit

**An end-to-end computational chemistry workflow for generating molecular analogues from a parent compound using functional-group substitution, calculating molecular descriptors, applying preliminary drug-likeness filters, and exporting candidate molecules for downstream virtual screening.**

🎥 Future Omics — Bioinformatics Made Easy For more bioinformatics, genomics, and omics tutorials:

📺 Future Omics — Bioinformatics Made Easy 📺 Future Omics — Bioinformatics Made Easy https://www.youtube.com/@Bioinformatics_Made_Easy?sub_confirmation=1

The channel focuses on simplified bioinformatics and omics tutorials for students, researchers, and life-science learners.

## Overview

The Virtual Screening Molecule Generator is a Python-based cheminformatics workflow designed to explore structural analogues of a parent compound. Users provide a parent molecule as a SMILES string and select functional groups to generate candidate derivatives.

The workflow uses **RDKit** for molecular structure manipulation, chemical validation, descriptor calculation, visualization, and molecular file export. It is designed to run in Google Colab without requiring a local chemistry software installation.

## Key Features

- Parent compound input using SMILES notation.
- Functional-group substitution at aromatic carbon–hydrogen positions.
- Generation of single-substitution analogues and configurable sequential substitutions.
- Chemical structure sanitization and duplicate removal.
- Molecular descriptor calculation.
- Preliminary Lipinski Rule of Five and TPSA filtering.
- QED-based drug-likeness assessment.
- Visualization of generated molecular structures.
- Export of molecular libraries in CSV and SDF formats.
- Google Colab-compatible execution.

## Workflow

```text
Parent Compound (SMILES)
          |
          v
Molecular Structure Validation
          |
          v
Functional-Group Selection
          |
          v
Analogue Generation Using RDKit
          |
          v
Chemical Validation and Deduplication
          |
          v
Molecular Descriptor Calculation
          |
          v
Preliminary Drug-Likeness Filtering
          |
          v
Molecular Visualization
          |
          v
CSV and SDF Export
```

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Workflow implementation |
| RDKit | Cheminformatics and molecular manipulation |
| Pandas | Data management and CSV export |
| Matplotlib | Visualization support |
| Google Colab | Cloud-based notebook execution |

## Functional Groups Supported

The example configuration includes:

- Fluoro
- Chloro
- Methyl
- Methoxy
- Hydroxyl
- Amino
- Cyano
- Carboxamide
- Trifluoromethyl
- Acetyl

The functional-group library can be modified by editing the reaction SMARTS definitions in the notebook.

**Scope:** The included transformations target aromatic C–H sites. They do not constitute a general-purpose functional-group replacement engine.

## Molecular Descriptors

The workflow calculates the following properties for generated molecules:

| Descriptor | Description |
|---|---|
| Molecular Weight | Average molecular mass |
| Exact Mass | Monoisotopic molecular mass |
| LogP | Estimated octanol–water partition coefficient |
| TPSA | Topological polar surface area |
| HBD | Hydrogen-bond donors |
| HBA | Hydrogen-bond acceptors |
| Rotatable Bonds | Number of rotatable bonds |
| Heavy Atoms | Number of non-hydrogen atoms |
| Formal Charge | Net formal molecular charge |
| QED | Quantitative Estimate of Drug-likeness |
| Ring Count | Number of rings identified by RDKit |

These descriptors support preliminary compound prioritization but do not establish pharmacological activity, safety, or clinical suitability.

## Installation

Run the following command in Google Colab:

```python
%pip install rdkit pandas matplotlib
```

The notebook contains the complete workflow, including installation, molecular generation, filtering, visualization, and export.

## How to Run

1. Download the Jupyter notebook from this repository.
2. Open [Google Colab](https://colab.research.google.com/).
3. Select **File → Upload notebook**.
4. Upload `End_to_End_Virtual_Screening_Molecule_Generator.ipynb`.
5. Run the installation and import cells.
6. Enter your parent compound's name and SMILES.
7. Configure the desired functional groups.
8. Set the maximum substitution rounds and library size.
9. Run the remaining cells sequentially.
10. Review the generated molecules and download the output files.

### Example Input

The notebook uses aspirin as a demonstration parent compound.

```python
PARENT_NAME = "Aspirin_demo"
PARENT_SMILES = "CC(=O)Oc1ccccc1C(=O)O"
```

Replace these values with the structure you want to investigate.

### Configuration

```python
MAX_SUBSTITUTIONS = 1
MAX_MOLECULES = 5000
```

- `MAX_SUBSTITUTIONS = 1`: Generates single-substitution analogues.
- `MAX_SUBSTITUTIONS = 2`: Also explores sequential two-substitution combinations.
- `MAX_MOLECULES`: Sets a safety cap on the number of unique structures.

Increasing the substitution rounds may substantially increase the number of generated structures.

## Drug-Likeness Filtering

The notebook applies configurable preliminary filters based on molecular weight, LogP, hydrogen-bond donors, hydrogen-bond acceptors, and TPSA.

Default thresholds:

| Property | Threshold |
|---|---:|
| Molecular Weight | ≤ 500 Da |
| LogP | ≤ 5 |
| HBD | ≤ 5 |
| HBA | ≤ 10 |
| TPSA | ≤ 140 Å² |

The implementation applies a four-of-five Lipinski-style rule and an additional TPSA cutoff. These are heuristic filters, not universal acceptance criteria.

## Output Files

The notebook produces the following files:

| File | Description |
|---|---|
| `virtual_screening_library.csv` | Complete unique molecular library and descriptors |
| `filtered_virtual_screening_library.csv` | Candidates passing the configured preliminary filters |
| `virtual_screening_library.sdf` | Molecular structures and selected properties for the complete library |
| `filtered_virtual_screening_library.sdf` | Molecular structures and properties for filtered candidates |
| `virtual_screening_summary.csv` | Summary of input settings and generation results |

The CSV files are suitable for tabular analysis, while SDF files can be used with compatible molecular visualization and docking tools.

## Potential Applications

- Computational drug discovery
- Structure–property exploration
- Medicinal chemistry research
- Molecular library generation
- Preliminary compound prioritization
- Preparation of candidate libraries for molecular docking
- Development of downstream machine-learning workflows

## Limitations

- The current reaction library targets aromatic C–H substitutions.
- Generated structures may not be synthetically accessible or chemically stable.
- The workflow does not automatically optimize protonation states, tautomers, salts, or stereochemistry.
- Lipinski-style filters and QED scores do not predict target-specific biological activity.
- Molecular docking, ADMET prediction, toxicity assessment, and experimental validation are not included in the current notebook.
- Each generated structure should be reviewed for chemical plausibility before downstream use.

## Future Enhancements

Possible extensions include:

- Structure-aware substitution-site selection.
- Additional reaction templates and fragment libraries.
- Synthetic accessibility scoring.
- Molecular fingerprint similarity analysis.
- ADMET and toxicity prediction.
- Protein–ligand docking integration.
- Machine-learning-based activity prediction.
- Multi-objective candidate ranking.
- Integration with ChEMBL and PubChem compound data.

## Reproducibility

The workflow is notebook-based and uses configurable inputs, reaction templates, and filtering thresholds. For reproducible results, record the parent SMILES, RDKit version, functional-group definitions, substitution rounds, and filtering parameters for each run.

## Disclaimer

This project is intended for educational and research purposes in computational chemistry and drug discovery. Generated compounds and calculated descriptors are computational hypotheses and should not be interpreted as evidence of efficacy, safety, or suitability for human use.

## License

Choose a suitable open-source license before distributing the repository. For example, the MIT License may be appropriate if you want to permit reuse and modification with attribution, subject to its terms.

