# GWO-DG-Placement

**Multi-Objective in Mapping the Optimal Distributed Generation Configuration through GWOA to Enhance Grid Performance Reliability**

Wijaya, I Gede Putu Oka Indra · Ikhsan, Rifki Rahman Nur · Yustika, Lindiasari Martha · Raharjo, Jangkung  
*Jurnal Rekayasa Elektrika, 21(3), 124–132, 2025*  
[![DOI](https://img.shields.io/badge/DOI-10.17529%2Fjre.v21i3.42929-blue)](https://doi.org/10.17529/jre.v21i3.42929)

Grey Wolf Optimizer for multi-objective distributed generation placement on the IEEE 14-bus system.

## Abstract

In electric power distribution systems, the distance between the load bus and the generating unit significantly affects grid efficiency and reliability, with longer distances causing greater voltage drops. To mitigate this, Distributed Generation (DG) is increasingly being used, generating electricity closer to the point of consumption. Determining the optimal DG location requires advanced metaheuristic methods. This research proposes the Grey Wolf Optimizer Algorithm (GWOA) to determine optimal DG placement, tested on the IEEE 14-bus distribution grid. The method generated two scenarios: In the first scenario, power losses were reduced by 98.1465% for real power and 98.9538% for reactive power compared to the existing conditions, while voltage increased by an average of 0.0127 p.u. for all buses combined. The second scenario also showed a notable voltage increase of 0.0064 p.u. The GWOA method proves to be an efficient and effective solution for DG placement, enhancing system reliability and protecting household electronic devices.



## Proposed method

Grey Wolf Optimizer (GWO) searches for the bus and capacity of one distributed generator on the IEEE 14-bus network. Each wolf encodes a candidate placement; the pack is led by the three best placements ($\alpha$, $\beta$, $\delta$), and the objective is network loss subject to the grid-code voltage band. The paper reports two scenarios, with loss reductions of 98.15% (real) and 98.95% (reactive) in the first.

### Problem formulation

The network loss is the sum of $I^2R$ over all branches, equivalently the double-sum expression in bus voltages and admittances:

$$\min_{\text{bus},~P_{DG}}~P_{\text{loss}}=\sum_{k=1}^{N_l}I_k^2R_k=\sum_{i=1}^{N}\sum_{j=1}^{N}G_{ij}\left(V_i^2+V_j^2-2V_iV_j\cos(\theta_i-\theta_j)\right).$$

The constraints are the grid-code voltage band, the DG penetration cap and the DG size bounds:

$$0.90\le V_i\le1.05~\text{p.u.},\qquad P_{DG}\le0.20~P_{\text{peak}},\qquad P_{DG}^{\min}\le P_{DG}\le P_{DG}^{\max}.$$

### Notation

| Symbol | Meaning | Unit |
|---|---|---|
| $N$ | number of buses | – |
| $N_l$ | number of branches | – |
| $V_i,\theta_i$ | voltage magnitude and angle at bus $i$ | p.u., rad |
| $G_{ij}$ | real part of the bus admittance matrix | p.u. |
| $I_k,R_k$ | current and resistance of branch $k$ | p.u., p.u. |
| $P_{\text{loss}}$ | total active-power loss | MW |
| $P_{DG}$ | DG capacity | MW |
| $P_{\text{peak}}$ | peak system demand | MW |
| $\mathbf{X}$ | wolf position (bus and capacity) | – |
| $\mathbf{X}_\alpha,\mathbf{X}_\beta,\mathbf{X}_\delta$ | three best positions | – |
| $\mathbf{A},\mathbf{C}$ | GWO coefficient vectors | – |
| $a$ | encircling parameter, decreases from 2 to 0 | – |
| $t,T$ | iteration and iteration cap | – |

### GWO equations

Encircling the prey:

$$\mathbf{D}=\left|\mathbf{C}\odot\mathbf{X}_p(t)-\mathbf{X}(t)\right|,\qquad \mathbf{X}(t+1)=\mathbf{X}_p(t)-\mathbf{A}\odot\mathbf{D},$$

$$\mathbf{A}=2a\mathbf{r}_1-a,\qquad \mathbf{C}=2\mathbf{r}_2,\qquad a=2-\frac{2t}{T}.$$

The vector $\mathbf{A}$ controls whether the wolf approaches or moves away from the prey, and $\mathbf{C}$ adds random weighting. As $a$ falls, the pack shifts from exploration to encirclement.

Hunting uses the three leaders:

$$\mathbf{D}_\alpha=\left|\mathbf{C}_1\mathbf{X}_\alpha-\mathbf{X}\right|,\quad \mathbf{D}_\beta=\left|\mathbf{C}_2\mathbf{X}_\beta-\mathbf{X}\right|,\quad \mathbf{D}_\delta=\left|\mathbf{C}_3\mathbf{X}_\delta-\mathbf{X}\right|,$$

$$\mathbf{X}_1=\mathbf{X}_\alpha-\mathbf{A}_1\mathbf{D}_\alpha,\qquad \mathbf{X}_2=\mathbf{X}_\beta-\mathbf{A}_2\mathbf{D}_\beta,\qquad \mathbf{X}_3=\mathbf{X}_\delta-\mathbf{A}_3\mathbf{D}_\delta,$$

$$\mathbf{X}(t+1)=\frac{\mathbf{X}_1+\mathbf{X}_2+\mathbf{X}_3}{3}.$$

Averaging the three candidate moves keeps the pack near the best-known region while still allowing the $\beta$ and $\delta$ wolves to influence the direction.

### Algorithm

1. Initialise 100 wolves over bus index and DG capacity; evaluate each with the Fast-Decoupled load flow.
2. Rank the pack and set $\alpha$, $\beta$, $\delta$.
3. Update $a$ from 2 to 0 and move every wolf with the equations above.
4. Re-evaluate losses and voltage; repeat until the iteration cap.
5. Report the $\alpha$ wolf as the optimal bus/capacity pair.

### Implementation note

The notebook evaluates a simplified loss proxy: line impedance is formed from resistance, reactance and susceptance, current is estimated with a flat $V=1.0$ p.u. assumption, and only the top three DG buses are kept. Voltage is not part of the notebook fitness, although the paper enforces the 0.90–1.05 p.u. band and reports voltage improvements. The load-flow results in the paper therefore come from the paper workflow, not from this notebook.
### Reported result
Scenario 1 places one DG and cuts active-power losses by 98.15% and reactive-power losses by 98.95%, with an average voltage rise of 0.0127 p.u.; scenario 2 raises the average voltage by 0.0064 p.u. Both scenarios stay inside the 0.90-1.05 p.u. band.

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


## Results

### Existing IEEE 14-bus condition, base case

| Quantity | Active power | Reactive power |
|---|---|---|
| Losses before DG | 25.3580 MW | 84.5010 MVAR |

### Scenario 1, maxiter 100, DG at buses 7, 8, 11, 14

| Measure | Value |
|---|---|
| DG size at bus 7 | 224.13 kW |
| DG size at bus 8 | 468.61 kW |
| DG size at bus 11 | 360.23 kW |
| DG size at bus 14 | 205.39 kW |
| Losses after DG | 0.4700 MW / 0.8840 MVAR |
| Active loss reduction | 98.1465% |
| Reactive loss reduction | 98.9538% |
| Average voltage change | +0.0127 p.u. |
| Lowest bus voltage | 0.9693 p.u. at bus 12 |

### Scenario 2, maxiter 50, DG at buses 1, 2, 8, 14

| Measure | Value |
|---|---|
| DG size at bus 1 | 152.23 kW |
| DG size at bus 2 | 293.88 kW |
| DG size at bus 8 | 648.63 kW |
| DG size at bus 14 | 174.18 kW |
| Losses after DG | 1.3250 MW / 2.6520 MVAR |
| Active loss reduction | 94.7748% |
| Reactive loss reduction | 96.8616% |
| Average voltage change | +0.0064 p.u. |
| Lowest bus voltage | 0.9242 p.u. at bus 14 |


## Requirements

Python. Python notebooks: `numpy`, `pandas`, `scipy`, `matplotlib` (as imported). MATLAB scripts: R2021a+.

## Citation

```bibtex
@article{Wijaya_2025, title={Multi-Objective in Mapping the Optimal Distributed Generation Configuration through GWOA to Enhance Grid Performance Reliability}, volume={21}, ISSN={1412-4785}, url={http://dx.doi.org/10.17529/jre.v21i3.42929}, DOI={10.17529/jre.v21i3.42929}, number={3}, journal={Jurnal Rekayasa Elektrika}, publisher={Jurnal Rekayasa Elektrika (JRE)}, author={Wijaya, I Gede Putu Oka Indra and Ikhsan, Rifki Rahman Nur and Yustika, Lindiasari Martha and Raharjo, Jangkung}, year={2025}, month=Sept }
```

## License

[![CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](LICENSE)

Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). **Attribution is required**: any use of this code, results, or figures, including in publications, must cite:

> I Gede Putu Oka Indra Wijaya; Rifki Rahman Nur Ikhsan; Lindiasari Martha Yustika; Jangkung Raharjo (2025). Multi-Objective in Mapping the Optimal Distributed Generation Configuration through GWOA to Enhance Grid Performance Reliability. *Jurnal Rekayasa Elektrika*. https://doi.org/10.17529/jre.v21i3.42929
