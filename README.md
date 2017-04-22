# BIOC3301
Code available for Anita Waltho BIOC3301 

ABSTRACT:
For centuries the huge microbial diversity of the 4-6 x1030 prokaryotic cells on our planet has remained largely undiscovered. Due to recent breakthroughs in culture-independent genomic analyses and next-generation sequencing (NGS) we have begun to uncover the >99% of microbial species previously unclassified. Following in the footsteps of largescale metagenomics projects like the Earth Microbiome Project, we aimed to sequence, classify and compare the soil microbiome of a Central London park from 2016-2017. Using the Illumina MiSeq platform we obtained 5 million 253-bp sequences from 4 samples in 2016 and 11 million 251-bp sequences from 8 samples in 2017. 73.1% of reads from 2017 and 39.4% of reads from 2016 were successfully annotated. Across all samples there was significant alpha-diversity with a wide variety of bacterial phyla. As reported by previous literature, acidobacteria, proteobacteria and verrucomicrobia were the most abundant phyla in this ecosystem. Surprising, beta-diversity was only weakly correlated with the year the sample was taken. The largest variation in microbial communities existed within the 2017 samples, with samples 17.3 and 17.6 varying significantly. Ultimately, this study serves as a key example of the ease of employing metagenomics technology to even small-scale projects, demonstrating its wide-range of applications which will completely redefine microbiology in future years.


This resulting sequence data was processed using QIIME (Quantitative Insight Into Microbial Ecology) 1.9.1 on UCL legion. 
Pre-processing was carried out (removing primers and adapters, demultiplexing and quality filter).
This was followed by close reference based picking of OTUs with Greengenes using buclust to build an OTU table. 

Further sequence analysis was conducted on the sequence data from both years using QIIME on MacBook Terminal through Miniconda command line. 
