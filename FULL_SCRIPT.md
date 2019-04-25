
# Welcome to General Stat for microbiome data

## installing and opening required packages

```
install.packages(“psych”,dependencies=TRUE)
install.packages(“ctv”)
install.views(“Psychometrics”)
```

```
library(psych)
library(ctv)

```

## Importing otu [table](otu_pups.txt) in R studio

```
otu_pups <- read.delim("otu_pups.txt", header=TRUE)
otu_mothers<- read.delim(Otu_mothers.txt, header=TRUE)
```
## Firmicutes/Bacteroidetes ratio colum

```
otu_pups$FirmicutesonBacteroidetesratio <- otu_pups$Firmicutes / otu_pups$Bacteroidetes
```

## General stats (mean, median, std...)

```
Otu_pups_stat_treatment<-describeBy(otu_pups,otu_pups$Treatment,mat=TRUE)
Final_Otu_pups_stat_treatment <- Otu_pups_stat_treatment[-c(1, 2, 3,4,5,6), ] 
write.table(Final_Otu_pups_stat_treatment,"Otu_pups_stat.txt",sep="\t")
```
Here is the final [table](Otu_pups_stat.txt) with your stats!

## Krukal-Wallis test

### subseting the data to test
(this will allow the comparison of two groups at a time)

```
otu_pups_Ctrl_ADI1x<-subset(otu_pups, Treatment!= "ADI2x")
otu_pups_Ctrl_ADI2x<-subset(otu_pups, Treatment!= "ADI1x")

```
Kruskal-Wallis test
```
KW_Verruco_test_pups_ADI1x_Ctrl<- kruskal.test(Verrucomicrobia ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Verruco_test_pups_ADI2x_Ctrl<- kruskal.test(Verrucomicrobia ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Tenericut_test_pups_ADI1x_Ctrl<- kruskal.test(Tenericutes ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Tenericut_test_pups_ADI2x_Ctrl<- kruskal.test(Tenericutes ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Unassigned_test_pups_ADI1x_Ctrl<- kruskal.test(Unassigned ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Unassigned_test_pups_ADI2x_Ctrl<- kruskal.test(Unassigned ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Bacteroidetes_test_pups_ADI1x_Ctrl<- kruskal.test(Bacteroidetes ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Bacteroidetes_test_pups_ADI2x_Ctrl<- kruskal.test(Bacteroidetes ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Firmicutes_test_pups_ADI1x_Ctrl<- kruskal.test(Firmicutes ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Firmicutes_test_pups_ADI2x_Ctrl<- kruskal.test(Firmicutes ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Proteobacteria_test_pups_ADI1x_Ctrl<- kruskal.test(Proteobacteria ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Proteobacteria_test_pups_ADI2x_Ctrl<- kruskal.test(Proteobacteria ~ Treatment, data = otu_pups_Ctrl_ADI2x)

```
Creating a table with the Kruskal-Wallis test result

```
KW_Test_results<- c(KW_Verruco_test_pups_ADI1x_Ctrl$p.value,KW_Verruco_test_pups_ADI2x_Ctrl$p.value,KW_Tenericut_test_pups_ADI1x_Ctrl$p.value,KW_Tenericut_test_pups_ADI2x_Ctrl$p.value,KW_Unassigned_test_pups_ADI1x_Ctrl$p.value,KW_Unassigned_test_pups_ADI2x_Ctrl$p.value,KW_Bacteroidetes_test_pups_ADI1x_Ctrl$p.value,KW_Bacteroidetes_test_pups_ADI2x_Ctrl$p.value,KW_Firmicutes_test_pups_ADI1x_Ctrl$p.value,KW_Firmicutes_test_pups_ADI2x_Ctrl$p.value,KW_Proteobacteria_test_pups_ADI1x_Ctrl$p.value,KW_Proteobacteria_test_pups_ADI2x_Ctrl$p.value)
```
```
KW_Test_sample <- c("KW_Verruco_test_pups_ADI1x_Ctrl","KW_Verruco_test_pups_ADI2x_Ctrl","KW_Tenericut_test_pups_ADI1x_Ctrl","KW_Tenericut_test_pups_ADI2x_Ctrl","KW_Unassigned_test_pups_ADI1x_Ctrl","KW_Unassigned_test_pups_ADI2x_Ctrl","KW_Bacteroidetes_test_pups_ADI1x_Ctrl","KW_Bacteroidetes_test_pups_ADI2x_Ctrl","KW_Firmicutes_test_pups_ADI1x_Ctrl","KW_Firmicutes_test_pups_ADI2x_Ctrl","KW_Proteobacteria_test_pups_ADI1x_Ctrl", "KW_Proteobacteria_test_pups_ADI2x_Ctrl")
```
```
KW_result<- data.frame(KW_Test_sample, KW_Test_results) 
KW_result$pvalueSignificance <-ifelse(KW_result$KW_Test_results>0.05, "ns",(ifelse(KW_result$KW_Test_results<0.001, "****",(ifelse(KW_result$KW_Test_results<0.005, "***", (ifelse(KW_result$KW_Test_results<0.01, "**", (ifelse(KW_result$KW_Test_results<0.05, "*", "-")))))))))
write.table(KW_result,"KW_result.txt",sep="\t")

```
Here is the final [table](KW_result.txt) with your test results!

