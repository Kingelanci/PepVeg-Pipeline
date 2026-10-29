# PepVeg-Pipeline

ESM-2-based screening of plant- and fungi-derived peptide libraries against a defined
protein-protein interaction interface. Developed for the MDM2 case study (SPAFESTWDILK).

Reported in: Romiti M, Sandri C, Paiola G, Ashtiani M, "SPAFESTWDILK, a
plant-proteome-database-derived dodecapeptide from Zingiber officinale, as a predicted
MDM2-binding peptide: computational discovery and multi-method evaluation",
Computational and Structural Biotechnology Journal.

## What it does

`PepVeg_Pipeline_v19.ipynb` runs six stages, in this order:

1. Pharmacophore pre-screening of whole proteins - the F-x(3)-W motif with strict i/i+4
   spacing, applied to the proteomes before anything else
2. In silico enzymatic hydrolysis of the motif-carrying proteins only, with trypsin,
   bromelain, chymotrypsin, pepsin, alcalase and papain, keeping fragments of 6-20 residues
3. Physicochemical filtering - Boman index, GRAVY, net charge, molecular weight and
   hydrophobic fraction
4. ESM-2 ranking by cosine similarity to a reference peptide
   (`facebook/esm2_t33_650M_UR50D`)
5. Writes the AlphaFold 3 job files for the top-ranked candidates
6. Writes the GROMACS inputs for the MD triage

The notebook stops at the job files: co-folding and dynamics are run outside it, on the
AlphaFold 3 Server and on a GPU, and their results are in the Zenodo record below.

The instability-index filter and the 7-parameter binding score of v10 are not part of
v19: the filter was removed and the pipeline rerun. The stage order also differs - v10
hydrolyses first, v19 applies the pharmacophore first.

## Notebooks

- `PepVeg_Pipeline_v19.ipynb` - the pipeline of the paper. Start here.
- `GROMACS_MD_setup_CHARMM36m.ipynb` - GROMACS MD setup and analysis on a RunPod GPU
- `legacy/PepVeg_Pipeline_v10.ipynb` - earlier version, kept for the record
- `legacy/PepVeg_Pipeline_v10_SingleFilter.ipynb` - applies each biochemical filter
  independently on the raw hydrolysate

## Requirements

Python 3.9+, GPU (NVIDIA T4 minimum) for the ESM-2 stage. See `requirements.txt`.

`transformers` is pinned to 4.44.2 - newer versions require `torch >= 2.5`.

## Input

Proteome archive: 22 UniProt reference proteomes, https://doi.org/10.5281/zenodo.20447996

## Usage

1. Download the proteome archive and place it where the notebook can read it
2. Open `PepVeg_Pipeline_v19.ipynb`. The setup cell mounts Google Drive and reads from a
   fixed folder: if you are not on Colab, or your archive is elsewhere, set `DATA_DIR` at
   the top of that cell first
3. Run the setup cells, then the stage cells in order - each stage reads what the previous
   one wrote, so they are not interchangeable
4. Hydrolysis, the physicochemical filter and the ESM-2 stage write checkpoints and can be
   resumed if a session is interrupted

## Related works

Computational outputs of the case study - AF3 benchmark, structure predictions, GROMACS
trajectories, MM-PBSA decompositions, and the supplementary tables with the scripts that
rebuild them - are deposited at:

https://doi.org/10.5281/zenodo.19859570

This is the concept DOI: it always resolves to the latest version.

## License

PepVeg-Pipeline is licensed under the GNU General Public License v3.0 - Copyright (C) 2026  Sherman Tree Nutraceuticals S.r.l.
Permissions of this strong copyleft license are conditioned on making available complete source code of licensed works and modifications, which include larger works using a licensed work, under the same license. Copyright and license notices must be preserved. Contributors provide an express grant of patent rights.
