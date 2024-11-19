# Domain Matching for Reference-based Super Resolution

Official implementation of "Bridging the Domain Gap: A Simple Domain Matching Method for Reference-based Image Super-Resolution in Remote Sensing"

## Overview
We propose a simple but effective domain matching method for reference-based image super-resolution (RefSR) that works well even when there is a large domain gap between input and reference images. Our method consists of three key components:

1. Gray Matching - Reduces domain gap in correspondence matching
2. Whitening and Coloring Transform (WCT) - Aligns feature distributions 
3. Phase Replacement (PR) - Preserves structural information

![overview](Overview-1.png)

## Features
- Plug-and-play domain matching modules for existing RefSR models
- No additional training required
- Significant performance improvements on real-world remote sensing data
- Easy integration with SOTA RefSR models like C2-Matching, AMSA, and DATSR

## Installation

```bash
git clone https://github.com/username/domain-matching-refsr.git
cd domain-matching-refsr
pip install -r requirements.txt
```

## Dataset
We use the RRSSRD dataset which contains paired electro-optical satellite images:
- HR images: Gaofen-2, WorldView, Microsoft Virtual Earth 2018
- Reference images: Google Earth
- 4,047 training pairs (480×480)

## Usage

```python
# Example usage with DATSR model
from models.datsr import DATSR
from models.domain_matching import DomainMatching

# Initialize models
datsr = DATSR()
dm = DomainMatching()

# Load images
lr = load_image('lr.png')
ref = load_image('ref.png')

# Apply domain matching
lr_gray, ref_gray = dm.gray_matching(lr, ref)
matched_features = dm.wct_matching(lr_gray, ref_gray)
sr = datsr(lr, matched_features)
```

## Results

### Quantitative Results on RRSSRD Test Set
| Method | PSNR↑ | SSIM↑ |
|--------|--------|--------|
| C2-Matching | 34.05 | 0.891 |
| + Ours | 34.08 | 0.891 |
| AMSA | 34.12 | 0.891 | 
| + Ours | 34.16 | 0.892 |
| DATSR | 33.98 | 0.890 |
| + Ours | 34.10 | 0.891 |

## Citation
If you find this work useful for your research, please cite our paper:
```bibtex
@article{min2024bridging,
  title={Bridging the Domain Gap: A Simple Domain Matching Method for Reference-based Image Super-Resolution in Remote Sensing},
  author={Min, Jeongho and Lee, Yejun and Kim, Dongyoung and Yoo, Jaejun},
  journal={arXiv preprint arXiv:2401.15944},
  year={2024}
}
```

## Contact
For any questions, please contact the authors:
- Jeongho Min (jeongho.min@unist.ac.kr)
- Jaejun Yoo (jaejun.yoo@unist.ac.kr)

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements
This work was supported by KRIT, NRF Korea, and IITP grants.
