# BIOC3301
Code available for Anita Waltho BIOC3301 
Datasets from 2016 and 2017 were procressed on UCL Legion according to bash scripts:
2016_cr_join_no_golay.sh
and
2017_cr_no_golay.sh
The standard outputs were: 2016_stdout and 2017_stdout 

# Validate mapping file command (Ensure mapping file compatibility with QIIME)
validate_mapping_file.py
-i map.tsv
-o /map

# Demultiplexing (split libraries)command
split_libraries_fastaq.py
-i read1.fastq.gz
-b barcode.fastq.gz
-m map.tsv./map/map_corrected.txt
-o slout/

# Pick OTUs command (Picking OTU with Greengenes closed reference)
parallel_pick_otus_uclust_ref.py
-i /slout/seqs.fna
-o /otus/uclust_ref_picked_otus
-r /qiime1/lib/python2.7/site-packages/qiime_default_reference/gg_13_8_otus/rep_set/97_otus.fasta 

# Make OTU table command
make_otu_table.py
-i /otus/uclust_ref_picked_otus/seqa_otus.txt
-t /qiime1/lib/python2.7/site-packages/qiime_default_reference/gg_13_8_otus/taxonomy/97_otu_taxonomy.txt
-o /otus/otu_table.biom

# Summary statistsics of OTU table command
biom_summarize_table.py
-i /otus/otu_table_mc2_w_tax_no_pynast_failures.biom

# merge BIOM-formated tables command
merge_otu_tables.py
-i ./2016/otus/otu_table.biom,./2017/otus/otu_table.biom
-o merged_otu_table.biom
Generating phylogenic trees: 2016/otus and 2017/otus


Further analysis ran using QIIME 1.9.1 on Macboook Terminal:
source activate qiime1

#  Core diversity analyses command(Generates alpha- and beta-diversity and taxonomic bar plots)
core_diversity_analyses.py 
-i /merged_otu_table.biom 
-m /map/map.tsv_corrected.txt 
-t /otus/97_otus.tree 
-e 371590 
-o matrix.html

# Statistically compare taxa level 2 (L2) Phyla abundance between 2016 and 2017 with ANOVA commands
summarize_taxa.py 
-i /merged_otu_table.biom 
-L 2 
-o taxa_summaries

group_significance.py 
-i /merge_otu_table_L2.biom 
-m /map.tsv_corrected.txt 
-c Year 
-o anova_tests_L2.txt

# Visually compare Phyla abundance between 2016 and 2017 by bar plots:
summarize_taxa_through_plots.py 
-i /merge_otu_table.biom 
-m /map.tsv_corrected.txt 
-c Year 
-o taxa_summary_by_year

# Generate heatmap of samples at Phyla level command
make_otu_heatmap.py 
-i /merge_otu_table_L2.biom 
-o heatmap.pdf

# Generate biplot command
jackknifed_beta_diversity.py 
-i /merged_otu_table.biom 
-t /otus/97_otus.tree 
-m /map.tsv_corrected.txt 
-e 371590 
-o jack

# Generate clustered phylogenic tree from jackknifed_beta_diversity
make_bootstrapped_tree.py 
-m /jack/unweighted_unifrac/upgma_cmp/master_tree.tre 
-s /jack/unweighted_unifrac/upgma_cmp/jackknife_support.txt 
-o /jackknife_named_nodes.pdf
