# phage_tail_fibers_SUMMER_2K20
Work related code (R)

This is an ongoing active project.

This is a repository of the commands I used to filter the blast_data provided for analysis. The code can be run in the R terminal.

The focus of this project is to identify novel phages (viruses that infect bacteria) that could be used to target antibiotic resistant bacterial infections
from environmental virus metagenomes from various samples such as the pacific ocean or soil.
The project began by comparing statistically significant alignments between charachterized viral tail fiber proteins (which are responsible for host specificity) 
and bacterial tail fiber proteins (many of which are from pathogenic taxa) using E value, coverage, and percent identity as the filtering parameters in R.
The bacterial tail fiber protein from each selected significant alignment are aligned against each other using Muscle (in MEGA) or MAFFT and phylogentic trees 
infereed using MEGA and visualized using Figtree to observe the diversity of the selected taxa. The selected bacterial tail fiber proteins are evidence that these
bacterial species have been infected by a phage in the past and therefore is a potential target for phage therapy in the future.   
The selected bacterial tail fiber proteins will be searched using tblastn against different viromes from the ocean and soil where novel viruses with specificity 
for pathogenic bacteria will hopefully be identified. These novel phages will be further investigated for possible use in phage therapy. 

No manual sorting was performed on any of the following files for reproducibility. See Github repository for R commands used and below 
for links to other sources used.

Files:

blast_data contains the original data provided by Dean and contains 89965 alignments of a bacterial and a viral protein in 13 variables.

working_70_cdhit contains 157 unique bacterial protein sequences that were filtered from blast_data with e value < 0.01, qcovs > 80%, 
pident > 35% using tidyr package in R followed by similar sequence clustering using the UCSD CD HIT web server with the similarity (identity)
threshold set to 70%, this clustered sequences with over 70% identity to one representative sequence from the set which was retained.
The file extension specifies what form the data is in e.g. sseqid, fasta, tree, alignment, etc.

working contains 384 unique bacterial protein sequences that were filtered from blast_data with e value < 0.01, qcovs > 80%, pident > 35%
using tidyr package in R. This dataset contains numerous very similar sequences as no clustering was done.

working_viruses contains 211 unique viral sequences sorted from blast_data that correspond with the sequences in working (211<384)
due to virus aligning with more than one bacterial protein). Sorting parameters were e value < 0.01, qcovs > 80%, pident > 35% 
using tidyr package in R.

working_V contains working concatenated with working_viruses.

working_70_cdhit_V contains working_70_cdhit concatenated with working_viruses.

->Similar sequence clustering based on identity was performed using CD HIT through the following server at UCSD: 
http://weizhong-lab.ucsd.edu/cdhit-web-server/cgi-bin/index.cgi?cmd=cd-hit 
->For all clustering jobs the sequence identity cut-off was set to 0.7; therefore, sequences with greater than 70% identity were clustered
together and represented by one sequence chosen from the cluster. All other settings were left in the default setting.
->Batch Entrez was used to recover the fasta files for selected sequences. 
->Github repository with annotated R commands: https://github.com/Lowkiime/SUMMER20/blob/master/work
