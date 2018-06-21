setwd("E:/R (BA)")
library("dtw")
Ti9B <- read.csv("9BTest.csv")
Ti10A <- read.csv("10AonlyTest.csv")
Full10Ti <- read.csv("Full10Test.csv")

## TiD represents Ti normalised but multiplied by 10000 to easier visualise

alignmentOBE <- dtw(Ti10A$TiD, Ti9B$TiD, keep=TRUE,step=asymmetric, open.end=TRUE,open.begin=TRUE)
plot(alignmentOBE,type="two",off=4000);

## Triple plot to see both plots easier with the links between 

hq <- (0:200)/15
hq <- round(hq*1000)      #  indices in query for  pi/4 .. 7/4 pi
hw <- (alignmentOBE$index1 %in% hq)   # where are they on the w. curve?
hi <- (1:length(alignmentOBE$index1))[hw];   # get the indices of TRUE elems
dtwPlotThreeWay(alignmentOBE,match.indices=hi, ylab="9B\n", xlab="\n10A", margin = 3.75, inner.margin = 0.44, main = "Ti cps: 9B vs. 10A");

##Full 10 plot - working on linking then to floating below (section 11)

alignment2 <- dtw(Full10Ti$TiD, Ti9B$TiD, keep=TRUE,step=asymmetric, open.end=TRUE,open.begin=TRUE)
plot(alignment2,type="two",off=4000);


hq <- (0:200)/5
hq <- round(hq*1000)      #  indices in query for  pi/4 .. 7/4 pi
hw <- (alignment2$index1 %in% hq)   # where are they on the w. curve?
hi <- (1:length(alignment2$index1))[hw];   # get the indices of TRUE elems
dtwPlotThreeWay(alignment2,match.indices=hi)
