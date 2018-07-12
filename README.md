# dashboard

data visulization 
----------------

```r
library(ggplot2)
library("showtext")
library(Cairo)
library("Rmisc")
library(grid)
```

```r
font.add("myfont","msyh.ttc")
bardata<-seq(from=0,to=270,length=1000)
rectdata<-seq(from=0,to=270,by=27)%>%c(360)
setwd("F:/微信公众号/公众号——数据小魔方/2017年4月/20170415")
```

```r
target<-1/3
assist<-target*270
```

### simple dashboard:<br>

```r
CairoPNG(file="dashboard.png",width=800,height=540)
showtext.begin()
ggplot(data=NULL)+
geom_rect(aes(xmin=rectdata[-12],xmax=rectdata[-1],ymin=5,ymax=10),fill="#F2F2F2",col="white")+
geom_bar(aes(x=bardata,y=5,col=bardata),stat="identity",fill=NA,size=2)+
geom_text(aes(x=rectdata[-12],y=-5,label=seq(0,100,by=10)),vjust=.5,hjust=.5,size=5,family="myfont",col="#0F1110")+
geom_segment(aes(x=assist,y=-50,xend=assist,yend=-10),arrow =arrow(length=unit(0.4,"cm")),size=1.2,col="red")+
geom_point(aes(x=assist,y=-50),shape=21,fill="white",col="black",size=7)+
annotate("text",x=315,y=-30,label=percent(target),size=12,hjust=.5,vjust=.5,family="myfont",col=ifelse(target<.5,"#F32626","#38E968"),fontface="plain")+ 
annotate("text",x=315,y=-15,label="指标1",size=15,hjust=.5,vjust=.5,family="myfont")+ 
ylim(-50,12)+
coord_polar(theta="x",start=179.85)+
scale_colour_gradient(low="#F32626",high="#38E968",guide=FALSE)+
theme_minimal()+
theme(
text=element_blank(),
line=element_blank(),
rect=element_blank()
)
showtext.end()
dev.off()
```

<div  align="center">    
<img src="https://github.com/ljtyduyu/dashboard/blob/master/Image/dashboard.png" width = "600" height = "405" alt="dashboard" align=center />
</div>

------------------------------------------------------------------------------

```r
set.seed(123)
target<-runif(5,0,1)
assist<-270*target
```

### syntaxic dashboard <br>
```r
CairoPNG(file="bigdashboard.png",width=1500,height=675)
showtext.begin()
grid.newpage()
pushViewport(viewport(layout=grid.layout(1,5)))
vplayout<-function(x,y){viewport(layout.pos.row =x,layout.pos.col=y)}
for(i in 1:5){
p<-ggplot(data=NULL)+
geom_rect(aes(xmin=rectdata[-12],xmax=rectdata[-1],ymin=5,ymax=12),fill="#F2F2F2",col="white")+
geom_bar(aes(x=bardata,y=5,col=bardata),stat="identity",fill=NA,size=2)+
geom_text(aes(x=rectdata[-12],y=-5,label=seq(0,100,by=10)),vjust=.5,hjust=.5,size=3.5,family="myfont",col="#0F1110")+
geom_segment(aes(x=assist[i],y=-50,xend=assist[i],yend=-10),arrow =arrow(length=unit(0.4,"cm")),size=1.2,col="red")+
geom_point(aes(x=assist[i],y=-50),shape=21,fill="white",col="black",size=7)+
annotate("text",x=315,y=-30,label=percent(target[i]),size=7.5,hjust=.5,vjust=.5,family="myfont",col=ifelse(target[i]<.5,"#F32626","#38E968"),fontface="plain")+ 
annotate("text",x=315,y=-15,label=paste0("指标",i),size=8.5,hjust=.5,vjust=.5,family="myfont")+ 
ylim(-50,12)+
coord_polar(theta="x",start=179.85)+
scale_colour_gradient(low="#F32626",high="#38E968",guide=FALSE)+
theme_minimal()+
theme(
text=element_blank(),
line=element_blank(),
rect=element_blank()
)
print(p,vp=vplayout(1,i))
}
showtext.end()
dev.off()
```

<div  align="center">    
<img src="https://github.com/ljtyduyu/dashboard/blob/master/Image/bigdashboard.png" width = "750" height = "337.5" alt="bigdashboard" align=center />
</div>



联系方式：
----------------------------------------------------
wechat：ljty1991  <br>
Mail:578708965@qq.com <br>
个人公众号：数据小魔方（datamofang） <br>
团队公众号：EasyCharts <br>
qq交流群：[魔方学院]553270834


备注信息：
----------------------------------------------------
<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">知识共享署名-非商业性使用 4.0 国际许可协议</a>进行许可。

