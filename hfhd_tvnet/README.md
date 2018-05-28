[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **hfhd_tvnet** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml


Name of Quantlet: hfhd_tvnet

Published in: 	  Bootstrapped Market Impact with Limit Order Books

Description:      'hfhd_tvnet code plots the time-varying full-sample 
		   connectedness network.'


Keywords:         limit order book, interconnection, network, plot

Author:           Shi Chen

Submitted:        2017/09/11

Output:           'The network graph of full-sample time-varying connectedness 
		   for the selected trading day.'

```

![Picture1](11.png)

![Picture2](12.png)

![Picture3](13.png)

![Picture4](14.png)

![Picture5](15.png)

![Picture6](16.png)

![Picture7](17.png)

### R Code
```r

rm(list=ls(all=T))
graphics.off()

setwd("")
load("mydate.RData")
load("GIR_30s.RData")#for fullconnectedness4.RData
#str(res1)


dem=conn1=NULL
for( ddd in 1: length(res1)){
  day1 = res1[[ddd]]
  mnum = matrix(0,63,63)
  num1=NULL
  for( i in 1:30){
    #i=1
    num1 = day1[,i,]^2
    mnum = mnum + num1
  }
  dem=t(mnum)/colSums(mnum)
  conn1[[ddd]] = t(dem)
}


nr=22#for example
graphics.off()
par(mfrow=c(3,3))

#for(nr in 18:21){
tc1=matrix(0,43,63)
for(nc in 1:63){
  
  for( ddd in 1: length(res1)){
    
    tc1[ddd,nc]=conn1[[ddd]][nr,nc]
  }
}


for(aa in 1:63){
  plot(tc1[,aa], ylim = c(0,0.5), type="l", ylab = aa)
}
#}


myfu <- function(nc){
tc1=matrix(0,43,63)
for(nc in 1:63){
  
  for( ddd in 1: length(res1)){
    
    tc1[ddd,nc]=conn1[[ddd]][nr,nc]
  }
}
return(t(tc1))
}

#For stock MSFT
nr=1; f1=22; f2=57#for p
par(mfrow=c(1,1))
barplot(myfu(nr)[c(f1,f2),], beside = T, 
        legend.text = c(myname[f1],myname[f2]), main=myname[nr])
axis(1,at=seq(1,125,by=3),labels=seq(1,42,by=1),cex.axis=1.5)
#axis(2, pos=0)

nr=2; f1=3; f2=4
nr=3; f1=2; f2=4
nr=4; f1=3; f2=28
nr=5; f1=6; f2=7
nr=6; f1=5; f2=7
nr=7; f1=6; f2=5
par(mfrow=c(1,1))
barplot(myfu(nr)[c(f1,f2),], beside = T, 
        legend.text = c(myname[f1],myname[f2]), main=myname[nr])
axis(1,at=seq(1,125,by=3),labels=seq(1,42,by=1),cex.axis=1.5)

```

automatically created on 2018-05-28