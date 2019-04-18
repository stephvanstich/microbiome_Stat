
Welcome to General Stat for microbiome data

## Importing otu table in R studio

```
otu_pups <- read.delim("otu_pups.txt", header=TRUE)
```

## General stats (mean, median, std...)

```
Otu_pups_stat_treatment<-describeBy(otu_pups,otu_pups$Treatment,mat=TRUE)
write.table(Otu_pups_stat_treatment,"Otu_pups_stat.txt",sep="\t")
```

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

