


# R package to create manhattan plots using ggplot 

##Note: 
The package is currently under development.  Please raise issues for any bugs you identify.

## Installation

```
library(devtools)
install_github("veera-dr/ggman")
```

##Usage 

### Example data 

```
head(gwas)

  CHR     SNP BP      P     OR
1   1   rs1_0  1 0.2954 1.1050
2   1 rs1_0_M  2 0.9296 0.9922
3   1   rs1_1  3 0.8162 1.0160
4   1 rs1_1_M  4 0.6669 0.9719
5   1   rs1_2  5 0.4310 0.9426
6   1 rs1_2_M  6 0.3743 1.0580
>
```

### Create a basic Manhattan plot 

```
ggman(gwas, snp = "SNP", bp = "BP", chrom = "CHR", pvalue = "P")
```

![enter image description here](https://github.com/veera-dr/ggman/blob/master/data/manhattan.basic.png)

### Add labels to Manhattan plot 

```
p1 <- ggman(gwas, snp = "SNP", bp = "BP", chrom = "CHR", pvalue = "P")

gwas.sig <- gwas[-log10(gwas$P) > 8,]

ggmanLabel(p1,labelDfm = gwas.sig, snp = "SNP", label = "SNP")
```

![enter image description here](https://github.com/veera-dr/ggman/blob/master/data/manhattan.labelled.png)

### Highlight markers

```
ggmanHighlight(p1, highlight = highlights, colour="red")
```

![enter image description here](https://github.com/veera-dr/ggman/blob/master/data/Manhattan.highlights.png)

### Add multiple highlights

```
p1 <- ggman(gwas, snp = "SNP", bp = "BP", chrom = "CHR", pvalue = "P")

## add first highlights
p2 <- ggmanHighlight(p1, highlight = highlights, colour = "red")

## Lets create some more vectors of SNPs to highlight

highlights2 <- with(gwas, SNP[grep("rs06",SNP)])
highlights3 <- with(gwas, SNP[grep("rs0011",SNP)])

## add highlights

p3 <- ggmanHighlight(p2, highlight = highlights2, colour = "orange")
p4 <- ggmanHighlight(p3, highlight = highlights3, colour = "green4")
p4
```

![enter image description here](https://github.com/veera-dr/ggman/blob/master/data/multi%20highlights.png)

### Plot Odds Ratio instead of P values

```
ggman(gwas, snp = "SNP", bp = "BP", pvalue = "OR", chrom = "CHR", logTransform = FALSE, ymax = 3, ylab = "Odds Ratio")
```

![enter image description here](https://github.com/veera-dr/ggman/blob/master/data/or_plot.png)

### Inverted Manhattan Plot

```
ggmanInvert(gwas, snp = "SNP", bp = "BP", chrom = "CHR", pvalue = "P", effect = "OR", method = "or")
```

![enter image description here](https://github.com/veera-dr/ggman/blob/master/data/inverted.manhattan.png)