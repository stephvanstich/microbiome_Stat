


'''
install.packages("xlsx")
library("xlsx", lib.loc="/Library/Frameworks/R.framework/Versions/3.5/Resources/library")
'''

## Importing otu table in R studio

'''
otu_pups <- read.delim("otu_pups.txt", header=TRUE)
otu_mothers <- read.delim("otu_mothers.txt", header=TRUE)
'''

## General stats

'''
Otu_mothers_stat_treatment<-describeBy(otu_mothers,otu_mothers$Treatment,mat=TRUE)
write.table(Otu_mothers_stat_treatment,"Otu_mothers_stat.txt",sep="\t")
'''

'''
Otu_pups_stat_treatment<-describeBy(otu_pups,otu_pups$Treatment,mat=TRUE)
write.table(Otu_pups_stat_treatment,"Otu_pups_stat.txt",sep="\t")
'''

## pvalue

