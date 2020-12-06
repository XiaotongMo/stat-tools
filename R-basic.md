## R basic
### 1 some reference materials

### 2 install
```r
install.packages("**")
library(**)
update.packages()
```
### 3 r basics
```r
v = c(1,4,4,3,2,2,3)#给v赋值，使其成为向量
v[c(2,3,4)]#取 向量v中第2，3，4个元素  中括号内是序号
v[2:4]#取 向量v中第2到4个元素
v[c(2,4,3)]#取 向量v中第2，4，3个元素
v[-2]#删除 向量v中第2个元素
v[-2:-4]#删除 向量v中第2到4个元素
v[v<3]#取 向量v中值小于3的所有元素
which(v==3)#取 向量v中值为3的元素的序号
whicn.max(v)#取 向量v中值最大的元素的序号
which.min(v)#同理，值最小
```

### 4 number
```r
set.seed(250)
a = runif(3, min=0, max=100)#均一分布取随机数
floor(a)#取 下整数
ceiling(a)#取 上整数
round(a,4)#取 a的值到小数点后4位
```

### data input
```r
data1=read.csv(file="~/documents/rugby.txt")#csv中将首行当作变量名
data2=read.table(file="~/documents/rugby.txt")#table中将首行当作变量值
data3=read.csv("http://www.macalester.edu/~kaplan/ISM/datasets/swim100m.csv")
attach(data3)#将首行作为变量名并赋值

set.seed(123)
x=rnorm(100,mean=100,sd=10)
set.seed(234)
y=rnorm(100,mean=100,sd=10)
hist(x,breaks=20,col="blue")#频率直方图 将x变量分20组画频率直方图，蓝色
plot(density(x))
plot(x)
boxplot(x,y)
boxplot(time~sex)
qqnorm(x)
qqline(x)
qqplot(x,y)
```
