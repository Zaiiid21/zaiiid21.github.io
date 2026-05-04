---
layout: post
title: "Cloud-based AI Digital Pathology Platform: ComPRePS"
subtitle: "Technical summary of Mimar et al. (bioRxiv, 2024)"
tags: [digital pathology, cloud, ai, computational pathology, kidney, whole slide imaging]
author: "Zaid Al Hakioui (blog summary)"
comments: true
---

> **Credit to the original authors:** This post summarizes the preprint by **Sayat Mimar, Anindya S. Paul, Nicholas Lucarelli, Samuel Border, Briana A. Santo, Ahmed Naglah, Laura Barisoni, Jeffrey Hodgin, Avi Z. Rosenberg, William Clapp, and Pinaki Sarder (for the Kidney Precision Medicine Project)** <a href="#ref-1">[1]</a>.  
> I am the author of this blog summary, not the author of the original paper.

Digital pathology is one of the clearest examples of where cloud and AI have to work together. Whole-slide images (WSIs) are extremely large, pathologist time is limited, and robust model deployment is often harder than model training itself. In this post, I summarize **ComPRePS** (Computational Renal Pathology Suite), a cloud-based platform designed to make AI-powered pathology analysis more accessible to non-technical end users <a href="#ref-1">[1]</a>.

## Why this matters

The paper frames a practical bottleneck: we already have good deep learning methods for histopathology, but adoption is constrained by data scale, compute requirements, and workflow fragmentation <a href="#ref-1">[1]</a>, <a href="#ref-3">[3]</a>. ComPRePS addresses this by combining:

- Browser-based WSI visualization and annotation workflows
- Cloud-hosted AI model training and inference
- Built-in post-processing and feature extraction
- Exportable outputs for downstream analysis

The design also aligns with FAIR principles (Findable, Accessible, Interoperable, Reusable), which are explicitly highlighted as a guiding motivation <a href="#ref-1">[1]</a>, <a href="#ref-2">[2]</a>.

## Platform architecture in practice

According to the manuscript, ComPRePS uses HistomicsUI/Girder/DSA for data management and interactive WSI visualization <a href="#ref-1">[1]</a>, <a href="#ref-8">[8]</a>, <a href="#ref-9">[9]</a>. On the AI side, the segmentation stack is built around Detectron2-based panoptic segmentation pipelines <a href="#ref-1">[1]</a>, <a href="#ref-5">[5]</a>.

That gives a practical end-to-end sequence:

1. Upload/manage WSI + metadata in browser.
2. Launch training or prediction jobs with configurable hyperparameters.
3. Run patch-wise segmentation and stitch whole-slide masks.
4. Visualize color-coded overlays directly in the UI.
5. Manually edit masks when needed and persist JSON annotations.

This “single platform” experience is a key contribution, because it reduces tool-switching for pathologists and clinical researchers <a href="#ref-1">[1]</a>, <a href="#ref-4">[4]</a>.

## Data and targets used in the study

The authors report a training corpus with **190 WSIs** across multiple stains (H&E, PAS, trichrome, Jones Methenamine Silver), plus additional sub-WSIs from reference kidneys and biopsy material <a href="#ref-1">[1]</a>.

The main multi-compartment kidney targets include:

- Non-globally sclerotic glomeruli
- Globally sclerotic glomeruli
- Cortical interstitium
- Medullary interstitium
- Tubules
- Arteries/arterioles

Additional pipelines are described for peritubular capillaries (PTC) and interstitial fibrosis/tubular atrophy (IFTA) <a href="#ref-1">[1]</a>.

## Figures from the paper

![ComPRePS workflow and plugin/job UI (Figure 1 from the preprint)]({{ '/images/compreps-figure1.png' | relative_url }})

*Figure 1 (source: <a href="#ref-1">[1]</a>): HistomicsUI + ComPRePS plugin workflow, including model/job execution and annotation overlay.*

![Multi-compartment segmentation outputs (Figure 2 from the preprint)]({{ '/images/compreps-figure2.png' | relative_url }})

*Figure 2 (source: <a href="#ref-1">[1]</a>): Example outputs for cortical/medullary interstitium, glomeruli classes, tubules, arteries/arterioles, IFTA, and PTC.*

## What I find most relevant

Three aspects stand out for real-world deployment:

- **Democratization of AI use**: users can run segmentation and review outputs without coding.
- **Cloud-native scalability**: dockerized pipelines and model-zoo style reuse support multi-user scenarios.
- **Human-in-the-loop QA**: edited masks are integrated into workflow rather than treated as external artifacts.

The manuscript also notes active use across NIH-associated efforts (KPMP and HuBMAP), with a larger formal usability study planned <a href="#ref-1">[1]</a>, <a href="#ref-6">[6]</a>, <a href="#ref-7">[7]</a>.

## Caveats

This work is a **preprint** and should be interpreted accordingly. The paper demonstrates strong engineering integration and promising qualitative/operational results, but broader external validation and formal usability outcomes are still important next steps <a href="#ref-1">[1]</a>.

## References

1. <span id="ref-1"></span>Mimar S, Paul AS, Lucarelli N, et al. *ComPRePS: An Automated Cloud-based Image Analysis tool to democratize AI in Digital Pathology*. bioRxiv (2024). DOI: [10.1101/2024.03.21.586102](https://doi.org/10.1101/2024.03.21.586102)
2. <span id="ref-2"></span>Wilkinson MD, Dumontier M, Aalbersberg IJ, et al. *The FAIR Guiding Principles for scientific data management and stewardship*. Scientific Data (2016). DOI: [10.1038/sdata.2016.18](https://doi.org/10.1038/sdata.2016.18)
3. <span id="ref-3"></span>Gurcan MN, Boucheron LE, Can A, Madabhushi A, Rajpoot NM, Yener B. *Histopathological image analysis: A review*. IEEE Reviews in Biomedical Engineering (2009). DOI: [10.1109/RBME.2009.2034865](https://doi.org/10.1109/RBME.2009.2034865)
4. <span id="ref-4"></span>Lutnick B, Manthey D, Becker JU, et al. *A user-friendly tool for cloud-based whole slide image segmentation with examples from renal histopathology*. Communications Medicine (2022). DOI: [10.1038/s43856-022-00154-6](https://doi.org/10.1038/s43856-022-00154-6)
5. <span id="ref-5"></span>Detectron2 (Facebook AI Research): [https://github.com/facebookresearch/detectron2](https://github.com/facebookresearch/detectron2)
6. <span id="ref-6"></span>Kidney Precision Medicine Project (KPMP): [https://www.kpmp.org](https://www.kpmp.org)
7. <span id="ref-7"></span>HuBMAP Consortium: [https://hubmapconsortium.org](https://hubmapconsortium.org)
8. <span id="ref-8"></span>Girder: [https://github.com/girder/girder](https://github.com/girder/girder)
9. <span id="ref-9"></span>Digital Slide Archive: [https://github.com/DigitalSlideArchive/digital_slide_archive](https://github.com/DigitalSlideArchive/digital_slide_archive)

