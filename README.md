
开发环境： Anaconda3(64-bit) Scrapy

IDE :PyCharm

参考网文:

http://studyai.site/2016/11/30/%E6%88%BF%E4%BB%B7%E9%A2%84%E6%B5%8B%EF%BC%881%EF%BC%89-%E6%90%9C%E6%88%BF%E7%BD%91%E6%95%B0%E6%8D%AE%E7%88%AC%E5%8F%96/

http://studyai.site/2016/11/30/%E6%88%BF%E4%BB%B7%E9%A2%84%E6%B5%8B%EF%BC%881%EF%BC%89-%E6%90%9C%E6%88%BF%E7%BD%91%E6%95%B0%E6%8D%AE%E7%88%AC%E5%8F%96/

http://studyai.site/2016/12/15/%E6%88%BF%E4%BB%B7%E9%A2%84%E6%B5%8B%EF%BC%883%EF%BC%89-%E6%95%B0%E6%8D%AE%E5%8F%AF%E8%A7%86%E5%8C%96/

代码执行:

crapy crawl degreeroom

R 展现:

library(mongolite)

con <- mongo("soufang",url="mongodb://192.168.59.105:27017/soufang")

mydata <- con$find()

barplot(table(x<-as.numeric(mydata$total)))

plot(x<-as.numeric(mydata$mian_ji),y<-as.numeric(mydata$total_price),xlab = "面积",ylab = "总价")

pie(table(mydata$hu_xin))

pie(table(mydata$xiao_qu))

pie(table(mydata$xue_xiao))

barplot(table(mydata$publish_date))

boxplot(as.numeric(mydata$total_price)/as.numeric(mydata$mian_ji),ylim=c(0.7,2.5))

con_gb_publis_time <- mongo("soufang_gb_publish_time", url = "mongodb://192.168.59.105:27017/soufang")

myGbData <- con_gb_publis_time$find(sort='{"publish_date":-1}')

barplot(height=as.numeric(myGbData$avg),table(myGbData$publish_date))

plot(x<-as.numeric(gsub('-','',myGbData$publish_date)),y<-as.numeric(myGbData$avg),type="o")
