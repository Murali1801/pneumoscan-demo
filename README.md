---
title: PneumoScan
emoji: 🫁
colorFrom: gray
colorTo: green
sdk: docker
app_port: 7860
pinned: false
license: mit
---

# PneumoScan — Explainable Pneumonia Screening

Upload a chest X-ray (DICOM, PNG or JPEG) and get a prediction with a Grad-CAM
heatmap showing what drove it.

**Research demonstration only — not a medical device.**

| | |
|---|---|
| Model | DenseNet121, 320×320 input, CLAHE preprocessing |
| Data | RSNA Pneumonia Detection Challenge (predominantly adult) |
| Test AUROC | 0.879 on 4,447 held-out images |
| Sensitivity / Specificity | 0.826 / 0.767 |
| NPV / PPV | 0.938 / 0.510 |

The decision threshold is the value tuned on validation data, not 0.5 — at this
prevalence 0.5 is arbitrary. **NPV is the number that matters**: this is a
rule-out aid. A negative is trustworthy; a positive needs a radiologist.

Grad-CAM localisation was validated against the radiologist bounding boxes that
ship with RSNA — the heatmap's hottest pixel lands inside a box 5.4× more often
than chance.

## Deploying this

Needs **Python 3.10-3.12**. TensorFlow publishes no wheels for 3.13 or 3.14, and
hosts default to the newest interpreter, so set the version *before* the first
deploy or the build fails with `No matching distribution found for
tensorflow-cpu`.

* **Streamlit Community Cloud** — *Advanced settings -> Python version -> 3.12*
  at deploy time. Note it does not fetch Git LFS objects, which is why the
  checkpoint here is a plain 12.8 MB file.
* **Docker** — the included `Dockerfile` pins `python:3.11-slim`, so this is
  already handled.

Full training pipeline: https://github.com/Murali1801/pneumoscan
