# CaPD 1.0: Step-by-Step Tutorial

**Seung-Jin Park** <br>
**2023-08-01**

# Introduction

Proteogenomics, a combination of proteomics and genomics, is expected to bridge the gap be-tween cancer genotypes and phenotypes. It provides a comprehensive understanding of the downstream effects of genomic alterations on protein expression and post-translational altera-tions such as phosphorylation, acetylation, glycosylation, and ubiquitination. To facilitate easy and efficient analysis of cancer proteogenomic data, we developed CaPD, a specialized web-based cancer proteogenomic database including the most extensive proteogenomic datasets. CaPD contains 11 human tissues, 18 cancers, and 2139 samples, and consists of five intercon-nected steps that can also be utilized independently. The five steps include: i) analysis of the impact of mutations on protein expression; ii) genome-wide analysis of the impact of a mutation on transcriptomes, proteomes, and post-translational modifications (PTMs); iii) analysis and vis-ualization of the impact of a mutation on mRNA, protein, and PTM changes of a gene; iv) iden-tification of mutations associated with a specific gene expression change; and v) mutation-mutation associations. Through its five-step process, CaPD offers systematic and biologically insightful results. 

# Citation

If you find this tool useful, please cite:

___Seung-Jin Park and Seon-Young Kim. 2023. CaPD: A web-based Cancer Proteogenomic Database___


# Connection

As our platform is optimized for **the Google Chrome browser**, we recommend accessing it using Chrome. If you encounter any issues accessing the platform via the provided link, please report the problem by submitting an [issue](https://github.com/prosium/CaPD/issues).


# Step-by-Step Tutorial

## STEP 1. Finding Impactful Mutations: Analysis of the Impact of Mutations on Protein Expression.

<b>Brief introduction</b>: 

This process compares the protein abundance selected randomly from COSMIC cancer-associated genes or selected manually. We provide a plot that illustrates the impacts of mutations on the protein abundance. Through this analysis, we evaluate the impact of a specific mutation on the proteins in a particular tumor type. Target mutations selected from this analysis are used in the subsequent analyses (STEPs 2-5). *Details methods are referred to paper.*

<b>Example Command</b>: _L24-Manual-(TP53,NFE2L2,ARID1A,SYNE1,DNAH5)-(DNMT3A,GCLC,MAP3K1,ARID1A,MAP2K1)_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/104dbe91-691f-4f1b-b1b7-53872d812900" width="400" height="400">

<b>Caveats</b>: At least one significant relationship between MutGene and ExpGene must be present for it to be displayed.


## STEP 2. Target Screening: Genome-wide Analysis of the Impact of a Mutation on Transcriptomes, Pro-teomes, and PTMs.

<b>Brief introduction</b>: 

We compare the levels of transcriptome (x-axis) and proteome (y-axis, including phosphoproteome, glycoproteome, acetylproteome, ubiquitylome) using signed minus log10(p-value). The simultaneous observation of changes in the transcriptome and proteome is made possible by STEP 2. It may identify genes that experience cascade changes as a result of a particular mutation at the transcriptome, proteome, and PTM levels, either favorably (top right) or negatively (bottom left). Additionally, it can highlight genes that, despite no changes at the transcriptome level, show positive (upper center) or negative (lower center) changes at the proteome or PTM level. *Details methods are referred to paper.*

<b>Example Command</b>: _L24-NFE2L2_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/727803c6-aa91-469f-9c92-79a9bfd80d0a" width="350" height="400">

<b>Caveats</b>: Analyzing various data types may take some time as it can be a time-consuming process. However, this stage provides highly powerful and useful results. Please be patient.


## STEP 3. Multi-omics Heatmap: Analysis and Visualization of the Impact of a Mutation on the Change of mRNa, Protein, and PTM of a Gene.

<b>Brief introduction</b>: 

This step analyzes and visualizes the relationship between a mutation and a target gene. We plot the normalized value and results of significance test in possible datatypes such as transcriptome, proteome, and PTMs between mutated and wild-type samples. This analysis allows users to explore the relationship between a mutated gene and its target gene at various levels. *Details methods are referred to paper.*


<b>Example Command</b>: _L24-NFE2L2-GCLC_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/a9256c96-1775-4cfd-aab0-87c21a793b42" width="430" height="400">


## STEP 4. Finding Mutations: Identification of Mutations Associated with a Specific Gene Expression Change.

<b>Brief introduction</b>: 

This step allows users to identify other mutations affecting a target gene of interest. While a mutation identified in the previous step may significantly regulate the abundance of a specific gene, the target gene may be regulated by other mutations as well. When users input a target of interest, this analysis tests all the other mutations against the target of interest and provides a plot showing both positive and negative associations between other mutations and the target of interest. *Details methods are referred to paper.*

<b>Example Command</b>: _L24_Acetylproteome_GCLC:A560K_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/791cc380-0888-4c66-acdc-37b29bb13cfa" width="400" height="430">


## STEP 5. Analysis of Mutation-Mutation Associations.

<b>Brief introduction</b>: 

This step allows users to explore mutation-mutation associations on a genome-wide scale. Taking a single mutation as an input, this analysis calculates the interaction between a mutation of interest and all other mutations and plot the result. This analysis identifies both co-occurring and mutually exclusive relationships that a specific mutation possesses. *Details methods are referred to paper.*

<b>Example Command</b>: _L24-NFE2L2_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/925b9d16-ee96-4bbf-8323-023c13278f98" width="380" height="400">




# Support

If you have any issues, bug reports or feature requests please feel free to raise an issue on Github [page](https://github.com/prosium/CaPD/issues).