## Correlation

Here, we want to correlate teh entire microbiome of two different groups of samples (mothers and  pups). 

BE CAREFUL: for the correlation, the taxa between your two datasets need to be IN THE SAME column/row ORDER. This is crucial for both the correlation and the statistical test!

We will reuse the data frame created before for the pups named - Otu_pups_stat_treatment- .
We will import and repeat the stat for the second group to correlate (here is the [mothers](otu_mothers.txt))
```
otu_mothers<- read.delim("otu_mothers.txt", header=TRUE, row.names = 1)
Otu_mothers_stat_treatment<-describeBy(otu_mothers,otu_mothers$Treatment,mat=TRUE)

```

Then, we will extract the mean of each species across samples.

```
Otu_pups_mean<- Otu_pups_stat_treatment[-c(1,2,3),c(2,5)]
Otu_mothers_mean<- Otu_mothers_stat_treatment[-c(1,2,3),c(2,5)]
```
We will then separate the file per treatment.
```
Otu_pups_Ctrl<- subset(Otu_pups_mean, Otu_pups_mean $group1 == "Ctrl")
Otu_pups_ADI1x<- subset(Otu_pups_mean, Otu_pups_mean $group1 == "ADI1x")
Otu_pups_ADI2x<- subset(Otu_pups_mean, Otu_pups_mean $group1 == "ADI2x")

Otu_mothers_Ctrl<- subset(Otu_mothers_mean, Otu_mothers_mean $group1 == "Ctrl")
Otu_mothers_ADI1x<- subset(Otu_mothers_mean, Otu_mothers_mean $group1 == "ADI1x")
Otu_mothers_ADI2x<- subset(Otu_mothers_mean, Otu_mothers_mean $group1 == "ADI2x")
```
Finally, we can make the correlation(spearman) and significance test(Spearman's rank correlation test).
```
Ctrl.corr.microbiome.mean <- cor(Otu_mothers_Ctrl$mean, Otu_pups_Ctrl$mean, method= "spearman")
ADI1x.corr.microbiome.mean <- cor(Otu_mothers_ADI1x$mean, Otu_pups_ADI1x$mean, method= "spearman")
ADI2x.corr.microbiome.mean <- cor(Otu_mothers_ADI2x$mean, Otu_pups_ADI2x$mean, method= "spearman")


pvalue.Ctrl<-cor.test(Otu_mothers_Ctrl$mean,Otu_pups_Ctrl$mean, method= "spearman")$p.value
pvalue.ADI1x<-cor.test(Otu_mothers_ADI1x$mean,Otu_pups_ADI1x$mean, method= "spearman")$p.value
pvalue.ADI2x<-cor.test(Otu_mothers_ADI2x$mean,Otu_pups_ADI2x$mean, method= "spearman")$p.value
```
This is the scripot to create a [table](Spearman.correlation.txt) with those values.
```
Spearman.correlation<- data.frame(c(Ctrl.corr.microbiome.mean, ADI1x.corr.microbiome.mean, ADI2x.corr.microbiome.mean), c(pvalue.Ctrl,pvalue.ADI1x,pvalue.ADI2x))
row.names(Spearman.correlation)<-c("Ctrl", "ADI1x", "ADI2x")
colnames(Spearman.correlation)<-c("Spearman", "pvalue")

write.table(Spearman.correlation, "Spearman.correlation.txt" ,sep="\t")

