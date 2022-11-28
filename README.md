# Environment setup

This project uses python 3.9. The dependencies are managed with pip-tools.

`requirements.in` file specifies packages needed by the project, with optional pins.

`requirements.txt` file records all resolved dependencies for the specified packages.

## Environment setup without GPU

To recreate the virtual environment:

1. Create virtual environment: `python -mvenv venv`
2. Activate it: `source venv/bin/activate`
3. Install `pip-tools`: `pip install pip-tools`
4. Install dependencies: `pip-sync`

## Environment setup on Quest with GPU

To enable support for GPU on Quest, I used 2 manually downloaded prebuilt python extensions: torch and jax, which I placed in the current root project directory.

To get them:

`wget "https://download.pytorch.org/whl/cu113/torch-1.12.1%2Bcu113-cp39-cp39-linux_x86_64.whl"`

`wget "https://storage.googleapis.com/jax-releases/cuda11/jaxlib-0.3.20+cuda11.cudnn82-cp39-cp39-manylinux2014_x86_64.whl"`

Then:

1. Create virtual environment: `python -mvenv venv`
2. Activate it: `source venv/bin/activate`
3. Install `pip-tools`: `pip install pip-tools`
4. Compile dependencies with the downloaded wheels: `pip-compile`
5. Check that only these files changed in `requirements.txt`: `git diff requirements.txt`
6. Install dependencies: `pip-sync`

After that, before launching `jupyter` or scripts, run `module load cuda/11.2.1-intel-19.0.5.281`

I use GPU nodes on Quest like this:
1. Schedule an interactive job on a node with GPU and enough memory (>150G)
2. Activate environment there
3. Launch jupyter lab
4. Use ssh port forwarding to connect my localhost port to GPU node port 8888
5. Open browser for the localhost port

# Contents

## CITE-seq analysis/predictions
1. `01_explore`: exploratory analysis of CITE-seq training RNA part
2. `02_explore_with_test`: exploratory analysis of CITE-seq training+test RNA part: no substantial batch effect between train and test
3. `03_scvi`: attempt to train scVI model on log-normalized counts of train+test RNA to obtain latent representation
4. `04_jax`: attempt to train simple autoencoder (AE) model on log-normalized counts of train+test RNA to obtain latent representations
5. `05_jax_predict`: catboost model to predict CITE-seq protein levels from simple AE latent representations, and submission

## ATAC-seq analysis/predictions

Exploratory analysis:  
TBD

AE-based models:

1. `10_atac_models`: train AE model per each chromosome, save models and latent dimensions
2. `11_atac_apply`: apply AE models to test data for each chromosome to get latent dimensions
3. `12_atac_predict`: train catboost models on train latent dimensions to predict mRNA levels
4. `13_atac_ae_explore`: explore AE training behaviour with changed in latent dimensions

Truncated SVD-based models:

1. `20_atac_models`: fit Truncated SVD per each chromosome, save top dimensions
2. `21_atac_apply`: apply SVD models per each chromosome to test data, save latent dimensions
3. `12_atac_predict`: train catboost models to predict mRNA from top SVD dimensions per chromosome
