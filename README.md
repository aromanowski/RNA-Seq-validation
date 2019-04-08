# RNA-Seq-validation

Author: Paulo Flores : 2019

Contact: Paulo.Flores@hutton.ac.uk / paulorapazote@gmail.com

"RNA-Seq will be validated with High-Resolution HR-RTPCR data"

# Description of the algorithm

This algorithm (HR-RTPCR_RNA-Seq_Comparison.sh) is a collection of 7 small bash shell scripts that associate HR-RTPCR data with a transcriptome previously quantified with SALMON.

Description of the individual scripts (modules):

Module 1 : Blast generates a transcriptome database with the transcriptome supplied in fasta format; The primers sequence are blasted (blastn) to the previous database;

Module 2 :

Module 3 :

Module 4 :

Module 5 :

Module 6 :

Module 7 :

# Tools and steps needed before running the algorithm:

Before running the HR-RTPCR_RNA-Seq_Comparison.sh algorithm was necessary to run SALMON, a pseudo alignment tool (algorithm tested with SALMON version 0.8.2). We aligned each of our RNA-Seq read samples to the reference transcriptome (transcriptome.fasta file) after index generation. Each SALMON output sample must be in a individual folder, line 29 of the algorithm contains the path to the folder where the samples are. 

Also, it is necessary ncbi blast tool (algorithm tested with version ncbi-blast-2.2.28+), path mentioned lines 42 and 50.

Threads, we run the algorithm with 4 threads (algorithm lines 2 and 50)

# Input Files:

1. transcriptome.fasta file, this file contains the transcript sequences in fasta format. The transcript headers can not contain empty spaces. Algorithm lines 20 (path to the folder where is the transcriptome) and line 22 (transcriptome file name) identify the folder location and transcriptome fasta file name we used.

2. PrimersSequences.fasta, this file contains the primer sequences in fasta format. Each pair of primers (reverse and forward) have similar name but end with different terminations: _R (reverse) and _F (forward), example - Hv43_R and Hv43_R. 

3. rtPCR_productsAndProportions.txt (file located in the same folder where we run the algorithm), tab-delimited text file containing:

Column (1) primer names without _R or _F termination (previous example - Hv43 and Hv43); 

Column (2) HR-RT PCR product size (the computed nucleotide distance between primer pairs);

Columns (3), (4), (..) - individual sample proportions of each product primer;

Example of rtPCR_productsAndProportions.txt file:


Primer 	Size	SAMPLE1	SAMPLE2	SAMPLE3	SAMPLE4	SAMPLE5

Hv43C	228	0.03	0.01	0.00	0.00	0.00

Hv43C	251	0.02	0.02	0.00	0.00	0.00

Hv43C	263	0.16	0.15	0.00	0.00	0.00

Hv43C	388	0.45	0.51	0.00	0.00	0.00

Hv43C	391	0.09	0.08	0.00	0.00	0.00

Hv43C	403	0.19	0.17	0.00	0.00	0.00

Hv43C	540	0.06	0.06	0.00	0.00	0.00


# Output Files:
Complete-PrimerBestPairs-data.txt file contains the principal results
FileWithAllSampleTPMs.txt contains the list of transcripts and TPM per sample (clustered)
Other_files folder contains intermediate files
# Running the algorithm
bash ./HR-RTPCR_RNA-Seq_Comparison.sh
