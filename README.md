# SurgFusion: Multimodal Surgical Video Understanding

A multimodal deep learning pipeline for surgical video analysis, combining **object/tool detection**, **surgical phase recognition**, and **fine-grained gesture recognition**, with a **weighted ensemble fusion** layer combining phase and gesture predictions.
---

## Overview

Surgical video understanding is typically split into three sub-tasks. This project implements all three as independent modules, and additionally explores whether phase-recognition features transfer to improve gesture recognition via a learnable weighted fusion head — even though the two source datasets share no video content (a cross-domain transfer setting).

| Module | Task | Model | Dataset |
|---|---|---|---|
| Object Detection | Tool/instrument localization | YOLO11m | m2cai16-tool-locations |
| Phase Recognition | Surgical phase classification (19 classes) | r3d_18 | SurgBench-E (AutoLaparo, CholecT50, EndoVis2019) |
| Gesture Recognition | Fine-grained gesture classification (13 classes) | C(2+1)D (`r2plus1d_18`) | JIGSAWS (Suturing, Knot-Tying, Needle-Passing) |
| **Fusion** | Weighted gesture+phase ensemble | Learnable weighted head on frozen embeddings | JIGSAWS (LOUO split) |

---

## Datasets

| Dataset | Access | Used for |
|---|---|---|
| [JIGSAWS](https://cs.jhu.edu/~los/jigsaws/info.php) | Request access via official form | Gesture recognition |
| [m2cai16-tool-locations](http://camma.u-strasbg.fr/m2cai2016/) | Request access via CAMMA | Object detection |
| AutoLaparo, CholecT50, EndoVis2019 (via SurgBench-E) | Request access — see [SurgBench paper](https://arxiv.org/abs/2506.07603) | Phase recognition |

---

## Citation

```bibtex
@article{wei2025surgbench,
  title={SurgBench: A Unified Large-Scale Benchmark for Surgical Video Analysis},
  author={Wei, Jianhui and Xiao, Zikai and Sun, Danyu and Gong, Luqi and Yang, Zongxin and Liu, Zuozhu and Wu, Jian},
  journal={arXiv preprint arXiv:2506.07603},
  year={2025}
}

@article{ahmidi2017jigsaws,
  title={A Dataset and Benchmarks for Segmentation and Recognition of Gestures in Robotic Surgery},
  author={Ahmidi, Narges and Tao, Lingling and Sefati, Shahin and Gao, Yixin and Lea, Colin and Haro, Benjam{\'\i}n B{\'e}jar and Zappella, Luca and Khudanpur, Sanjeev and Vidal, Ren{\'e} and Hager, Gregory D},
  journal={IEEE Transactions on Biomedical Engineering},
  volume={64}, number={9}, pages={2025--2041}, year={2017}
}

@inproceedings{tran2018closer,
  title={A Closer Look at Spatiotemporal Convolutions for Action Recognition},
  author={Tran, Du and Wang, Heng and Torresani, Lorenzo and Ray, Jamie and LeCun, Yann and Paluri, Manohar},
  booktitle={CVPR}, pages={6450--6459}, year={2018}
}
