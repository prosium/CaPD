# CaPD 1.0: Step-by-Step Tutorial



**Seung-Jin Park** <br>
**2023-08-12**

# Introduction

With the advancements in cancer proteogenomics, various datasets have been made publicly available. Particularly, cancer proteogenomics data from different cancer types using various sequencing (WGS, WES, or RNA) or LC-MS/MS techniques, with sample sizes ranging around 100, have been generated, primarily centered around CPTAC. These datasets provide crucial information for the development of cancer treatment strategies and prognostic predictions.

## Citation

If you find this tool useful, please cite:

___Seung-Jin Park, Seon-Young Kim. 2023. HCP: Web-based proteogenomic analysis database in cancer. [NAR. PMID:30303030](https://doi.org)___


## Connection

As our platform is optimized for **the Google Chrome browser**, we recommend accessing it using Chrome. If you encounter any issues accessing the platform via the provided link, please report the problem by submitting an [issue](https://github.com/prosium/hcpdb/issues).

## Construction

As shown in the table below, we collected proteogenomics data from 1,237 samples across 10 tumor types from [CPTAC](https://proteomics.cancer.gov/programs/cptac).

<details>
<summary>Data Summary</summary>

|StudyType|TumorType|Subtype|Sample|DataType|PMID|
|:---:|:---:|:---:|---:|:---:|:---:|
|CPTAC|BRCA|Primary|122|MTPFA|[33212010](https://pubmed.ncbi.nlm.nih.gov/33212010/)
|CPTAC|COAD|Primary|110|MTPF|[31031003](https://pubmed.ncbi.nlm.nih.gov/31031003/)
|CPTAC|GBM|Primary|99|MTPFA|[33577785](https://pubmed.ncbi.nlm.nih.gov/33577785/)
|CPTAC|HNSCC|HPV(-)|108|MTPF|[33417831](https://pubmed.ncbi.nlm.nih.gov/33417831/)
|CPTAC|ICC|Primary|262|MTPF|[34971568](https://pubmed.ncbi.nlm.nih.gov/34971568/)
|CPTAC|LSCC|Primary|108|MTPFAU|[34358469](https://pubmed.ncbi.nlm.nih.gov/34358469/)
|CPTAC|LUAD|Primary|110|MTPFA|[32649874](https://pubmed.ncbi.nlm.nih.gov/32649874/)
|CPTAC|OV|High_grade|83|MTPFG|[27372738](https://pubmed.ncbi.nlm.nih.gov/27372738/)
|CPTAC|PDAC|Primary|140|MTPF|[34534465](https://pubmed.ncbi.nlm.nih.gov/34534465/)
|CPTAC|UCEC|Primary|95|MTPFA|[32059776](https://pubmed.ncbi.nlm.nih.gov/32059776/)
|OTHERS|BRCA|TNBC|71|MTPF|[36001024](https://pubmed.ncbi.nlm.nih.gov/36001024/)
|OTHERS|HCC|HBV(+)|158|MTPF|[31585088](https://pubmed.ncbi.nlm.nih.gov/31585088/)
|OTHERS|LUAD.1st|Never-smoker|102|MTPF|[32649875](https://pubmed.ncbi.nlm.nih.gov/32649875/)
|OTHERS|LUAD.2nd|Primary|103|MTPF|[32649877](https://pubmed.ncbi.nlm.nih.gov/32649877/)
|OTHERS|OV|Low_grade|14|MTPF|[36528667](https://pubmed.ncbi.nlm.nih.gov/36528667/)


또한 Consortium 외 데이터를 5 tumor type에서 448 samples를 추가하여 다양한 tumor type에서 proteogenomics 분석을 수행할 수 있게 하였습니다.

</details>


<details>
<summary> Additional information on CPTAC </summary>

CPTAC, which stands for Clinical Proteomic Tumor Analysis Consortium, is a large-scale research program focused on cancer studies sponsored by the National Cancer Institute (NCI) in the United States. The primary goal of CPTAC is to provide comprehensive biological information on various types of cancer including genomics and proteomics. This involves understanding protein changes involved in cancer initiation and progression and developing personalized treatment strategies based on high-throughput data. As part of this effort, elaborate proteogenomics data generated from advanced LC-MS/MS techniques have been made publicly available. These datasets enable protein expression profiling, mutation analysis, and investigation of cancer mechanisms across different types of cancer, thereby enhancing our understanding of their interrelationships.

</details>

# Step-by-Step Tutorial

## Step1. Identifying effective mutations that significantly modulate the protein abundance of cancer-associated genes.

<b>Brief introduction</b>: 

This process involves comparing the protein abundance of 318 cancer-associated genes, obtained from [COSMIC](https://cancer.sanger.ac.uk/cosmic), between mutations and WT in each tumor type. We provide the plot that illustrate the impacts of the top N mutations on the protein abundance of n randomly selected genes out of the 318 total genes. Through this analysis, we can identify the association between a specific mutation and CAG protein in a particular tumor type, as well as detect variable mutation within a tumor type. Lastly, this analysis enables us to select target mutations necessary for future investigations. 

<b>Methods</b>:

First, we selected the top N mutations based on their _frequency_ and randomly chose n genes from the CAG genes using the [Python random library](https://docs.python.org/3/library/random.html). Subsequently, we calculated the p-value using [the Wilcoxon rank-sum test](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ranksums.html) from scipy to compare the protein abundance in patients with mutations to that of WT patients. signed minus log<sub>10</sub>(_p_-value) was computed to represent numerical distinctions between mutated and WT tumors, with the symbols '+' and '-' indicating the upregulation and downregulation of mRNA, proteins, phosphosites, and acetylsites, respectively. For the sake of conciseness, we divided protein abundance differences into four categories: [0, 1), >1, [-1, 0), <-1 and p-value into four categories: (0.01, 0.05], (0.001, 0.01], <0.001, ns too.

<b>Example Command</b>: _CPTAC-LUAD-10-40_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/5b373c10-584d-4bb9-bb7c-6be13df86d58" width="600" height="700">



## Step2. Screening Impact of the mutation across all multiomics levels.

<b>Brief introduction</b>: 

We compare the levels of transcriptome (x-axis) and proteome (y-axis, including phosphoproteome, glycoproteome, acetylproteome, metabolome, ubiquitylome) using signed minus log<sub>10</sub>(_p_-value). This allows us to identify genes or phosphosignaling that are regulated at various levels. For example, if there are no significant changes at the transcriptome level but a significant change is observed in the phosphoproteome, we can identify signaling initiated from post-translational modifications. Alternatively, we can also identify genes that cascade from the transcriptome to phosphoproteome level. The plot we provide is an interactive plot, allowing users to hover over data points to view computed values and zoom in on specific areas and users to download figure or data used for figure.

<b>Methods</b>:

First, we categorized patients into two groups: those with a specific mutation and those without (WT). Then, we performed the [T-test of two independent samples](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_ind.html) from scipy for each datatype separately. We represented the results as signed minus log<sub>10</sub> (_p_-value). The differences were calculated using the mean difference. Subsequently, we sorted the proteome data based on the transcriptome data and plotted them.

<b>Example Command</b>: _CPTAC-LUAD-EGFR_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/a182609e-df59-4cae-8d28-ad4d1a8e5034" width="600" height="910">



## Step3. Association the mutation with the gene

<b>Brief introduction</b>: 

To gain a deeper understanding of the relationship between mutations and specific gene changes, we have constructed this page. As mentioned earlier, mutations can impact at various levels, including transcriptome, proteome, and phosphoproteome. Therefore, we tested for significant changes in abundance differences at all levels such as proteome, phosphoproteome, acetylome, or others of a specific gene when a mutation occurred. We represented the raw values on the heatmap, with samples plotted on the x-axis and datatype on the y-axis.

<b>Methods</b>:

First, we categorized patients into two groups: those with a specific mutation and those without (WT). Then, we performed the [T-test of two independent samples](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_ind.html) from scipy for each datatype separately. Fianlly we plotted complex heatmap using [iheatmap](https://docs.ropensci.org/iheatmapr/index.html).

<b>Example Command</b>: _CPTAC-LUAD-EGFR-PTPN11_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/aac866ef-834a-4b50-918e-3a86a5e4369e" width="600" height="680">



## Step4. Finding effective mutations using Inverse probability.

<b>Brief introduction</b>: 

Although a genomic change identified in the previous step may significantly regulate the abundance of a specific gene, we can observe that a particular gene is not regulated solely by that genomic change. While most researchers hope that the identified genomic change is the primary factor regulating the expression, in reality, this is often not the case. Most researchers hope that the identified genomic change is the primary factor regulating the expression. However, in reality, this is often not the case. For example, a single genomic change may regulate the abundance of a gene, but it can also frequently co-regulate with other genomic changes, although to lesser significant than first genomic change. Furthermore, genomic changes that regulate the expression of the gene in the opposite direction will also be important. We conducted tests for all genomic changes in relation to these factors and plotted positively and negatively regulated genomic changes.

<b>Methods</b>:

First, we categorized patients into two groups: those with a specific mutation and those without (WT) at each mutation repetitively. Then, we performed the [T-test of two independent samples](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_ind.html) from scipy between mutation group and WT group. Fianlly we plotted complex heatmap using [iheatmap](https://docs.ropensci.org/iheatmapr/index.html).

<b>Example Command</b>: _CPTAC-LUAD-Phosphoproteome-PTPN11:Y62y_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/62727f93-b17e-4b40-8ad4-adab1d7959a7" width="600" height="750">


## Step5. Genome-wide Co-occurrent or mutually exclusive test of Mutations.

<b>Brief introduction</b>: 

We constructed a Step5 to comprehensively investigate the relationship of effective mutation(s) discovered so far on a genome-wide scale. Taking a single mutation as input, we calculated the interaction between this mutation and all other mutations occurring genome-wide and plotted the results. Through this analysis, we were able to determine both the co-occurring and mutually exclusive relationships that a specific mutation possesses. This suggests that the mutation may have a synergistic effect in regulating a specific abundance or phospho signaling, or the two mutations may act in opposing directions each other.

<b>Methods</b>:

First, we divided the patients into two groups: those with a specific mutation and those without (WT) based on the mutations entered by the user. We then performed [the pair-wise Fisher's Exact test](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.fisher_exact.html) for three or more mutations in the cohort, and represented them in different colors according to the calculated Odds ratio for each mutation.

<b>Example Command</b>: _CPTAC-LUAD-EGFR_

<b>Results</b>: 

<img src="https://github.com/prosium/repository1/assets/94524627/5dce5f9c-a25c-431f-95c1-d4e0532e249e" width="600" height="750">
