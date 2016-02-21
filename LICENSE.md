# Emmanuel Gonzalez Escobar Consulta y gráficas en R. 19/02/2016
library(foreign)
x<-read.dbf("C:\\Users\\SALA-C24\\Desktop\\SDEMT215.dbf",as.is = FALSE)
View(x,"ENOE 2T-2015")
table(x$CD_A)
table(x$CLASE1)
precod<-subset(x,(R_DEF=00) && (C_RES=1||C_RES=3) && (EDA>=15 && EDA<=98))
x$R_DEF1<-as.numeric(as.character(x$R_DEF))
x$C_RES1<-as.numeric(as.character(x$C_RES))
x$EDA1<-as.numeric(as.character(x$EDA))
precod<-subset(x,((R_DEF1==00) & (C_RES1==1|C_RES1==3) & 
                    (EDA1>=15 & EDA1<=98)),
               select = c(EDA1,SEX,HRSOCUP,CLASE2,CLASE1,CLASE3))
table(precod$EDA1)

table(precod$EDA1)
View(x)
sd1<-subset(x,CLASE2==1,select = c(EDA1,SEX,HRSOCUP,CLASE2,CLASE1,CLASE3,EDA5C,IMSSISSSTE))
frec<-table(sd1$IMSSISSSTE)
help("pie")
pie(frec)

pie(frec,labels = c("IMSS","ISSSTE","Otra","No recibe","no especificado"),main = "Institución de atención médica",col = c("cyan4","brown4","green","gray","yellow"))

frec1<- table(sd1$EDA5C)
barplot(frec1)
barplot(frec1,main = "Gráfica 1. Cinco grupos de edad",col =c("cyan4","brown4","green","gray","yellow"),names.arg = c("menor","14 a 24","25 a 44","45 a 64","65 y más","ne"),ylim = c(0,150000),ylab = "Edad",xlab = "Población")
help("barplot")
memory.size()##Para definir cuanta memoria va usar R
help("memory.size")
