# bioml-challenge-2024
Repository for [BioML Challenge 2024](https://www.biomlsociety.org/challenge). Contact [Rohit Satija](https://www.rohitium.com/) for any questions.

# Abstract

Solved structures of CD20 in complex with antibodies are available on the PDB: [6VJA](https://www.rcsb.org/structure/6vja), [6Y92](https://www.rcsb.org/structure/6Y92), and [6Y97](https://www.rcsb.org/structure/6Y97). In all three cases, the hotspot region of CD20 present inside the binding region is the short macrocyclic polypeptide connected by a disulfide bridge `NCEPANPSEKNSPSTQYC` (166-184, chain D, 6vja). For this reason, we decided to focus on this epitope as our binder target. We chose to take a rational design approach to pick fragments of antibodies closest to the target epitope in the PDB structures using a nearest neighbor search algorithm. These sequences were ranked according to a perplexity score computed from embeddings calculated using an open source 33 layer ESM-2 model with 650M params, originally trained on UniRef50. Top 500 sequences were submitted for experimental validation. This work resulted in a number of [jupyter notebooks](https://github.com/rohitium/bioml-challenge-2024/tree/main/notebooks) and a [rational protein design package](https://github.com/rohitium/rational_protein_design) that could be useful for future protein design studies.

# Detailed Protocol

To replicate the final result, i.e. [submission.fasta](https://github.com/rohitium/bioml-challenge-2024/blob/main/results/submission.fasta), follow these steps:

1. **Binder Design:** This step is accomplished using the [rational_design.ipynb](https://github.com/rohitium/bioml-challenge-2024/blob/main/notebooks/rational_design.ipynb) notebook. Briefly, the python package [rational_protein_design](https://pypi.org/project/rational-protein-design/) contains a class called `BinderDesigner` that takes in the following attributes:
    * `pdb_file`: Path to an existing PDB structure of the bound complex (Str)
    * `chain_id`: Chain ID of the target (Str)
    * `target_residues_range`: Range of residues on Target chain to design binders for (Tuple(Int))
    * `neighbor_chain_id`: Chain ID of the candidate bound molecule (Str)
    * `N`: Length of binder (Int)
    * `num_seq`: Number of binders to design (Int)
Provided these attributes to an object of the `BinderDesigner` class, the `design_binder()` method runs all the functions necessary to design binders for the target sequence and store them in a provided fasta file path.

2. **Rank Binders:** This step is accomplished using the [compute_embeddings.ipynb](https://github.com/rohitium/bioml-challenge-2024/blob/main/notebooks/compute_embeddings.ipynb) notebook. Briefly, we create embeddings for all candidate binder sequences produced in the previous step using Facebook's `esm2_t33_650M_UR50D` model (https://github.com/facebookresearch/esm?tab=readme-ov-file#main-models-you-should-use-). Next, we compute perplexity for each individual sequence (https://en.wikipedia.org/wiki/Perplexity) that is a metric describing how well the model predicts the existence of the sequence. We rank order the binder sequences using this score and save the top 500 sequences to file.