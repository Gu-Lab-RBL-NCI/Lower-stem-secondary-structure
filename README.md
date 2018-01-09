# Lower-stem-secondary-structure
### Scripts used for the analysis of the pri-miRNA lower stem structure.

Genomic sequences of pri-miRNAs were obtained from [UCSC Genome Browser](https://genome.ucsc.edu/). Each pri-miRNA analyzed consists of the pre-miRNA and flanking sequences of 30 nt both sides. The secondary structure was obtained using RNAfold [(Gruber et al., 2008)](https://www.ncbi.nlm.nih.gov/pubmed/18424795), and the bracket-dot notation of the lower stem was analyzed using this R scripts. 

<img src="https://github.com/Gu-Lab-RBL-NCI/Lower-stem-secondary-structure/blob/master/drosha-cleavage.png" width="175" height="189">

In brief, we first tested whether a nucleotide in one position is paired with another on the other side of the pre-miRNA. Nucleotides that failed such a test were labeled as unpaired. Then, we aligned all pri-miRNA 5p sequences by the 5’ Drosha cleavage site (5’ end of pre-miRNA) and aligned all 3p sequences by the 3’ Drosha cleavage site (3’ end of pre-miRNA). The fraction of paired nucleotides was calculated for each position and was plotted against its relative distance to the Drosha cleavage site.

### Example 1
 #### **1. pri-miRNA secondary structure**

Secondary structure from pri-miRNA sequence reported in [miRBase 21](http://www.mirbase.org/) usually don't contain many upstream or downstream nucleotides from the Drosha cleavage sites.

```
>hsa-mir-9-1 MI0000466
CGGGGUUGGUUGUUAUCUUUGGUUAUCUAGCUGUAUGAGUGGUGUGGAGUCUUCAUAAAGCUAGAUAACCGAAAGUAAAAAUAACCCCA
.(((((((....((((.(((((((((((((((.((((((.(.(....).).)))))).))))))))))))))).))))...))))))).
```

Therefore, we obtained the secondary structure from pri-miRNA sequence obtained from longer genomic sequences on [UCSC Genome Browser](https://genome.ucsc.edu/)

```
......(((((...(.(((((((....((((.(((((((((((((((.((((((.(.(....).).)))))).))))))))))))))).))))...))))))).)...))).)).......
```

*Note that in most cases the secondary structure of the pri-miRNA sequence reported in miRBase21 is already included in the longer sequence. Most discrepancies might come from alternative foldings derived from providing extra-context to RNAfold.*

#### **2. Isolate the 5' and 3' lower stem segments**

Structure of the 5' lower stem

```
-30__________________________-1
......(((((...(.(((((((....(((
```

Structure of the 3' lower stem

```
+1_________________________+30
))...))))))).)...))).)).......
```

#### **3. Fraction of stem base-paired nucleotides**

For each position on the lower stem, we count the frequency of nucleotides on the 5' with `(` over the total, while on the 3' we count only the `)`.


### Example 2
#### **4. Detection of secondary stems**

It is not unfrequent to detect pri-miRNA where the lower stem, due to its less structured nature, presents secondary stems.

```
hsa-mir-152 5' lower stem
-30__________________________-1
..((((...)))..))((((..((.(((((
```

In such cases, our script excludes those positions from the being counted as "lower stem base-paired" nucleotides. To that aim our code replaces in the bracket-dot notation, the brackets on the secondary stem for `*`.

```
hsa-mir-152 5' lower stem
-30__________________________-1
..***....***..**((((..((.(((((
```


### Acknowledgements:

This code was written by Susanna Chen and supervised by Xavier Bofill-De Ros supervision.

### References:

[Gruber, A.R., Lorenz, R., Bernhart, S.H., Neuböck, R., and Hofacker, I.L. (2008). The Vienna RNA websuite. Nucleic Acids Res 36, W70-4.](https://www.ncbi.nlm.nih.gov/pubmed/18424795)
