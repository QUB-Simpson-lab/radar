# radar
![logo](./logo.png)

Rapid Agnostic Detection of All Recombinants - Funded by COG UK (https://www.cogconsortium.uk/) Early Career Funding Scheme

## Installation
radar is written in python3 and requires numpy, pandas, and [nextclade](https://github.com/nextstrain/nextclade/blob/master/docs/user/nextclade-cli.md), so it is likely for genomic surveillance researchers that an existing python environment will suffice to run radar. However, should you require or desire a dedicated environment to run radar, an environment can be installed using the following commands using anaconda.

```
conda create -n radar
conda activate radar
conda install numpy pandas nextclade -c bioconda -c conda-forge
```

## Running radar
### Foreword
The alpha release of radar is (to be - expected by 31 Mar 2023) contained in radar.py, and will be updated periodically. As this project still under development, the software will not be as flexible or robust as its eventual final release. Further, it is envisioned that the running and installation process of radar will change.. We are actively working on improving and refining the code to ensure its quality and stability.

### Required Inputs
1. A reference sequence ```--ref```
2. A multiple sequence fasta of consensus sequences with which to detect recombinants from ```--in```
3. The nextclade dataset of the virus in question. ```--dataset```

```./radar.py --ref MN908947.3.fa --in sequences.fa --dataset ./nextclade/sars-cov-2```

### What radar is doing
radar works by systematically dividing each consensus FASTA sequence into windows and uses nextclade/nextstrain to assign a clade to each. The tool applies unbiased window-based lineage determinations to rapidly identify putative recombinant sequences, and subsequently applies higher resolution SNV-based analysis to determine breakpoints while assessing confidence in the lineage determinations. Futher details will be elucidated in a future scientific pre-print or peer-reviewed publication. In order to avoid confusion, the source of radar will be limited

### radar outputs
radar_results.tsv will provide the user with the following:
   the list of sample_ids (obtained from the fasta headers) as to which are samples are deemed to be recombinant.
   and for each sample: the list of recombinant 'breakpoints' (i.e., where the sequence changes from one clade to another) and the constitutent clades for each window.
