# urban-strata-assets

External runtime assets for `urban-strata-core`.

This folder is referenced through `urban-strata-core/config/paths.json` and stores the datasets, derived ecological products, trained models, climate files, and static visualization assets used by the project.

Layout:

- `datasets/stack_samples/`
- `raw/ecology/plant_traits/`
- `raw/site/zlinsky/`
- `raw/site/zlinsky/regional_occurrence/`
- `derived/site_ecology/`
- `raw/climate/kunovice_tmy.epw`
- `models/checkpoints/`
- `assets/static_visualization/`

Model layout:

- `models/checkpoints/geometry_vae/model.pt`
- `models/checkpoints/slope_surrogate/model.pt`
- `models/checkpoints/wetness_surrogate/model.pt`
- `models/checkpoints/sun_surrogate/model.pt`
- each model folder also stores `metadata.json`

Suggested workflow:

- keep source code, notebooks, docs, and Grasshopper definitions in `urban-strata-core`
- keep reusable datasets and model artifacts here
- retraining a model rewrites its own model-family folder

## Data storage (DVC, since 2026-11-01)

The data folders (`assets`, `datasets`, `derived`, `models`, `raw`, `review_exports`) are tracked with
[DVC](https://dvc.org), not Git LFS. Git holds only the small `*.dvc` pointer files; the data lives in the DVC
remote `drive` = the Google Drive folder `My Drive/dvc-remotes/urban-strata-assets` (account jhorak@vsup.cz,
synced by Google Drive for Desktop).

- get the data: `dvc pull`
- after changing data: `dvc add <folder>` → `dvc push` → commit the changed `<folder>.dvc`
- on another machine with Drive mounted elsewhere: `dvc remote modify --local drive url "<path to that folder>"`
- install: `uv tool install dvc`
