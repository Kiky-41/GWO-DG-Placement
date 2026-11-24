# GWO-DG-Placement

**Multi-Objective in Mapping the Optimal Distributed Generation Configuration through GWOA to Enhance Grid Performance Reliability**

Wijaya, I Gede Putu Oka Indra · Ikhsan, Rifki Rahman Nur · Yustika, Lindiasari Martha · Raharjo, Jangkung  
*Jurnal Rekayasa Elektrika, 21(3), 124–132, 2025*  
[![DOI](https://img.shields.io/badge/DOI-10.17529%2Fjre.v21i3.42929-blue)](https://doi.org/10.17529/jre.v21i3.42929)

Grey Wolf Optimizer for multi-objective distributed generation placement on the IEEE 14-bus system.

## Abstract

In electric power distribution systems, the distance between the load bus and the generating unit significantly affects grid efficiency and reliability, with longer distances causing greater voltage drops. To mitigate this, Distributed Generation (DG) is increasingly being used, generating electricity closer to the point of consumption. Determining the optimal DG location requires advanced metaheuristic methods. This research proposes the Grey Wolf Optimizer Algorithm (GWOA) to determine optimal DG placement, tested on the IEEE 14-bus distribution grid. The method generated two scenarios: In the first scenario, power losses were reduced by 98.1465% for real power and 98.9538% for reactive power compared to the existing conditions, while voltage increased by an average of 0.0127 p.u. for all buses combined. The second scenario also showed a notable voltage increase of 0.0064 p.u. The GWOA method proves to be an efficient and effective solution for DG placement, enhancing system reliability and protecting household electronic devices.

## Contents

```
.gitignore
GWO_DG.ipynb
```

## Data

Input data is **not included**. Place files in `data/` (notebooks) or next to the `.m` script (MATLAB):

| File | Columns |
|---|---|
| `dg14bus.xlsx` | (format: see code) |

## Requirements

Python. Python notebooks: `numpy`, `pandas`, `scipy`, `matplotlib` (as imported). MATLAB scripts: R2021a+.

## Citation

```bibtex
@article{Wijaya_2025, title={Multi-Objective in Mapping the Optimal Distributed Generation Configuration through GWOA to Enhance Grid Performance Reliability}, volume={21}, ISSN={1412-4785}, url={http://dx.doi.org/10.17529/jre.v21i3.42929}, DOI={10.17529/jre.v21i3.42929}, number={3}, journal={Jurnal Rekayasa Elektrika}, publisher={Jurnal Rekayasa Elektrika (JRE)}, author={Wijaya, I Gede Putu Oka Indra and Ikhsan, Rifki Rahman Nur and Yustika, Lindiasari Martha and Raharjo, Jangkung}, year={2025}, month=Sept }
```
