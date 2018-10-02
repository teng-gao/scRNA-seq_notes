# A continually expanding collection of scRNA-seq tools

Issues with suggestions and pull requests are welcome!

# Table of content

* [Preprocessing pipelines](#preprocessing-pipelines)
* [Quality control](#quality-control)
* [Normalization](#normalization)
* [Batch effect](#batch-effect)
* [Dimensionality reduction](#dimensionality-reduction)
* [Clustering and visualization](#clustering-and-visualization)
  * [Time inference](#time-inference)
  * [Networks](#networks)
* [Differential expression](#differential-expression)
* [10X Genomics](#10x-genomics)
  * [QC](#10x-qc)
* [Data](#data)
  * [Brain single-cell data](#Brain-single-cell-data)
    * [Human](#human)
    * [Mouse](#mouse)
* [Links and other resources](#links)

## Preprocessing pipelines

- `Granatum` - web-based scRNA-seq analysis. list of modules, including plate merging and batch-effect removal, outlier-sample removal, gene-expression normalization, imputation, gene filtering, cell clustering, differential gene expression analysis, pathway/ontology enrichment analysis, protein network interaction visualization, and pseudo-time cell series reconstruction. http://garmiregroup.org/granatum/app, http://ilab.hawaii.edu:8111/
    - Zhu, Xun, Thomas K. Wolfgruber, Austin Tasato, Cédric Arisdakessian, David G. Garmire, and Lana X. Garmire. “Granatum: A Graphical Single-Cell RNA-Seq Analysis Pipeline for Genomics Scientists.” Genome Medicine 9, no. 1 (December 2017). https://doi.org/10.1186/s13073-017-0492-3.

- `SEQC` - Single-Cell Sequencing Quality Control and Processing Software, a general purpose method to build a count matrix from single cell sequencing reads, able to process data from inDrop, drop-seq, 10X, and Mars-Seq2 technologies. https://github.com/ambrosejcarr/seqc
    - Azizi, Elham, Ambrose J. Carr, George Plitas, Andrew E. Cornish, Catherine Konopacki, Sandhya Prabhakaran, Juozas Nainys, et al. “Single-Cell Map of Diverse Immune Phenotypes in the Breast Tumor Microenvironment.” Cell, June 2018. https://doi.org/10.1016/j.cell.2018.05.060.

- `Seurat` - an R package designed for QC, analysis, and exploration of single cell RNA-seq data. Single-cell RNA-seq for spatial cellular localization, using in situ RNA patterns as a reference. Impute landmark genes, relate them to the reference map. http://satijalab.org/seurat/, https://davetang.org/muse/2017/08/01/getting-started-seurat/
    - Satija, Rahul, Jeffrey A. Farrell, David Gennert, Alexander F. Schier, and Aviv Regev. “Spatial Reconstruction of Single-Cell Gene Expression Data.” Nature Biotechnology 33, no. 5 (May 2015): 495–502. https://doi.org/10.1038/nbt.3192.

- `scPipe` - A preprocessing pipeline for single cell RNA-seq data that starts from the fastq files and produces a gene count matrix with associated quality control information. It can process fastq data generated by CEL-seq, MARS-seq, Drop-seq, Chromium 10x and SMART-seq protocols. https://bioconductor.org/packages/release/bioc/html/scPipe.html
    - Tian et al. "scPipe: A flexible R/Bioconductor preprocessing pipeline for single-cell RNA-sequencing data" https://doi.org/10.1371/journal.pcbi.1006361 PLOS Computational Biology, 2018. https://doi.org/10.1371/journal.pcbi.1006361

## Quality control

- `scater` - A collection of tools for doing various analyses of single-cell RNA-seq gene expression data, with a focus on quality control. https://bioconductor.org/packages/release/bioc/html/scater.html
    - McCarthy et al. "Scater: pre-processing, quality control, normalisation and visualisation of single-cell RNA-seq data in R." Bioinformatics, 2017. https://doi.org/10.1093/bioinformatics/btw777

- `DropletUtils` - Provides a number of utility functions for handling single-cell (RNA-seq) data from droplet technologies such as 10X Genomics. This includes data loading, identification of cells from empty droplets, removal of barcode-swapped pseudo-cells, and downsampling of the count matrix. https://bioconductor.org/packages/release/bioc/html/DropletUtils.html
 
## Normalization

- `SCnorm` - normalization for single-cell data. Quantile regression to estimate the dependence of transcript expression on sequencing depth for every gene. Genes with similar dependence are then grouped, and a second quantile regression is used to estimate scale factors within each group. Within-group adjustment for sequencing depth is then performed using the estimated scale factors to provide normalized estimates of expression. Good statistical methods description. https://www.biostat.wisc.edu/~kendzior/SCNORM/
    - Bacher, Rhonda, Li-Fang Chu, Ning Leng, Audrey P Gasch, James A Thomson, Ron M Stewart, Michael Newton, and Christina Kendziorski. “SCnorm: Robust Normalization of Single-Cell RNA-Seq Data.” Nature Methods 14, no. 6 (April 17, 2017): 584–86. https://doi.org/10.1038/nmeth.4263.


## Batch effect

- `MNN` - mutual nearest neighbors method for single-cell batch correction. Assumptions: MNN exist between batches, batch is orthogonal to the biology. Cosine normalization, Euclidean distance, a pair-specific barch-correction vector as a vector difference between the expression profiles of the paired cells using selected genes of interest and hypervariable genes. Supplementary note 5 - algorithm. mnnCorrect function in the scran package https://bioconductor.org/packages/release/bioc/html/scran.html. Code for paper https://github.com/MarioniLab/MNN2017/
    - Haghverdi, Laleh, Aaron T L Lun, Michael D Morgan, and John C Marioni. “Batch Effects in Single-Cell RNA-Sequencing Data Are Corrected by Matching Mutual Nearest Neighbors.” Nature Biotechnology, April 2, 2018. https://doi.org/10.1038/nbt.4091.

- `scLVM` - a modelling framework for single-cell RNA-seq data that can be used to dissect the observed heterogeneity into different sources, thereby allowing for the correction of confounding sources of variation. Designed to correct for the cell cycle effect. Applied to naive T cells differentiating into TH2 cells. https://github.com/PMBio/scLVM
    - Buettner, Florian, Kedar N Natarajan, F Paolo Casale, Valentina Proserpio, Antonio Scialdone, Fabian J Theis, Sarah A Teichmann, John C Marioni, and Oliver Stegle. “Computational Analysis of Cell-to-Cell Heterogeneity in Single-Cell RNA-Sequencing Data Reveals Hidden Subpopulations of Cells.” Nature Biotechnology 33, no. 2 (March 2015): 155–60. https://doi.org/10.1038/nbt.3102.
    - Buettner, Florian, Naruemon Pratanwanich, Davis J. McCarthy, John C. Marioni, and Oliver Stegle. “F-ScLVM: Scalable and Versatile Factor Analysis for Single-Cell RNA-Seq.” Genome Biology 18, no. 1 (December 2017). https://doi.org/10.1186/s13059-017-1334-8. - f-scLVM - factorial single-cell latent variable model guided by pathway annotations to infer interpretable factors behind heterogeneity. PCA components are annotated by correlated genes and their enrichment in pathways. Docomposition of the original gene expression matrix to a sum of annotated, unannotated, and confounding components. Applied to their own naive T to TH2 cells, mESCs, reanalyzed 3005 neuronal cells. Simulated data. https://github.com/bioFAM/slalom


## Dimensionality reduction

- `CIDR` - Clustering through Imputation and Dimensionality Reduction. Impute dropouts. Explicitly deconvolve Euclidean distance into distance driven by complete, partially complete, and dropout pairs. Principal Coordinate Analysis. https://github.com/VCCRI/CIDR
    - Lin, Peijie, Michael Troup, and Joshua W. K. Ho. “CIDR: Ultrafast and Accurate Clustering through Imputation for Single-Cell RNA-Seq Data.” Genome Biology 18, no. 1 (December 2017). https://doi.org/10.1186/s13059-017-1188-0.

- `ZIFA` - Zero-inflated dimensionality reduction algorithm for single-cell data. Single-cell dimensionality reduction. Model dropout rate as double exponential, give less weights to these counts. EM algorithm that incorporates imputation step for the expected gene expression level of drop-outs. https://github.com/epierson9/ZIFA
    - Pierson, Emma, and Christopher Yau. “ZIFA: Dimensionality Reduction for Zero-Inflated Single-Cell Gene Expression Analysis.” Genome Biology 16 (November 2, 2015): 241. https://doi.org/10.1186/s13059-015-0805-z.

- `ZINB-WAVE` - Zero-inflated negative binomial model for normalization, batch removal, and dimensionality reduction. Extends the RUV model with more careful definition of "unwanted" variation as it may be biological. Good statistical derivations in Methods. Refs to real and simulated scRNA-seq datasets. https://bioconductor.org/packages/release/bioc/html/zinbwave.html
    - Risso, Davide, Fanny Perraudeau, Svetlana Gribkova, Sandrine Dudoit, and Jean-Philippe Vert. “ZINB-WaVE: A General and Flexible Method for Signal Extraction from Single-Cell RNA-Seq Data.” BioRxiv, January 1, 2017. https://doi.org/10.1101/125112.



## Clustering and visualization

- `Bisquit` - a Bayesian clustering and normalization method. https://github.com/sandhya212/BISCUIT_SingleCell_IMM_ICML_2016
    - Azizi, Elham, Ambrose J. Carr, George Plitas, Andrew E. Cornish, Catherine Konopacki, Sandhya Prabhakaran, Juozas Nainys, et al. “Single-Cell Map of Diverse Immune Phenotypes in the Breast Tumor Microenvironment.” Cell, June 2018. https://doi.org/10.1016/j.cell.2018.05.060.

- `celda` - CEllular Latent Dirichlet Allocation. Simultaneous clustering of cells into subpopulations and genes into transcriptional states. https://github.com/compbiomed/celda. Tutorials will be at https://github.com/compbiomed/celda_tutorials. No preprint yet.

- `CIDR` - Clustering through Imputation and Dimensionality Reduction. Impute dropouts. Explicitly deconvolve Euclidean distance into distance driven by complete, partially complete, and dropout pairs. Principal Coordinate Analysis. https://github.com/VCCRI/CIDR
    - Lin, Peijie, Michael Troup, and Joshua W. K. Ho. “CIDR: Ultrafast and Accurate Clustering through Imputation for Single-Cell RNA-Seq Data.” Genome Biology 18, no. 1 (December 2017). https://doi.org/10.1186/s13059-017-1188-0.

- `destiny` - R package for diffusion maps-based visualization of single-cell data. https://bioconductor.org/packages/release/bioc/html/destiny.html
    - Haghverdi, Laleh, Florian Buettner, and Fabian J. Theis. “Diffusion Maps for High-Dimensional Single-Cell Analysis of Differentiation Data.” Bioinformatics 31, no. 18 (September 15, 2015): 2989–98. https://doi.org/10.1093/bioinformatics/btv325. - Introduction of other methods, Table 1 compares them. Methods details. Performance is similar to PCA and tSNE. 

- `PhenoGraph` - discovers subpopulations in scRNA-seq data. High-dimensional space is modeled as a nearest-neighbor graph, then the Louvain community detection algorithm. No assumptions about the size, number, or form of subpopulations. https://github.com/jacoblevine/PhenoGraph
    - Levine, Jacob H., Erin F. Simonds, Sean C. Bendall, Kara L. Davis, El-ad D. Amir, Michelle D. Tadmor, Oren Litvin, et al. “Data-Driven Phenotypic Dissection of AML Reveals Progenitor-like Cells That Correlate with Prognosis.” Cell 162, no. 1 (July 2015): 184–97. https://doi.org/10.1016/j.cell.2015.05.047.

- `SC3` - single-cell clustering. Multiple clustering iterations, consensus matrix, then hierarhical clustering. Benchmarking against other methods. https://bioconductor.org/packages/release/bioc/html/SC3.html
    - Kiselev, Vladimir Yu, Kristina Kirschner, Michael T Schaub, Tallulah Andrews, Andrew Yiu, Tamir Chandra, Kedar N Natarajan, et al. “SC3: Consensus Clustering of Single-Cell RNA-Seq Data.” Nature Methods 14, no. 5 (March 27, 2017): 483–86. https://doi.org/10.1038/nmeth.4236.

- SIMLR - scRNA-seq dimensionality reduction, clustering, and visualization based on multiple kernel-learned distance metric. Comparison with PCA, t-SNE, ZIFA. Seven datasets. R and Matlab implementation. https://github.com/BatzoglouLabSU/SIMLR
    - Wang, Bo, Junjie Zhu, Emma Pierson, Daniele Ramazzotti, and Serafim Batzoglou. “Visualization and Analysis of Single-Cell RNA-Seq Data by Kernel-Based Similarity Learning.” Nature Methods 14, no. 4 (April 2017): 414–16. https://doi.org/10.1038/nmeth.4207.

- `SPRING` - a pipeline for data filtering, normalization and visualization using force-directed layout of k-nearest-neighbor graph. Web-based (10,000 cells max) https://kleintools.hms.harvard.edu/tools/spring.html) and GitHub https://github.com/AllonKleinLab/SPRING_dev 
    - Weinreb, Caleb, Samuel Wolock, and Allon M. Klein. “SPRING: A Kinetic Interface for Visualizing High Dimensional Single-Cell Expression Data.” Bioinformatics (Oxford, England) 34, no. 7 (April 1, 2018): 1246–48. https://doi.org/10.1093/bioinformatics/btx792.

- `SNN-Cliq` - shared nearest neighbor clustering of scRNA-seq data, represented as a graph. Similarity between two data points based on the ranking of their shared neighborhood. Automatically determine the number of clusters, accomodates different densities and shapes. Compared with K-means and DBSCAN using Purity, Adjusted Rand Indes, F1-score. Matlab, Python, R implementation. http://bioinfo.uncc.edu/SNNCliq/
    - Xu, Chen, and Zhengchang Su. “Identification of Cell Types from Single-Cell Transcriptomes Using a Novel Clustering Method.” Bioinformatics (Oxford, England) 31, no. 12 (June 15, 2015): 1974–80. https://doi.org/10.1093/bioinformatics/btv088.

- `viSNE` - the Barnes-Hut implementation of the t-SNE algorithm, improved and tailored for the analysis of single-cell data. Details of tSNE https://www.denovosoftware.com/site/manual/visne.htm, and the `Rtsne` R package https://cran.r-project.org/web/packages/Rtsne/index.html
    - Amir, El-ad David, Kara L Davis, Michelle D Tadmor, Erin F Simonds, Jacob H Levine, Sean C Bendall, Daniel K Shenfeld, Smita Krishnaswamy, Garry P Nolan, and Dana Pe’er. “ViSNE Enables Visualization of High Dimensional Single-Cell Data and Reveals Phenotypic Heterogeneity of Leukemia.” Nature Biotechnology 31, no. 6 (June 2013): 545–52. https://doi.org/10.1038/nbt.2594.

- `UCSC Single Cell Browser` - Python pipeline and Javascript scatter plot library for single-cell datasets. Pre-process an expression matrix by filtering, PCA, nearest-neighbors, clustering, t-SNE and UMAP and formats them for cbBuild. Stand-alone app on GitHub, https://github.com/maximilianh/cellBrowser, Demo that includes several landmark datasets, https://cells.ucsc.edu/


### Time inference

- A collection of 57 trajectory inference methods, https://github.com/dynverse/dynmethods#list-of-included-methods
    - Saelens, Wouter, Robrecht Cannoodt, Helena Todorov, and Yvan Saeys. “A Comparison of Single-Cell Trajectory Inference Methods: Towards More Accurate and Robust Tools,” March 5, 2018. https://doi.org/10.1101/276907. - Review of trajectory 29 inference methods for single-cell RNA-seq (out of 57 methods collected). Slingshot, TSCAN and Monocle DDRTree perform best overall. https://github.com/dynverse/dynverse

- `Monocle` - Temporal ordering of single cell gene expression profiles. Independent Component Analysis to reduce dimensionality, Minimum Spanning Tree on the reduced representation and the longest path through it. https://cole-trapnell-lab.github.io/monocle-release/
    - Trapnell, Cole, Davide Cacchiarelli, Jonna Grimsby, Prapti Pokharel, Shuqiang Li, Michael Morse, Niall J. Lennon, Kenneth J. Livak, Tarjei S. Mikkelsen, and John L. Rinn. “The Dynamics and Regulators of Cell Fate Decisions Are Revealed by Pseudotemporal Ordering of Single Cells.” Nature Biotechnology 32, no. 4 (April 2014): 381–86. https://doi.org/10.1038/nbt.2859.

- `SCUBA` - single-cell clustering using bifurcation analysis. Cells may differentiate in a monolineage manner or may differentiate into multiple cell lineages, which is the bifurcation event - two new lineages. Methods. Matlab code https://github.com/gcyuan/SCUBA
    - Marco, Eugenio, Robert L. Karp, Guoji Guo, Paul Robson, Adam H. Hart, Lorenzo Trippa, and Guo-Cheng Yuan. “Bifurcation Analysis of Single-Cell Gene Expression Data Reveals Epigenetic Landscape.” Proceedings of the National Academy of Sciences of the United States of America 111, no. 52 (December 30, 2014): E5643-5650. https://doi.org/10.1073/pnas.1408993111.


### Networks

- `GraphDDP` - combines user-guided clustering and transition of differentiation processes between clusters. Shortcomings of PCA, MDS, t-SNE. Tested on several datasets to improve interpretability of clustering, compared with other methods (Monocle2, SPRING, TSCAN). Detailed methods. https://github.com/fabriziocosta/GraphEmbed
    - Costa, Fabrizio, Dominic Grün, and Rolf Backofen. “GraphDDP: A Graph-Embedding Approach to Detect Differentiation Pathways in Single-Cell-Data Using Prior Class Knowledge.” Nature Communications 9, no. 1 (December 2018). https://doi.org/10.1038/s41467-018-05988-7. 


- `SCENIC` - single-cell network reconstruction and cell-state identification. Three modules: 1) GENIE3 - connect co-expressed genes and TFs using random forest regression; 2) RcisTarget - Refine them using cis-motif enrichment; 3) AUCell - assign activity scores for each network in each cell type. The R implementation of GENIE3 does not scale well with larger datasets; use arboreto instead, which is a much faster Python implementation. https://gbiomed.kuleuven.be/english/research/50000622/lcb/tools/scenic, https://github.com/aertslab/SCENIC, https://github.com/aertslab/GENIE3, https://github.com/aertslab/AUCell, https://github.com/tmoerman/arboreto, https://github.com/aertslab/pySCENIC
    - Aibar, Sara, Carmen Bravo González-Blas, Thomas Moerman, Vân Anh Huynh-Thu, Hana Imrichova, Gert Hulselmans, Florian Rambow, et al. “SCENIC: Single-Cell Regulatory Network Inference and Clustering.” Nature Methods 14, no. 11 (November 2017): 1083–86. https://doi.org/10.1038/nmeth.4463.
    - Davie et al. "A Single-Cell Transcriptome Atlas of the Aging Drosophila Brain" Cell, 2018 https://doi.org/10.1016/j.cell.2018.05.057

- SINCERA - identification of major cell types, the corresponding gene signatures and transcription factor networks. Pre-filtering (expression filter, cell specificity filter) improves inter-sample correlation and decrease inter-sample distance. Normalization: per-sample z-score, then trimmed mean across cells. Clustering (centered Pearson for distance, average linkage), and other metrics, permutation to assess clustering significance. Functional enrichment, cell type enrichment analysis, identification of cell signatures. TF networks and their parameters (disruptive fragmentation centrality, disruptive connection centrality, disruptive distance centrality). Example analysis of mouse lung cells at E16.5, Fluidigm, 9 clusters, comparison with SNN-Cliq, scLVM, SINGuLAR Analysis Toolset. Web-site: https://research.cchmc.org/pbge/sincera.html; GitHub: https://github.com/xu-lab/SINCERA; [Data](https://lungmap.net/breath-entity-page/?entityType=none&entityId=&entityLabel=&experimentTypes[]=LMXT0000000016) 
    - Guo, Minzhe, Hui Wang, S. Steven Potter, Jeffrey A. Whitsett, and Yan Xu. “SINCERA: A Pipeline for Single-Cell RNA-Seq Profiling Analysis.” PLoS Computational Biology 11, no. 11 (November 2015): e1004575. https://doi.org/10.1371/journal.pcbi.1004575.


## Differential expression

- Soneson, Charlotte, and Mark D Robinson. “Bias, Robustness and Scalability in Single-Cell Differential Expression Analysis.” Nature Methods, February 26, 2018. https://doi.org/10.1038/nmeth.4612. - Differential analysis of scRNA-seq data, 36 methods. Prefiltering of low expressed genes is important. edgeRQLFDetRate performs best. The conquer database, scRNA-seq datasets as RDS objects - http://imlspenticton.uzh.ch:3838/conquer/


- `MAST` - scRNA-seq DEG analysis. CDR - the fraction of genes that are detectably expressed in each cell - added to the hurdle model that explicitly parameterizes distributions of expressed and non-expressed genes. Generalized linear model, log2(TPM+1), Gaussian. Regression coeffs are estimated using Bayesian approach. Variance shrinkage, gamma distribution. https://github.com/RGLab/MAST
    - Finak, Greg, Andrew McDavid, Masanao Yajima, Jingyuan Deng, Vivian Gersuk, Alex K. Shalek, Chloe K. Slichter, et al. “MAST: A Flexible Statistical Framework for Assessing Transcriptional Changes and Characterizing Heterogeneity in Single-Cell RNA Sequencing Data.” Genome Biology 16 (December 10, 2015): 278. https://doi.org/10.1186/s13059-015-0844-5.

-  `SCDE`. Stochasticity of gene expression, high drop-out rate. A mixture model of two processes - detected expression and drop-out failure modeled as low-magnitude Poisson. Drop-out rate depends on the expected expression and can be approximated by logistic regression. https://hms-dbmi.github.io/scde/index.html
    - Kharchenko, Peter V., Lev Silberstein, and David T. Scadden. “Bayesian Approach to Single-Cell Differential Expression Analysis.” Nature Methods 11, no. 7 (July 2014): 740–42. https://doi.org/10.1038/nmeth.2967.

- `scDD` R package to identify differentially expressed genes in single cell RNA-seq data. Accounts for unobserved data. Four types of differential expression (DE, DP, DM, DB, see paper). https://github.com/kdkorthauer/scDD
    - Korthauer, Keegan D., Li-Fang Chu, Michael A. Newton, Yuan Li, James Thomson, Ron Stewart, and Christina Kendziorski. “A Statistical Approach for Identifying Differential Distributions in Single-Cell RNA-Seq Experiments.” Genome Biology 17, no. 1 (December 2016). https://doi.org/10.1186/s13059-016-1077-y.


## 10X Genomics

- Zheng, Grace X. Y., Jessica M. Terry, Phillip Belgrader, Paul Ryvkin, Zachary W. Bent, Ryan Wilson, Solongo B. Ziraldo, et al. “Massively Parallel Digital Transcriptional Profiling of Single Cells.” Nature Communications 8 (January 16, 2017): 14049. https://doi.org/10.1038/ncomms14049. - 10X technology. Details of each wet-lab step, sequencing, and basic computational analysis. scRNA- Seq dataset of 3000 peripheral blood mononuclear cells (PBMCs) from the 10X Genomics platform. https://support.10xgenomics.com/single-cell-gene-expression/datasets

- Cell Ranger, Loupe Cell Browser software download, https://support.10xgenomics.com/single-cell-gene-expression/software/downloads/latest

- Cell Ranger R kit, https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/rkit

### 10X QC

- `bxcheck` - Toolset for QC and processing 10x genomics data. https://github.com/pd3/bxcheck

## Data

- Multiple datasets, from the 10X Genomics website, https://support.10xgenomics.com/single-cell-gene-expression/datasets

- Buettner, Florian, Kedar N Natarajan, F Paolo Casale, Valentina Proserpio, Antonio Scialdone, Fabian J Theis, Sarah A Teichmann, John C Marioni, and Oliver Stegle. “Computational Analysis of Cell-to-Cell Heterogeneity in Single-Cell RNA-Sequencing Data Reveals Hidden Subpopulations of Cells.” Nature Biotechnology 33, no. 2 (March 2015): 155–60. https://doi.org/10.1038/nbt.3102.
    - `data/scLVM/nbt.3102-S7.xlsx` - Uncorrected and cell-cycle corrected expression values (81 cells x 7073 genes) for T-cell data. Includes cluster assignment to naive T cells vs. TH2 cells (GATA3 high marker). [Source](https://media.nature.com/original/nature-assets/nbt/journal/v33/n2/extref/nbt.3102-S7.xlsx)
    - `data/scLVM/nbt.3102-S8.xlsx` - Corrected and uncorrected expression values for the newly generated mouse ESC data. 182 samples x 9571 genes. [Source](https://media.nature.com/original/nature-assets/nbt/journal/v33/n2/extref/nbt.3102-S8.xlsx)

- Paul, Franziska, Ya’ara Arkin, Amir Giladi, Diego Adhemar Jaitin, Ephraim Kenigsberg, Hadas Keren-Shaul, Deborah Winter, et al. “Transcriptional Heterogeneity and Lineage Commitment in Myeloid Progenitors.” Cell 163, no. 7 (December 17, 2015): 1663–77. https://doi.org/10.1016/j.cell.2015.11.013. - 3′ MARS (massively parallel RNA single-cell)-Seq protocol with shallow sequencing (1,453 genes/cell) to examine heterogeneity across bone marrow resident myeloid progenitors, 2,686 cells. Batch-corrected UMI count matrix: 19 clusters. http://compgenomics.weizmann.ac.il/tanay/?page_id=649. Seurat (PMID: 29608179) clusters (Supplementary Data 2,https://www.nature.com/articles/nbt.4096#supplementary-information). GEO: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE72857
    - `Amit_2015/Supplementary_dataset_1.txt` - Cell metadata for IFNB response analysis. [Source](https://media.nature.com/original/nature-assets/nbt/journal/v36/n5/extref/nbt.4096-S3.txt)
    - `Amit_2015/Supplementary_dataset_2.txt` - Cell metadata for murine hematopoiesis analysis. [Source](https://media.nature.com/original/nature-assets/nbt/journal/v36/n5/extref/nbt.4096-S4.txt)
    - `Amit_2015` - Cell metadata for cross-species pancreatic islet analysis. [Source](https://media.nature.com/original/nature-assets/nbt/journal/v36/n5/extref/nbt.4096-S5.txt)
    - `Amit_2015/generate_clustering.tar.gz` - all the data and scripts required for reproducing the MARS-seq results. 913Gb. [Source](http://www.wisdom.weizmann.ac.il/~arkiny/Paul2015/generate_clustering.tar.gz)

- Cusanovich, Darren A., Andrew J. Hill, Delasa Aghamirzaie, Riza M. Daza, Hannah A. Pliner, Joel B. Berletch, Galina N. Filippova, et al. “A Single-Cell Atlas of In Vivo Mammalian Chromatin Accessibility.” Cell 174, no. 5 (August 2018): 1309-1324.e18. https://doi.org/10.1016/j.cell.2018.06.052. - Single-cell ATAC-seq, approx. 100,000 single cells from 13 adult mouse tissues. Two sequence platforms, good concordance. Filtered data assigned into 85 clusters. Genes associated with the corresponding ATAC sites (Cicero for identification). Differential accessibility. Motif enrichment (Basset CNN). GWAS results enrichment. All data and metadata are available for download as text or rds format at http://atlas.gs.washington.edu/mouse-atac/

- Nowakowski, Tomasz J., Aparna Bhaduri, Alex A. Pollen, Beatriz Alvarado, Mohammed A. Mostajo-Radji, Elizabeth Di Lullo, Maximilian Haeussler, et al. “Spatiotemporal Gene Expression Trajectories Reveal Developmental Hierarchies of the Human Cortex.” Science 358, no. 6368 (December 8, 2017): 1318–23. https://doi.org/10.1126/science.aap8809. - single-cell RNA-seq of human neuronal cell types. Dimensionality reduction, clustering, WGCNA, defining cell type-specific signatures, comparison with other signatures (Zeng, Miller). Supplementary material at http://science.sciencemag.org/content/suppl/2017/12/06/358.6368.1318.DC1 Table 5 has gene signatures.https://www.wired.com/story/neuroscientists-just-launched-an-atlas-of-the-developing-human-brain/. Controlled access data on dbGAP, https://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000989.v3.p1, summarized matrix with annotations is available on https://cells.ucsc.edu/?ds=cortex-dev


### Brain single-cell data

#### Human

- Darmanis, S., Sloan, S.A., Zhang, Y., Enge, M., Caneda, C., Shuer, L.M., Hayden Gephart, M.G., Barres, B.A., and Quake, S.R. (2015). A survey of human brain transcriptome diversity at the single cell level. Proc. Natl. Acad. Sci. USA 112, 7285–7290. - Single cell brain transcriptomics, human. Fluidigm C1 platform. Healthy cortex cells (466 cells) containing: Astrocytes, oligodendrocytes, oligodendrocyte precursor cells (OPCs), neurons, microglia, and vascular cells. Single cells clustered into 10 clusters, their top 20 gene signatures are in Supplementary Table S3. Raw data athttps://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE67835
    - `data/Brain/TableS3.txt` - top 20 cell type-specific genes
    - `data/Brain/TableS3_matrix.txt` - genes vs. cell types with 0/1 indicator variables.

- Nowakowski, Tomasz J., Aparna Bhaduri, Alex A. Pollen, Beatriz Alvarado, Mohammed A. Mostajo-Radji, Elizabeth Di Lullo, Maximilian Haeussler, et al. “Spatiotemporal Gene Expression Trajectories Reveal Developmental Hierarchies of the Human Cortex.” Science 358, no. 6368 (December 8, 2017): 1318–23. https://doi.org/10.1126/science.aap8809. - single-cell RNA-seq of neuronal cell types. Dimensionality reduction, clustering, WGCNA, defining cell type-specific signatures, comparison with other signatures (Zeng, Miller). 
    - `data/Brain/Nowakowski_2017_Tables_S1-S11.xlsx` - Table S5 has brain region-specific gene signatures. [Source](http://science.sciencemag.org/highwire/filestream/703290/field_highwire_adjunct_files/1/aap8809_Nowakowski_SM-Tables-S1-S11.xlsx) 

- Luo, Chongyuan, Christopher L. Keown, Laurie Kurihara, Jingtian Zhou, Yupeng He, Junhao Li, Rosa Castanon, et al. “Single-Cell Methylomes Identify Neuronal Subtypes and Regulatory Elements in Mammalian Cortex.” Science (New York, N.Y.) 357, no. 6351 (11 2017): 600–604. https://doi.org/10.1126/science.aan3351. - single-cell methylation of human and mouse neuronal cells. Marker genes with cell type-specific methylation profiles - Table S3, http://science.sciencemag.org/content/suppl/2017/08/09/357.6351.600.DC1

- Major Depressive Disorder Working Group of the Psychiatric Genomics Consortium et al., “Genetic Identification of Brain Cell Types Underlying Schizophrenia,” Nature Genetics 50, no. 6 (June 2018): 825–33, https://doi.org/10.1038/s41588-018-0129-5. - Cell-type specificity of schizophrenia SNPs judged by enrichment in expressed genes. scRNA-seq custom data collection. Difference between schizophrenia and neurological disorders.
    - `data/Brain_cell_type_gene_expression.xlsx` - Supplementary Table 4 - Specificity values for Karolinska scRNA-seq superset. Specificity represents the proportion of the total expression of a gene found in one cell type as compared to that in all cell types (i.e., the mean expression in one cell type divided by the mean expression in all cell types). Gene X cell type matrix. Level 1 (core cell types) and level 2 (extended collection of cell types) data. [Source](https://static-content.springer.com/esm/art%3A10.1038%2Fs41588-018-0129-5/MediaObjects/41588_2018_129_MOESM3_ESM.xlsx)

### Mouse

- The 1 million neuron data set from E18 mice, from the 10X Genomics website (https://support.10xgenomics.com/single-cell-gene-expression/datasets). R packages for its analyses: 
    - `TENxGenomics` - https://github.com/mtmorgan/TENxGenomics
    - `TENxBrainAnalysis` - https://github.com/Bioconductor/TENxBrainAnalysis

- Zeisel, A., Munoz-Manchado, A.B., Codeluppi, S., Lonnerberg, P., La Manno, G., Jureus, A., Marques, S., Munguba, H., He, L., Betsholtz, C., et al. (2015). Brain structure. Cell types in the mouse cortex and hippocampus revealed by single-cell RNA- seq. Science 347, 1138–1142. - 3,005 single cells from the hippocampus and cerebral cortex of mice. https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE60361, http://linnarssonlab.org/cortex/, and more on this site.
    - `data/Brain/Zeisel_2015_TableS1.xlsx` - Table S1 - gene signatures for Ependymal, Oligodendrocyte, Microglia, CA1 Pyramidal, Interneuron, Endothelial, S1 Pyramidal, Astrocyte, Mural cells. [Source](http://science.sciencemag.org/highwire/filestream/628248/field_highwire_adjunct_files/1/aaa1934_TableS1.xlsx)
    - `data/Brain/expression_mRNA_17-Aug-2014.txt` - 19,972 genes x 3005 cells. Additional rows with class annotations to interneurons, pyramidal SS, pyramidal CA1, oligodendrocytes, microglia, endothelial-mural, astrocytes_ependymal, further subdivided into 47 subclasses. [Source](https://storage.googleapis.com/linnarsson-lab-www-blobs/blobs/cortex/expression_mRNA_17-Aug-2014.txt)

- Carter, Robert A., Laure Bihannic, Celeste Rosencrance, Jennifer L. Hadley, Yiai Tong, Timothy N. Phoenix, Sivaraman Natarajan, John Easton, Paul A. Northcott, and Charles Gawad. “A Single-Cell Transcriptional Atlas of the Developing Murine Cerebellum.” Current Biology, September 2018. https://doi.org/10.1016/j.cub.2018.07.062. - scRNA-seq (10X Genomics) of murine cerebellum. 39245 cells (after filtering) from 12 time points, 48 distinct clusters. Cell Seek for online exploration, https://cellseek.stjude.org/cerebellum/ and https://gawadlab.github.io/CellSeek/. Approx. 83,000 cells (BAM files per time point) are available at https://www.ebi.ac.uk/ena/data/view/PRJEB23051. No annotations.




## Links

- http://hemberg-lab.github.io/scRNA.seq.course/.
- https://en.wikipedia.org/wiki/List_of_RNA-Seq_bioinformatics_tools#Single_cell_RNA-Seq
- https://github.com/crazyhottommy/RNA-seq-analysis#single-cell-rna-seq
- https://www.scrna-tools.org/
- https://github.com/seandavi/awesome-single-cell
- https://github.com/johandahlberg/awesome-10x-genomics
- https://davetang.org/muse/category/single-cell-2/

