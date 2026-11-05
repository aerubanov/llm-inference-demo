# llm-inference-demo

Demonstrations of different LLM inference algorithms from research papers, implemented as runnable Jupyter notebooks.

## Setup

Requirements: [uv](https://docs.astral.sh/uv/) and Python 3.12 or newer (uv can install it for you).

```bash
git clone <repo-url>
cd llm-inference-demo

# create .venv and install all dependencies, including the dev group (JupyterLab, ipykernel, nbstripout, ruff)
uv sync

# one-time per clone: strip notebook outputs on commit (writes to .git/config)
uv run nbstripout --install

# launch notebooks
uv run jupyter lab
```

Then open a notebook from the `notebooks/` directory and run it top to bottom.

Notes:

- Notebooks that use a language model download it from Hugging Face on first run, so the first run needs network access
  and some disk space (see the notebook's description below for the model size).
- Notebooks pick the device automatically: Apple-silicon `mps` when available, otherwise `cpu`.
- Lint and format with `uv run ruff check .` and `uv run ruff format .`.
- To run a notebook headlessly (widget output is not saved):
  `uv run jupyter nbconvert --to notebook --execute notebooks/<name>.ipynb --output-dir <dir> --output executed.ipynb`.

## Notebooks

Each notebook covers one algorithm or paper and is self-contained. Its first cell cites the paper.

| Notebook | Topic | Description | Paper |
| --- | --- | --- | --- |
| [`typical_sampling.ipynb`](notebooks/typical_sampling.ipynb) | Decoding / sampling | Sample only tokens whose information content is close to the distribution's entropy; compared with greedy on a coin, a die and Qwen2.5-1.5B. | Meister et al., *Locally Typical Sampling* ([arXiv:2202.00666](https://arxiv.org/abs/2202.00666)) |

More notebooks for other inference methods will be added to this table.
