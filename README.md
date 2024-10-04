# bioml-challenge-2024
Repository for BioML Challenge 2024 [Link](https://www.biomlsociety.org/challenge)

# Abstract

Solved structures of CD20 in complex with antibodies are available on the PDB: [6VJA](https://www.rcsb.org/structure/6vja), [6Y92](https://www.rcsb.org/structure/6Y92), and [6Y97](https://www.rcsb.org/structure/6Y97). In all three cases, the hotspot region of CD20 present inside the binding region is the short macrocyclic polypeptide connected by a disulfide bridge `NCEPANPSEKNSPSTQYC` (166-184, chain D, 6vja). For this reason, we decided to focus on this epitope as our binder target. We chose to take a rational design approach to pick fragments of antibodies closest to the target epitope in the PDB structures using a nearest neighbor search algorithm. These sequences were ranked according to a perplexity score computed from embeddings calculated using an open source 33 layer ESM-2 model with 650M params, originally trained on UniRef50. Top 500 sequences were submitted for experimental validation. This work resulted in a number of [jupyter notebooks](https://github.com/rohitium/bioml-challenge-2024/tree/main/notebooks) and a [rational protein design package](https://github.com/rohitium/rational_protein_design) that could be useful for future protein design studies.

# Detailed Protocol

To replicate the final result, i.e. [submission.fasta](), use the below steps:
