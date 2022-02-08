
################
## Exercise 1 ##
################

### Map the RNA-seq data to the reference

```bash
# Got to the exercise directory
cd /home/manager/Task_1_SexualDevelopment

# Index the genome reference sequence
hisat2-build PbANKA_v3.fa PbANKA_v3_hisat2id


# Map the reads trying to used a bash script with iterations
chmod +x run_mapping.sh 
./run_mapping.sh 
```

################
## Exercise 2 ##
################

### Confirm the knockout in the mutant samples
```bash
# Index the fasta file so Artemis can view each chromosome separately
samtools faidx PbANKA_v3.fa

art -Dbam="Pb_MUT1_sorted.bam,Pb_MUT2_sorted.bam,Pb_MUT3_sorted.bam,Pb_WT1_sorted.bam,Pb_WT2_sorted.bam,Pb_WT3_sorted.bam" PbANKA_v3.fa +PbANKA_14_v3.embl &
```



################
## Exercise 3 ##
################

### Call differentially expressed genes

```bash
# Kallisto needs an index of the transcript sequences.



```

################
## Exercise 4 ##
################

### Perform a Gene Ontology enrichment analysis (we have provided an R script to help with this)

```R



```
