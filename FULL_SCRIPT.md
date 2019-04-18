


```
install.packages("xlsx")
library("xlsx", lib.loc="/Library/Frameworks/R.framework/Versions/3.5/Resources/library")
```

## Importing otu table in R studio

```
otu_pups <- read.delim("otu_pups.txt", header=TRUE)
otu_mothers <- read.delim("otu_mothers.txt", header=TRUE)
```

## General stats

```
Otu_mothers_stat_treatment<-describeBy(otu_mothers,otu_mothers$Treatment,mat=TRUE)
write.table(Otu_mothers_stat_treatment,"Otu_mothers_stat.txt",sep="\t")
```

```
Otu_pups_stat_treatment<-describeBy(otu_pups,otu_pups$Treatment,mat=TRUE)
write.table(Otu_pups_stat_treatment,"Otu_pups_stat.txt",sep="\t")
```

## Krukal-Wallis test

### subseting the data to test

```
otu_mothers_Ctrl_ADI1x<-subset(otu_mothers, Treatment!= "ADI2x")
otu_mothers_Ctrl_ADI2x<-subset(otu_mothers, Treatment!= "ADI1x")

otu_pups_Ctrl_ADI1x<-subset(otu_pups, Treatment!= "ADI2x")
otu_pups_Ctrl_ADI2x<-subset(otu_pups, Treatment!= "ADI1x")

```
```
KW_Verruco_test_mothers_ADI1x_Ctrl<- kruskal.test(Verrucomicrobia ~ Treatment, data = otu_mothers_Ctrl_ADI1x)
KW_Verruco_test_mothers_ADI2x_Ctrl<- kruskal.test(Verrucomicrobia ~ Treatment, data = otu_mothers_Ctrl_ADI2x)
KW_Verruco_test_pups_ADI1x_Ctrl<- kruskal.test(Verrucomicrobia ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Verruco_test_pups_ADI2x_Ctrl<- kruskal.test(Verrucomicrobia ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Tenericut_test_mothers_ADI1x_Ctrl<- kruskal.test(Tenericutes ~ Treatment, data = otu_mothers_Ctrl_ADI1x)
KW_Tenericut_test_mothers_ADI2x_Ctrl<- kruskal.test(Tenericutes ~ Treatment, data = otu_mothers_Ctrl_ADI2x)
KW_Tenericut_test_pups_ADI1x_Ctrl<- kruskal.test(Tenericutes ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Tenericut_test_pups_ADI2x_Ctrl<- kruskal.test(Tenericutes ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Unassigned_test_mothers_ADI1x_Ctrl<- kruskal.test(Unassigned ~ Treatment, data = otu_mothers_Ctrl_ADI1x)
KW_Unassigned_test_mothers_ADI2x_Ctrl<- kruskal.test(Unassigned ~ Treatment, data = otu_mothers_Ctrl_ADI2x)
KW_Unassigned_test_pups_ADI1x_Ctrl<- kruskal.test(Unassigned ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Unassigned_test_pups_ADI2x_Ctrl<- kruskal.test(Unassigned ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Bacteroidetes_test_mothers_ADI1x_Ctrl<- kruskal.test(Bacteroidetes ~ Treatment, data = otu_mothers_Ctrl_ADI1x)
KW_Bacteroidetes_test_mothers_ADI2x_Ctrl<- kruskal.test(Bacteroidetes ~ Treatment, data = otu_mothers_Ctrl_ADI2x)
KW_Bacteroidetes_test_pups_ADI1x_Ctrl<- kruskal.test(Bacteroidetes ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Bacteroidetes_test_pups_ADI2x_Ctrl<- kruskal.test(Bacteroidetes ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Firmicutes_test_mothers_ADI1x_Ctrl<- kruskal.test(Firmicutes ~ Treatment, data = otu_mothers_Ctrl_ADI1x)
KW_Firmicutes_test_mothers_ADI2x_Ctrl<- kruskal.test(Firmicutes ~ Treatment, data = otu_mothers_Ctrl_ADI2x)
KW_Firmicutes_test_pups_ADI1x_Ctrl<- kruskal.test(Firmicutes ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Firmicutes_test_pups_ADI2x_Ctrl<- kruskal.test(Firmicutes ~ Treatment, data = otu_pups_Ctrl_ADI2x)

KW_Proteobacteria_test_mothers_ADI1x_Ctrl<- kruskal.test(Proteobacteria ~ Treatment, data = otu_mothers_Ctrl_ADI1x)
KW_Proteobacteria_test_mothers_ADI2x_Ctrl<- kruskal.test(Proteobacteria ~ Treatment, data = otu_mothers_Ctrl_ADI2x)
KW_Proteobacteria_test_pups_ADI1x_Ctrl<- kruskal.test(Proteobacteria ~ Treatment, data = otu_pups_Ctrl_ADI1x)
KW_Proteobacteria_test_pups_ADI2x_Ctrl<- kruskal.test(Proteobacteria ~ Treatment, data = otu_pups_Ctrl_ADI2x)

```
```
KW_Test_results<- c(KW_Verruco_test_mothers_ADI1x_Ctrl$p.value,KW_Verruco_test_mothers_ADI2x_Ctrl$p.value,KW_Verruco_test_pups_ADI1x_Ctrl$p.value,KW_Verruco_test_pups_ADI2x_Ctrl$p.value,KW_Tenericut_test_mothers_ADI1x_Ctrl$p.value,KW_Tenericut_test_mothers_ADI1x_Ctrl$p.value,KW_Tenericut_test_pups_ADI1x_Ctrl$p.value,KW_Tenericut_test_pups_ADI2x_Ctrl$p.value,KW_Unassigned_test_mothers_ADI1x_Ctrl$p.value,KW_Unassigned_test_mothers_ADI2x_Ctrl$p.value,KW_Unassigned_test_pups_ADI1x_Ctrl$p.value,KW_Unassigned_test_pups_ADI2x_Ctrl$p.value,KW_Bacteroidetes_test_mothers_ADI1x_Ctrl$p.value,KW_Bacteroidetes_test_mothers_ADI2x_Ctrl$p.value,KW_Bacteroidetes_test_pups_ADI1x_Ctrl$p.value,KW_Bacteroidetes_test_pups_ADI2x_Ctrl$p.value,KW_Firmicutes_test_mothers_ADI1x_Ctrl$p.value,KW_Firmicutes_test_mothers_ADI2x_Ctrl$p.value,KW_Firmicutes_test_pups_ADI1x_Ctrl$p.value,KW_Firmicutes_test_pups_ADI2x_Ctrl$p.value,KW_Proteobacteria_test_mothers_ADI1x_Ctrl$p.value,KW_Proteobacteria_test_mothers_ADI2x_Ctrl$p.value,KW_Proteobacteria_test_pups_ADI1x_Ctrl$p.value, KW_Proteobacteria_test_pups_ADI2x_Ctrl$p.value)
```
```
KW_Test_sample <- c("KW_Verruco_test_mothers_ADI1x_Ctrl","KW_Verruco_test_mothers_ADI2x_Ctrl","KW_Verruco_test_pups_ADI1x_Ctrl","KW_Verruco_test_pups_ADI2x_Ctrl","KW_Tenericut_test_mothers_ADI1x_Ctrl","KW_Tenericut_test_mothers_ADI1x_Ctrl","KW_Tenericut_test_pups_ADI1x_Ctrl","KW_Tenericut_test_pups_ADI2x_Ctrl","KW_Unassigned_test_mothers_ADI1x_Ctrl","KW_Unassigned_test_mothers_ADI2x_Ctrl","KW_Unassigned_test_pups_ADI1x_Ctrl","KW_Unassigned_test_pups_ADI2x_Ctrl","KW_Bacteroidetes_test_mothers_ADI1x_Ctrl","KW_Bacteroidetes_test_mothers_ADI2x_Ctrl","KW_Bacteroidetes_test_pups_ADI1x_Ctrl","KW_Bacteroidetes_test_pups_ADI2x_Ctrl","KW_Firmicutes_test_mothers_ADI1x_Ctrl","KW_Firmicutes_test_mothers_ADI2x_Ctrl","KW_Firmicutes_test_pups_ADI1x_Ctrl","KW_Firmicutes_test_pups_ADI2x_Ctrl","KW_Proteobacteria_test_mothers_ADI1x_Ctrl","KW_Proteobacteria_test_mothers_ADI2x_Ctrl","KW_Proteobacteria_test_pups_ADI1x_Ctrl", "KW_Proteobacteria_test_pups_ADI2x_Ctrl")
```
```
KW_result<- matrix(KW_Test_results, nrow=24, ncol=1, byrow=TRUE,dimnames=list(KW_Test_sample)) 
```
