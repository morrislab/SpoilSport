# SpoilSport
SpoilSport is a method to correct the inferred cellular proportion and number of mutations in a subclonal reconstruction for the effect of the winner's curse.
For a description of the method, see Supplement section XX in the PCAWG Heterogeneity paper (available on BioArxiv at:)
SpoilSport requires R, and the bbmle and emdbook packages.
SpoilSport has been tested on OS X Version 10.14 with the following package versions:
R: version 3.5.0
bbmle 1.0.20
emdbook 1.3.10

The source code is released under the GNU Public License v3.
SpoilSport requires the following input:
1) The inferred purity of the tumour sample
2) The inferred ploidy of the tumour sample
3) The mean read depth of the tumour sequencing
4) The typical minimum number of reads required to call a variant (typical value: 3)
5) A list of the cellular proportions for each identified cancerous population.  It's important to note that the cellular proportion is different from the cancer cell fraction.  If you have CCF values, multiply them by the purity before passing them in to SpoilSport.  This list should be in order from largest to smallest.

# Example usage:

```
source("spoilsport.R")
wcc(0.8,2.5,65,3,c(0.8,0.5,0.1))
```

The output is a dataframe with 4 columns and a number of rows equal to the number of cellular proportions input.
The columns are:
1) The subclonal number
2) The original cellular proportion of the population
3) The scale factor of the number of mutations (e.g. if this is 2, spoilsport thinks the true number of mutations is twice what are observed)
4) The corrected cellular proportion of the population.

The expected output from the sample command above is:
```
  sc_n  cp       sf         tp
1    1 0.8 1.000000 0.80000000
2    2 0.5 1.000041 0.49998226
3    3 0.1 3.752984 0.06616887
```

It should take only seconds to run.
