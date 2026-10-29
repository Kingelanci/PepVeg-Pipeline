# legacy

Earlier versions of the pipeline, kept for the record. They are not the version reported
in the paper.

- `PepVeg_Pipeline_v10.ipynb` - hydrolyses the proteomes first and applies the
  pharmacophore afterwards, uses an instability-index filter and a 7-parameter binding
  score. None of the three is part of v19.
- `PepVeg_Pipeline_v10_SingleFilter.ipynb` - applies each biochemical filter
  independently on the raw hydrolysate.

The current pipeline is `PepVeg_Pipeline_v19.ipynb` in the repository root.
