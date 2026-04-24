# From Canopy to Crown: High-Fidelity Tree Façade Synthesis from Nadir LiDAR Data



**Authors:** Raghav Sharma¹, Frank Zhang², Jane Liu³, Baoxin Hu⁴

¹² Department of Computer Science, University of Fraser Valley, Abbotsford, BC, Canada  
³ Department of Geography and Planning, University of Toronto, Toronto, ON, Canada  
⁴ Department of Earth and Space Science and Engineering, York University, Toronto, ON, Canada

---

## Overview

This repository contains the implementation of the first conditional diffusion model to generate structurally plausible façade views of individual tree crowns from single nadir-view LiDAR rasters. Our approach addresses a fundamental challenge in remote sensing: transforming readily available top-down tree imagery into logistically expensive side-view representations.

![Nadir to Façade Synthesis](https://github.com/raghav-sharma272381/Canopytocrown/blob/main/sample.png?raw=true)
*Illustration of the nadir-to-façade synthesis challenge. Left: Widely available nadir (top-down) view. Right: Logistically expensive façade (side) view. Center: Our conditional diffusion approach.*

## Key Contributions

- **Novel Task**: First work to apply diffusion models for cross-dimensional tree view synthesis
- **Systematic Conditioning**: Demonstrates that nadir imagery alone is insufficient, but conditioning on species and height enables realistic façade generation
- **Strong Performance**: Fully conditioned model achieves LPIPS of 0.184 and SSIM of 0.576, outperforming nadir-only baselines by more than twofold
- **Scalable Solution**: Reduces need for resource-intensive ground surveys in large-scale forest inventories

## Dataset

We leverage the **FOR-species20K** benchmark dataset (Puliti et al., 2025), featuring:
- 20,158 individual tree point clouds
- 33 species across 19 genera
- Multi-platform acquisition (TLS, ULS, MLS)
- Global coverage: Europe, Canada, Australia, New Zealand
- Tree heights ranging from 0.3m to 56m
- Final processed dataset: 11,440 paired nadir-façade images

## Method

### Architecture
- **Framework**: Denoising Diffusion Probabilistic Model (DDPM)
- **Backbone**: Conditional U-Net with skip connections
- **Input**: 128×128 three-channel nadir view (RGB encoding point density, normalized height, and height variation)
- **Output**: 128×128 single-channel façade view (grayscale point density)

### Conditioning Mechanisms
1. **Image-based**: Nadir view concatenated with noisy façade
2. **Attribute-based**: Tree height (MLP) + species label (embedding layer)
3. **Timestep-based**: Sinusoidal positional encoding

### Experimental Models
- **Model 1 (Fully-Conditioned)**: Nadir + Species + Height
- **Model 2 (Height-Conditioned)**: Nadir + Height
- **Model 3 (Nadir-Only)**: Nadir view only

## Results

| Model | MAE ↓ | PSNR ↑ | SSIM ↑ | LPIPS ↓ |
|-------|-------|--------|---------|----------|
| Nadir + Species + Height | **0.077** | **15.48** | **0.576** | **0.184** |
| Nadir + Height | 0.087 | 14.57 | 0.538 | 0.259 |
| Nadir Only | 0.123 | 12.95 | 0.269 | 0.424 |

The fully-conditioned model demonstrates substantial improvements across all metrics, with particularly strong perceptual quality (LPIPS) indicating successful learning of species-specific structural priors.

## Applications

- **Forest Inventory**: Enhanced biomass, timber volume, and carbon stock estimates
- **Urban Forestry**: Scalable assessment of structural health and hazard detection
- **Ecological Modeling**: Detailed habitat modeling for species dependent on specific tree architectures
- **3D Reconstruction**: Pathway toward full 3D point cloud generation from nadir views

## Limitations

- Closed-set species recognition (30 species)
- Trained on isolated, well-segmented trees
- Single fixed façade view (not full 360° structure)

## Future Work

- Photorealistic RGB façade synthesis
- Full 3D point cloud generation
- Multi-view synthesis with 360° coverage
- Open-set species recognition
- Complex scene handling with overlapping canopies


## Acknowledgments

We acknowledge the FOR-species20K dataset contributors (Puliti et al., 2025) for making this research possible. Training was conducted on NVIDIA A100 GPUs.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For questions or collaborations, please open an issue or contact:
- Raghav Sharma: [raghav.sharma2@student.ufv.ca]
- Frank Zhang: [frank.zhang@ufv.ca]

---

**Status**: 📝 [Accepted at ISPRS Journal of Photogrammetry and Remote Sensing](https://www.researchgate.net/publication/400780858_From_Canopy_to_Crown_High-Fidelity_Tree_Facade_Synthesis_from_Nadir_LiDAR_data)  
               [Under Review at Remote Sensing Applications Society and Environment](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6412841)

**Last Updated**: April 2026
