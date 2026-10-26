# Remedy Structure Explorer

Visualizing, docking, and simulating common remedies and their protein targets, all in Google Colab. The project starts with a simple molecule (aspirin) and builds up to how it binds to its target enzyme, COX-1, and how drugs differ between COX-1 and COX-2.

## Notebooks

Click a badge to open the notebook in Colab.

| Notebook | What it does | Open |
|---|---|---|
| aspirin_structure | 2D and 3D structure of aspirin, properties, functional groups | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/adonaytetemke-wq/aspirin-structure-/blob/main/aspirin_structure.ipynb) |
| insulin_folding | Insulin protein structure, helices, disulfide bonds, AlphaFold comparison | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/adonaytetemke-wq/aspirin-structure-/blob/main/insulin_folding.ipynb) |
| aspirin_cox1_docking | Docking aspirin into COX-1 with AutoDock Vina, validated by re-docking | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/adonaytetemke-wq/aspirin-structure-/blob/main/aspirin_cox1_docking.ipynb) |
| aspirin_cox1_md | Molecular dynamics of the aspirin-COX-1 complex in water (OpenMM, GPU) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/adonaytetemke-wq/aspirin-structure-/blob/main/aspirin_cox1_md.ipynb) |
| cox_selectivity_docking | Seven remedies docked into COX-1 and COX-2, compared to known selectivity | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/adonaytetemke-wq/aspirin-structure-/blob/main/cox_selectivity_docking.ipynb) |

## Why aspirin's structure matters

| Part | Role |
|---|---|
| Benzene ring | Rigid, flat backbone |
| Carboxylic acid | Acidity, solubility, binding |
| Ester (acetyl group) | Transfers to the COX enzyme, blocking pain and inflammation signals |

## Results

*Add your own numbers and images after running the notebooks.*

- Docking validation: re-docked ibuprofen RMSD = ___ Å
- Aspirin docking score: ___ kcal/mol; residues contacted: ___
- MD: mean aspirin RMSD = ___ Å over ___ ps
- Selectivity: mean score difference for COX-2-selective drugs = ___ kcal/mol

## What I learned

*Write 3 to 4 honest sentences, for example: what worked, what surprised you, and where the methods fall short.*

## How to run

1. Click a badge above.
2. In Colab choose **Runtime, Run all**.
3. The MD notebook needs a GPU: Runtime, Change runtime type, T4 GPU.

## Tools

Python, RDKit, py3Dmol, AutoDock Vina, OpenMM, MDTraj. Structures from the RCSB Protein Data Bank.

## Limitations

Docking and short MD runs are approximate. Rigid receptors, no heme or water in docking, and aspirin's covalent binding is not modeled. Results show plausible binding, not proof.

## License

MIT
