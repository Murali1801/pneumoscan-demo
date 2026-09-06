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
| Model | DenseNet121, 224×224 input, CLAHE preprocessing |
| Data | RSNA Pneumonia Detection Challenge (predominantly adult) |
| Test AUROC | 0.876 on 4,447 held-out images |
| Sensitivity / Specificity | 0.821 / 0.774 |
| NPV / PPV | 0.937 / 0.516 |

The decision threshold is the value tuned on validation data, not 0.5 — at this
prevalence 0.5 is arbitrary. **NPV is the number that matters**: this is a
rule-out aid. A negative is trustworthy; a positive needs a radiologist.

Grad-CAM localisation was validated against the radiologist bounding boxes that
ship with RSNA — the heatmap's hottest pixel lands inside a box 5.4× more often
than chance.

Full training pipeline: https://github.com/Murali1801/pneumoscan
