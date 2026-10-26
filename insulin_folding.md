# Insulin: How a Protein Folds into Its Working Shape
Insulin is a small protein hormone used as a remedy for diabetes. It is made of two chains (A and B) that fold and lock together with disulfide bonds. Here we load its real experimental structure, color its helices, highlight its disulfide bonds, and compare it with an AlphaFold prediction.

## 1. Setup

**Code cell 1** (tap + Code in Colab, paste, run):

```python
!pip install py3Dmol requests -q
```

**Code cell 2** (tap + Code in Colab, paste, run):

```python
import requests, py3Dmol

def fetch(url):
    r = requests.get(url, timeout=30)
    r.raise_for_status()
    return r.text
```

## 2. Load the experimental structure (PDB: 4INS)
The Protein Data Bank stores structures solved by X-ray crystallography.

**Code cell 3** (tap + Code in Colab, paste, run):

```python
pdb_text = fetch("https://files.rcsb.org/download/4INS.pdb")

chains = {}
for line in pdb_text.splitlines():
    if line.startswith("ATOM") and line[12:16].strip() == "CA":
        chains.setdefault(line[21], 0)
        chains[line[21]] += 1
print("Chains and residue counts:", chains)
```

## 3. Secondary structure and disulfide bonds

**Code cell 4** (tap + Code in Colab, paste, run):

```python
helix = [l for l in pdb_text.splitlines() if l.startswith("HELIX")]
sheet = [l for l in pdb_text.splitlines() if l.startswith("SHEET")]
ssbond = [l for l in pdb_text.splitlines() if l.startswith("SSBOND")]
print("Helices:", len(helix))
print("Sheet strands:", len(sheet))
print("Disulfide bonds:", len(ssbond))
```

## 4. Interactive 3D view
Helices, sheets and loops are colored by type; yellow sticks are the disulfide bonds that hold the chains together.

**Code cell 5** (tap + Code in Colab, paste, run):

```python
view = py3Dmol.view(width=500, height=450)
view.addModel(pdb_text, "pdb")
view.setStyle({"cartoon": {"colorscheme": "ssJmol"}})
view.addStyle({"resn": "CYS"}, {"stick": {"colorscheme": "yellowCarbon"}})
view.zoomTo()
view.show()
```

## 5. Color by chain

**Code cell 6** (tap + Code in Colab, paste, run):

```python
view = py3Dmol.view(width=500, height=450)
view.addModel(pdb_text, "pdb")
view.setStyle({"cartoon": {"colorscheme": "chain"}})
view.zoomTo()
view.show()
```

## 6. Compare with AlphaFold
AlphaFold predicts structure from the amino acid sequence alone. Its insulin entry (UniProt P01308) is the full precursor, preproinsulin, so it includes extra pieces that are cut away in mature insulin.

**Code cell 7** (tap + Code in Colab, paste, run):

```python
info = requests.get("https://alphafold.ebi.ac.uk/api/prediction/P01308", timeout=30).json()[0]
af_text = fetch(info["pdbUrl"])

grid = py3Dmol.view(width=800, height=400, viewergrid=(1, 2))
grid.addModel(pdb_text, "pdb", viewer=(0, 0))
grid.setStyle({"cartoon": {"colorscheme": "chain"}}, viewer=(0, 0))
grid.addModel(af_text, "pdb", viewer=(0, 1))
grid.setStyle({"cartoon": {"color": "spectrum"}}, viewer=(0, 1))
grid.zoomTo()
grid.show()
```

- **Left:** experimental structure (4INS)
- **Right:** AlphaFold prediction (rainbow from start to end)

The helical core matches well. Differences come from the precursor's extra segments and from experiments showing a stable, assembled form.

## What this shows about folding
- The amino acid sequence determines the 3D shape.
- Helices and disulfide bonds stabilize insulin's compact core.
- A misfolded protein cannot do its job, which is why folding matters in medicine.
