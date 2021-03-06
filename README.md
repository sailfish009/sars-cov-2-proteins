# SARS-Cov-2 protein structure models
We have predicted and/or refined SARS-Cov-2 protein structure models. We initially focused on proteins which were hard to predict by using homology modeling (template-based modeling) because of the lack of experimentally determined homolog protein structures. We are publishing three sets of structure models: models based on our structure prediction pipeline, refined AlphaFold models, and refined RaptorX models. We made additional predictions based on our pipeline and by refining other models on proteins which have experimental homolog protein structures, but not too close (sequence identity < 90%). Finally, for 4 membrane proteins, we revised our predictions or selected some models among available models that are more likely, and we refined those selected models as their physiological oligomeric forms in the ER membrane bilayer.

**For detailed modeling procedures and analyses, see [our bioRxiv paper](https://www.biorxiv.org/content/10.1101/2020.03.25.008904v1).**

### Our structure prediction pipeline-based models (FeigLab)
We predicted 10 models for SARS-Cov-2 proteins based on our latest structure prediction pipeline. Our structure prediction pipeline consists of two major features: initial contact-based structure prediction followed by molecular dynamics (MD) simulation-based refinement. We use trRosetta [1] for the initial contact-based structure prediction. We generated 10 models for each target protein, and the best scored model was subjected to the further refinement. Our refinement protocol is based on molecular dynamics (MD) simulations [2]. Various structures are sampled in the vicinity of the initial model structure via MD simulations during the refinement, and a set of low energy conformations is selected and averaged to get an ensemble averaged structure. Our refinement protocol demonstrated success during the last several CASPs with consistent improvements in model qualities. [3] The refinement protocol used here is improved from the method used during the last CASP.

### Refinement of AlphaFold models (AlphaFold)
Early in March 2020, Google DeepMind published their predicted models on [their web page](https://deepmind.com/research/open-source/computational-predictions-of-protein-structures-associated-with-COVID-19) by using their latest AlphaFold method [4]. The models cover 6 SARS-Cov-2 proteins. We refined those AlphaFold models by using our latest refinement protocol. We found earlier that AlphaFold models which are machine learning-based can be improved further with physics-based refinement method. [5] Physics-based refinement can complement machine learning-based models by providing more atomistic details such as better structure packing and loop structures. We therefore expect that these refined models have increased accuracy over the initial AlphaFold predictions and may be more suitable for further applications such as molecular docking and virtual screening.

### Refinement of RaptorX models
As a collaboration with Jinbo Xu, we refined his models, which are based on [RaptorX-Contact](http://raptorx.uchicago.edu/), one of the best protein inter-residue contact prediction methods. The models covers the exactly same SARS-CoV-2 proteins that of ours. We applied the same refinement method used for refining AlphaFold models or our in-house structure prediction pipeline.

### Refinement of a Baker lab's model
For nsp2, as it was one of the proteins that have most diverse topologies among [CASP-Commons predictions](http://predictioncenter.org/caspcommons/), we refined the Baker lab's model by using the same refinement protocol.

### Refinement of SWISS-MODEL models
We refined some of the [SWISS-MODEL](http://swissmodel.expasy.org/repository/species/2697049) models. We selected models
to be refined, which were able to predict by using homology modeling, but those homolog structures were not too close
(sequence identity > 90%). Since SWISS-MODEL predictions were domain-basis, we named PDB file names as
${proteinName}\_${domainNumber}\_swiss.pdb for refined ${proteinName}'s ${domainNumber}.pdb

### Refinement of Membrane proteins
We revisited 4 membrane proteins, M, E, nsp4, and nsp6, to refine with consideration of membrane environment. We did our
best to predict or select among available models for the initial models by doing literature searches carefully. For the
detailed explanation on the initial models are described below. We refined the proteins in the ER membrane (55% POPC, 25% POPE, 10% POPI, 2% POPS, 6% Cholestreol, 2% cardiolipin), which
is set up via [CHARMM-GUI](http://www.charmm-gui.org/?doc=input/membrane.bilayer). Refinement simulations were performed
on GPU clusters provided by [COVID-19 HPC Consortium](https://covid19-hpc-consortium.org/) and
the [MSU-HPCC](https://icer.msu.edu/about/announcements/covid-19-research-icer-queue-times).

For M protein, we first revised its monomer structure by combining information from the AlphaFold model and ours. As it
forms dimer in physiological condition, we built dimer models by facing two out of three transmembrane helices; it
resulted in three candidates. These dimer models were subjected to coarse-grained MD simulations to adjust relative
orientations by Prof. Khalid in Univ. of Southampton, UK. The resulting coarse-grained models were converted into
all-atom models. One of the all-atom model was selected for the further refinement by using membrane insertion energy
and visual inspection.

For E protein, we predicted its monomer structure by using our structure prediction pipeline. Then, the model was used
to built a homo-pentameric structure by using pentameric assembly of E protein of SARS-CoV (PDB ID: 5x29). Because
C-terminal residues should not be in the membrane, so we manually adjusted their relative positions.

For nsp4, we re-built our model with additional information from literature search.

For nsp6, we took AlphaFold model for the refinement in the menbrane environment.

### Spike/M protein complex model
We modeled Spike (trimer) and M protein (dimer) complexes with a stoichometry of 1:4 in the ER membrane environment.
Coarse-grained MD simulations were performed from random orientations of those proteins by using MARTINI force field by
Prof. Khalid. We clustered sampled conformations via DBSCAN algorithm with a 5 Angstrom of CA-RMSD cutoff. We got 5
clusters, and the most of the conformations were in the biggest cluster (>99%). We took the cluster center from the
biggest cluster and converted into all-atom representation by superposing all-atom models. As there were a few
side-chain overlaps between proteins, we slightly adjusted orientation manually. Finally, we set up all-atom MD simulation 
with the ER membrane by using [CHARMM-GUI](http://www.charmm-gui.org/?doc=input/membrane.bilayer) and conducted
refinement simulations.

### M protein (revisited)
We revisited the M protein modeling as ORF3a structure has been resolved ([6XDC](https://www.rcsb.org/structure/6XDC)),
which seems in structural homolog relationship to the M protein. The ORF3a structure has a tighter dimerization
interface than we thought earlier. Thus, we decided to re-model the M protein with the dimerization information. We
found that we could build a dimer model while it still satisfied the predicted contacts, but some of the contacts were
inter-chain contacts rather than intra-chain contacts. We applied our membrane protein refinement method to the new M
protein model. Here is the [link](https://github.com/feiglab/sars-cov-2-proteins/tree/master/Membrane/M_dimer_new.pdb)
to the new model.

![M protein contacts](https://github.com/feiglab/sars-cov-2-proteins/blob/master/images/M_contact.png)

### Model summary and comparisons
|  Protein  | RefSeq | [FeigLab](https://github.com/feiglab/sars-cov-2-proteins/tree/master/FeigLab) | [RaptorX](https://github.com/feiglab/sars-cov-2-proteins/tree/master/RaptorX) | [AlphaFold](https://github.com/feiglab/sars-cov-2-proteins/tree/master/AlphaFold) | [BakerLab](https://github.com/feiglab/sars-cov-2-proteins/tree/master/Soluble) | [SWISS-MODEL](https://github.com/feiglab/sars-cov-2-proteins/tree/master/Soluble) | [Membrane](https://github.com/feiglab/sars-cov-2-proteins/tree/master/Membrane) | [CASP-Commons](http://predictioncenter.org/caspcommons/models_consensus2.cgi) |
|:---------:|:--------:|:-------:|:-------:|:---------:|:--------:|:-----------:|:--------:|:--:|
|nsp1       | [YP_009725297.1](https://www.ncbi.nlm.nih.gov/protein/YP_009725297.1) | O | X | X | X | O | X | X |
|nsp2       | [YP_009725298.1](https://www.ncbi.nlm.nih.gov/protein/YP_009725298.1) | O | O | O | O | X | X | O |
|PL-PRO     | [YP_009725299.1](https://www.ncbi.nlm.nih.gov/protein/YP_009725299.1) | O | O | O | X | O | X | O |
|nsp4       | [YP_009725300.1](https://www.ncbi.nlm.nih.gov/protein/YP_009725300.1) | O | O | O | X | (partial) | O | O |
|nsp6       | [YP_009725302.1](https://www.ncbi.nlm.nih.gov/protein/YP_009725302.1) | O | O | O | X | X | O | O |
|ORF3a      | [YP_009724391.1](https://www.ncbi.nlm.nih.gov/protein/YP_009724391.1) | O | O | O | X | X | X | O |
|E\_protein | [YP_009724392.1](https://www.ncbi.nlm.nih.gov/protein/YP_009724392.1) | X | X | X | X | X | O | X |
|M\_protein | [YP_009724393.1](https://www.ncbi.nlm.nih.gov/protein/YP_009724393.1) | O | O | O | X | X | O | O |
|ORF6       | [YP_009724394.1](https://www.ncbi.nlm.nih.gov/protein/YP_009724394.1) | O | O | X | X | X | X | O |
|ORF7a      | [YP_009724395.1](https://www.ncbi.nlm.nih.gov/protein/YP_009724395.1) | O | X | X | O | O | X | X |
|ORF7b      | [YP_009725296.1](https://www.ncbi.nlm.nih.gov/protein/YP_009725296.1) | O | O | X | X | X | X | O |
|ORF8       | [YP_009724396.1](https://www.ncbi.nlm.nih.gov/protein/YP_009724396.1) | O | O | X | X | O | X | O |
|ORF10      | [YP_009725255.1](https://www.ncbi.nlm.nih.gov/protein/YP_009725255.1) | O | O | X | X | X | X | O |
|S/M complex| - | X | X | X | X | X | O | X |


### Acknowledgements


### References
1. Yang, J. *et al.*, Improved protein structure prediction using predicted interresidue orientations, *Proc. Natl. Acad. Sci. USA*, (**2020**). [[LINK]](https://www.pnas.org/content/117/3/1496.short)
2. Heo, L. and Feig, M., PREFMD: a web server for protein structure refinement via molecular dynamics simulations, *Bioinformatics*, (**2017**). [[LINK]](https://academic.oup.com/bioinformatics/article/34/6/1063/4604595)
3. Heo, L, Arbour, C.F., and Feig, M., Driven to near-experimental accuracy by refinement via molecular dynamics simulations, *Proteins* (**2019**). [[LINK]](https://onlinelibrary.wiley.com/doi/full/10.1002/prot.25759)
4. Jumper, J. *et al.*, Computational predictions of protein structures associated with COVID-19, [DeepMind website](https://deepmind.com/research/open-source/computational-predictions-of-protein-structures-associated-with-COVID-19), (March 5, 2020).
5. Heo, L. and Feig, M., High-accuracy protein structures by combining machine-learning with physics-based refinement, *Proteins* (**2019**). [[LINK]](https://onlinelibrary.wiley.com/doi/abs/10.1002/prot.25847)
