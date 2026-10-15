
# AMCF-Net: Surgical Smoke Removal in Laparoscopic Imaging

This repository contains the implementation and experimental files for **AMCF-Net (Adaptive Multiscale Cross-Domain Feature Network)**, an unpaired deep learning framework for removing surgical smoke from laparoscopic images.

## Approach

AMCF-Net performs **unpaired image-to-image translation**, so paired smoky and smoke-free images are not required.

The proposed network combines:

- **Adaptive Smoke Prior Estimator (ASPE)** for spatial smoke estimation
- **Adaptive Multiscale Encoder (AME)** for multiscale feature extraction
- **Frequency-domain feature enhancement** for preserving fine details
- **Cross-Domain Feature Fusion (CDFF)** for combining complementary features
- **Lightweight Global Context module** for long-range feature interaction
- **Edge-guided reconstruction** for structural and boundary preservation
- Cycle-consistent adversarial learning for unpaired training

The repository also contains baseline implementations used for comparison, including **CycleGAN, FastCUT-style, and Cycle-Dehaze-style** approaches.

## Dataset

Experiments were conducted using the **DeSmoke-LAP dataset**.

The dataset was treated as two independent domains:

- **Domain A:** Smoky laparoscopic images
- **Domain B:** Clear laparoscopic images

No pixel-level correspondence between the two domains was used.

### Dataset split

| Split | Surgical Cases |
|---|---|
| Training | TLH_2, TLH_6, TLH_7, TLH_8, TLH_9, TLH_10 |
| Validation | TLH_11, TLH_12 |
| Testing | TLH_16, TLH_17 |

The training set contains **1,800 smoky and 1,800 clear images**. :chatgpt-content-reference{index="0"}

## Results

AMCF-Net was evaluated using FADE, PIQE, FID, and KID, which are suitable for the unpaired evaluation setting.

| Method | FADE ↓ | PIQE ↓ | FID ↓ | KID ↓ |
|---|---:|---:|---:|---:|
| CycleGAN | 0.292845 | 18.400478 | 166.736222 | 0.082690 |
| FastCUT-style | 0.242386 | 14.578081 | 281.420317 | 0.121304 |
| Cycle-Dehaze-style | 0.335887 | 16.570272 | 152.179890 | 0.068829 |
| **AMCF-Net** | **0.220436** | **12.558423** | **149.601400** | **0.052156** |

AMCF-Net achieved the lowest value across all four evaluated metrics in the same-dataset comparison.

## Repository Structure

```text
├── AMCF_Net.ipynb
│
├── baseline_comparision.ipynb
│
└── README.md
```

## Training

The model was trained for **50 epochs** using PyTorch with GPU acceleration and mixed precision. The average training time was approximately **353.11 seconds per epoch**.

> Note: Real-time inference performance has not yet been experimentally verified. FPS and inference latency should be measured on the target deployment hardware.