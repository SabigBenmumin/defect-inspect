# defect-inspect

> Work in progress — Sabig will finalize this README on Day 19.

Surface-defect inspection on KolektorSDD2: image-level accept/reject decisions,
False Reject / False Accept operating-point selection, error analysis,
a simulated production → retraining feedback loop, and ONNX deployment.

## Setup

```bash
python -m venv .venv
.venv\Scripts\activate          # Windows
# Install PyTorch for your CUDA version first: https://pytorch.org/get-started/locally/
pip install -r requirements.txt
```

Download KolektorSDD2 from https://www.vicos.si/resources/kolektorsdd2/
and extract it into `data/raw/`.

## Dataset & license

KolektorSDD2 by Kolektor Group d.o.o. and ViCoS, University of Ljubljana,
licensed CC BY-NC-SA 4.0. This repository is a non-commercial learning project.
