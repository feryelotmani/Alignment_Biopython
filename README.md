# SARS-CoV-2 Wuhan vs Omicron: a simple alignment checked with Nextclade

A bioinformatics project. I compared the Wuhan-Hu-1 reference genome with an Omicron BA.1 genome using a basic pairwise alignment in Biopython, and I checked my results against Nextclade.

# Data

Both sequences come from NCBI Nucleotide (GenBank):

Sequence	Accession	Description
Reference	NC_045512.2	SARS-CoV-2 isolate Wuhan-Hu-1, complete genome
Omicron	OM011974.1	[isolate SARS-CoV-2/human/MAR/CNRST-HM36/2021, check the GenBank record]

# Method 
Read the two FASTA files with Biopython (SeqIO).
Run a global pairwise alignment with Bio.Align.PairwiseAligner, using the Wuhan sequence as the target and the Omicron sequence as the query. Scoring: [Biopython defaults: match 1, mismatch 0, gap 0, check the printed parameters in the notebook].
Compare the aligned bases column by column to list the substitutions. Insertions and deletions are not counted.
Put the results in a table with pandas.
Ran the same Omicron sequence through Nextclade and compared its substitution list with mine.

# Results

My alignment found 58 substitutions, including the well-known C241T and C3037T.
Nextclade assigned the sequence to clade 21K (Omicron, BA.1), reported no non-ACGTN bases, and listed 55 substitutions.
54 of the 55 Nextclade substitutions were also in my list: 15 with identical positions and 39 shifted by +6 after position 22204.
1 Nextclade substitution (C21762T) was missing from mine, and my list had 4 extra (T22196G, T22198G, A22199C, T22209A).

# Limitations
My positions are alignment positions, not reference positions. After the 9-nucleotide insertion at 22204 (and a neighbouring 3-nucleotide deletion), they are shifted by +6 compared with Nextclade.
The four extra substitutions and the missing one are all near that insertion and deletion. They are probably alignment artifacts.
Only one Omicron sequence was analysed, so the findings describe this sample and not the variant as a whole.
Nextclade, which aligns in a codon- and indel-aware way, is the reliable tool for mutation calling. This project shows why.

## A full written report is posted on my linkedin profil ckeck it for more informations

# How to run
Open the notebook in Google Colab.
Upload the two FASTA files from data/ to your Google Drive.
Update the file paths in the third code cell, then use Runtime → Run all.

# Tools

Python, Biopython (Cock et al., 2009), pandas, Google Colab, Nextclade (Aksamentov et al., 2021).

# Author
Feryel Otmani. feel free to share your thoughts and opinions.
