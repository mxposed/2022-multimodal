# Environment setup

This project uses python 3.9. The dependencies are managed with pip-tools.
To recreate the virtual environment:

1. Create virtual environment: `python -mvenv venv`
2. Activate it: `source venv/bin/activate`
3. Install `pip-tools`: `pip install pip-tools`
4. Install dependencies: `pip-sync`

During step 4 you might need to provide some external dependencies / activate modules on quest.

# Contents

## CITE-seq analysis/predictions
1. `01_explore`: exploratory analysis of CITE-seq training RNA part
2. `02_explore_with_test`: exploratory analysis of CITE-seq training+test RNA part: no substantial batch effect between train and test
3. `03_scvi`: attempt to train scVI model on log-normalized counts of train+test RNA to obtain latent representation
4. `04_jax`: attempt to train simple autoencoder (AE) model on log-normalized counts of train+test RNA to obtain latent representations
5. `05_jax_predict`: catboost model to predict CITE-seq protein levels from simple AE latent representations, and submission

