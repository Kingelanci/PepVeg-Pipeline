# PepVeg-Pipeline

ESM-2-based screening of plant- and fungi-derived peptide libraries against a protein target. Developed for the MDM2 case study.

## What it does

1. Loads plant/fungi proteomes (FASTA)
2. In silico enzymatic hydrolysis with 6 proteases (trypsin, pepsin, chymotrypsin, papain, bromelain, alcalase)
3. Biochemical pre-filter (Boman, GRAVY, charge, instability, MW, hydrophobicity)
4. ESM-2 cosine-similarity mining against a reference peptide (`facebook/esm2_t33_650M_UR50D`)
5. 7-parameter binding score (3 target-specific + 4 generic)
6. Export of ranked candidates as YAML/FASTA for downstream 3D co-folding
7. GROMACS molecular dynamics on the target-peptide complex (CHARMM36m, 310 K)

## Notebooks

- `PepVeg_Pipeline_v10.ipynb` — full screening pipeline
- `PepVeg_Pipeline_v10_SingleFilter.ipynb` — applies each biochemical filter independently on the raw hydrolysate (six standalone pass counts)
- `GROMACS_MD_setup_CHARMM36m.ipynb — GROMACS MD setup and analysis on RunPod GPU

## Requirements

Python 3.9+, GPU (NVIDIA T4 minimum). Pinned dependencies are installed by STEP 0 of each notebook; see `requirements.txt`.

`transformers` is pinned to 4.44.2 — newer versions require `torch ≥ 2.5`.

## Input

Proteome archive contains FASTA files from UniProt https://zenodo.org/records/20447996

## Usage

1. Place `db_*.tar.gz` in `/workspace/` (RunPod) or `/content/` (Colab)
2. Run STEP 0 to install pinned dependencies
3. Restart the kernel
4. Run STEP 0b and select database(s) and target(s) from the interactive menu
5. Execute the remaining cells in order

## License

MIT.
