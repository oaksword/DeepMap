# DeepMap

An elegant method for single-cell data integration.

# Installation

It is advisable to download DeepMap from GitHub. Below is an illustration of the installation process.

1. Open a terminal and establish a new environment in anaconda (optional).

```bash
conda create -n deepmap python=3.7
```

2. Activate the new environment `deepmap` (optional).

```bash
conda activate deepmap
```

3. Obtain source code from GitHub.

```bash
git clone https://github.com/oaksword/DeepMap.git
```

4. Execute the installation with `pip`. The dependencies will be installed automatically.

```bash
cd DeepMap
tar -xvf deepmap-0.1.tar.gz
pip install deepmap-0.1/
```

# Usage

DeepMap reveives an `anndata` object containing all the datasets to be integrated and outputs an `anndata` object of integrated datasets. A basic example is presented below.

```python
model = DeepMap()
model.preprocess(adata, batch_key='batch')
model.integrate()
```

The result datasets are aggregated into `model.integrated`.

Key parameters of `DeepMap.__init__()`:
- `metric`: The metric employed for performing cell matching (`cosine` by default).
- `k`: The number of neighbors for each cell (`10` by default).
- `mnn_only`: Merely preserve MNN pairs or not (`False` by default).
- `device`: Use GPU (specified as `cuda`) or CPU (specified as `cpu`) for optimization. If this parameter is not specified, GPU will be used when `torch.cuda.is_available()` returns `True`.

Key parameters of `DeepMap.preprocess()`:
- `batch_key`: The attribute in columns of `anndata.obs` that indicates the resources of cells (`batch` by default).
- `gene_num`: The number of highly variable genes selected for each dataset (`4000` by default).
- `scale`: Scale datasets by column or not (`True` by default). We recommend to set `scale=False` when integrating scATAC-seq datasets.

Key parameters of `DeepMap.integrate()`:
- `dim`: The dimension of latent space (`20` by default).
- `n_reconstructs`: The number of reconstructions (`5` by default).
- `beta`: The parameter balancing mixing and original structure preservation (`0.1` by default).

# Demos

Examples of typical demos can be located within the [examples](https://github.com/oaksword/DeepMap-reproducibility/tree/main/examples) directory. Kindly execute the code located in the [preprocessing](https://github.com/oaksword/DeepMap-reproducibility/tree/main/preprocessing) directory initially to obtain the datasets.
