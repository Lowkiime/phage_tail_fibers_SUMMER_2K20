# phage_tail_fibers_SUMMER_2K20

I plan to continue working on this project now that my internship is over, only at a slower rate.

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

Programs used:

NCBI Genome Workbench Version  3.4.1

CD HIT Server cd-hit accessed 6/22/2020

NCBI Magic-Blast Version 1.5.0

R STUDIO Version 1.3.959

MAFFT Version 7.467

FigTree Version 1.4.4

MEGA X Version 10.1.8 build 10200331

AliView Version 1.26

HMMER Version 3.3

NCBI Batch Entrez Accessed from 5/18/2020 to 8/3/2020

NCBI TBLASTN Accessed from 6/20/2020 to 8/3/2020

First metagenomic dataset:

https://www.ebi.ac.uk/metagenomics/search#analyses

https://www.ebi.ac.uk/ena/browser/view/PRJNA304204

This dataset from China was made into a Blast database using Magic Blast and then used as a local subject database in NCBI Genome Workbench to run tblastn with
the 157 sequences in the file working_70_cdhit.fasta as query.
No hits were found using tblastn with parameters set at word size=3, e-value=0.01, and threshold=13; however, there were 3 hits with the parameters set at size=3, 
e-value=0.1, and threshold=13.

The 2 tblastn subject data files were retrieved from https://www.ebi.ac.uk/metagenomics/search#analyses followed by unzipping the files and converting them to fasta format in the command line. Next, each file was made into a blast database and the query sequences in the file working_70_cdhit.fasta blasted against eavh using tblastn with parameters set as: -max_target_seqs 2, max_hsps 1, evalue 10, with outfmt '7. The best hits were selected in R studio based on three catgories and the seqids saved and duplicates filtered out. Those sequences with evalue<0.1, or qcovs>40% ,or pident>57% were combined and saved. The corresponding sequences from each of the seqids was extracted from the two blast databases. The file 300reads.fasta contains these sequences. 

Second BH set of file from https://www.ebi.ac.uk/metagenomics/analyses/MGYA00345647#download

Large set of environmental metagenomes in file Subject metagenomes.txt from https://www.ncbi.nlm.nih.gov/bioproject/?term=txid1070528[Organism:noexp]

