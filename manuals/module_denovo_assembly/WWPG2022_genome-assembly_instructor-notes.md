# WWPG_module5_genome-assembly_instructor-notes


## STEP 1. Checking raw sequencing data before assembly

### FastQC / MultiQC output
**Q. What are the similarities / differences between read 1 and read 2?**

Should see similar FastQC profiles between read 1 and read2, however, the quality scores of read 2 will be a little worse than in read 1. This is because the 

**Q. Are the base quality and nucleotide frequency distributions relatively level, or are they uneven?**

The base quality decreases over the length of the read.

The nucleotide frequency distribution should be relatively even across the read, but the frequency will be determined by the GC content of the genome. Different library preps / enzymes / shearing may also influence the distribution

### 2. Kraken
**Q. What proportion of the reads are “unclassified”, and therefore potentially S. mansoni reads?**

Kraken works by matching kmers in the reads against kmers in the database. The kraken database contains primarily bacterial and viral reference sequnences from NCBI, as well as human and mouse. There is no parasites, ie, S. mansoni, so any S. manoni reads will be “unclassified”

**Q. What looks to be the main contaminant? Why might this be so?**

Main contaminant is mouse reads, as the S. mansoni lifecycle maintained at Sanger uses mouse (instead of human) as the mammalian host. The introduction of the manual gives this hint away.


## STEP 2. Estimating your genome size from raw sequence data

**Q. what is my predicted genome / chromosome size? how does it compare to the expected size?**
 
Should be relatively close. Not exact. This is simply to illustrate you can get a fair estimate from nothing more than the reads themselves, before doing any analysis.

Knowing this could help, for example, when doing a genome assembly as having some expectation of what assembly size to expect.

**Q. what does changing the kmer length do?**

In this case, it doesnt do a lot. However, choosing a kmer length is a tradeoff between sensitivity and specificity. 
- longer kmers will be more specific, but there will be less of them
- shorter kmers will be more sensitive, but a lot more


## Step 3: Performing a genome assembly using either Illumina short read or Pacbio long read data

***NOTE: dont get them to run the MINIMAP assembly. It “usually” works on decent modern 
computers, but will likely fail on home computers.*** 

**Q. how do my assemblies compare to the expected size of chomosome IV?**

Chromosome IV is about 42 Mb - this is mentioned in the introduction.

Canu and miniasm assemblies are pretty similar in size

Spades assembly is much smaller both pacbio assemblies. Pacbio reads can span repeats much more efficiently than Illumina short reads, so they are better represented in the pacbio assembly. In Illumina assemblies, the repeats get highly collapsed, so the are represented but in much fewer copies.
 
 
**Q. what is the impact of long reads versus short reads on assembly contiguity?**

The Pacbio assemblies are much more contiguous and are in fewer pieces than the Illumina assembly. As above, repeats cause less of a problem 

It can be very difficult to sequence through repeats that are longer than the sequencing reads themselves.
- Pacbio = long reads that are multi 1000s bp long (some very long up to 100 kb)
- Illumina = short reads that are typically 100-300 bp long
 
**Q. how did the uncorrected (Minimap/miniasm) assembly compare to the corrected Canu assembly?**

Fairly similar genome assembly stats

Miniasm was much quicker than Canu - only hours, rather than days

Miniasm is uncorrected, canu is corrected - miniasm will have lots of indel errors (a common type of error in pacbio data), and may impact downstream analyses.
Eg, genes models will be wrong, due to a lot of frameshift errors. 



## Step 4: Comparison of your assemblies against the known reference sequence
**Q. how does each assembly compare against the reference?**

The pacbio genomes generally agree with the reference genome - there are a comple of small misassemblies, but most of the genome falls on the diagonal line, meaning the order of the sequences are the same.
 
particularly in the ref vs PB dot plot comparison, what sequence features are found and sequence ends, and why might they be there?

Should be able to see different types of repeats at the ends of the sequences- there is a guide in the manual on how to interpret these. Take home message - repeats break assemblies. 
 
**Q. are there base level characteristics found in one assembly but not the other? Is there anything specific to the Pacbio assembly but not Illumina assembly, and vice versa?**

You should be able to see an increase in the indels in the pacbio assemblies - this is a common feature and sequencing bias. This is not the case in the illumina assemblies.
 
**Q. what sequence features define the uncorrected Miniasm in particular?**

A lot more indels.






**Q. what are the main differences between the Pacbio and Illumina genome graphs?**

The graphs will look very different.
- the pacbio graph will be relatively simple, with some nice examples of different contigs joined together
- the illumina graph will look like a massive hairball mess. The key idea here is the it is in many more pieces, simply becasue the assembler could not resolve the repeats. This is a representation of that, where many repeats could be joined, but impossible to know the truth. 

**Q. what is the length of your new sequence?**

This will vary depending on what seqences they choose.

**Q. how did your new sequence compare to the reference? Was it syntenic?**

If they chose a sensible path throguh the graph, it should result in a bigger contig that remains syntenic with the reference. GenomeScope is very similar to ACT - it produces ribbons between two sequences, so look for ribbons along the sequence, including twisted ribbons suggesting inversions or misassemblies. 


