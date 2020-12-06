
a website for introduction:  
https://www.jianshu.com/p/q81RER

R在需求导向下学习更好。

---


# *Introduction to R Programming*
Author:Minghao Wu  
minghaowu_2015@163.com

Menu
---
<!-- TOC -->

- [*Introduction to R Programming*](#introduction-to-r-programming)
- [Lecture 1](#lecture-1)
    - [1 Some Reference Materials](#1-some-reference-materials)
    - [2 Install](#2-install)
    - [3 R Basics](#3-r-basics)
    - [4 Number](#4-number)
    - [5 Data Input](#5-data-input)
    - [6 Graph](#6-graph)
        - [histogram直方图](#histogram直方图)
        - [频率密度图](#频率密度图)
- [Lecture 2](#lecture-2)
    - [Understanding Dataset](#understanding-dataset)
        - [single value](#single-value)
        - [vector](#vector)
        - [matrix](#matrix)
        - [array](#array)
        - [data frame](#data-frame)
        - [list](#list)
    - [Graphs](#graphs)
        - [Graphical parameters](#graphical-parameters)

<!-- /TOC -->

# Lecture 1
## 1 Some Reference Materials

## 2 Install
    install.packages("**")  
    library( ** )  
    update.packages()
    
## 3 R Basics

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

## 4 Number
    set.seed(250)
    a = runif(3, min=0, max=100)#均一分布取随机数
    floor(a)#取 下整数
    ceiling(a)#取 上整数
    round(a,4)#取 a的值到小数点后4位


## 5 Data Input
    data1=read.csv(file="~/documents/rugby.txt")#csv中将首行当作变量名
    data2=read.table(file="~/documents/rugby.txt")#table中将首行当作变量值
    data3=read.csv("http://www.macalester.edu/~kaplan/ISM/datasets/swim100m.csv")
    attach(data3)#将首行作为变量名并赋值

## 6 Graph
    #生成随机数
    set.seed(123) 
    x=rnorm(100,mean=100,sd=10)
    set.seed(234)
    y=rnorm(100,mean=100,sd=10)

### histogram直方图
>hist(x,breaks=20,col="blue")#频率直方图 将x变量分20组画频率直方图，蓝色。还有其他参数可以设置  
    hist(x, breaks = "Sturges",		`#breaks即分界点数量`  
     freq = NULL, probability = !freq,  
     include.lowest = TRUE, right = TRUE,  
     density = NULL, angle = 45, col = NULL, border = NULL,	   #density即密度  
     main = paste("Histogram of" , xname),	`#main即图名`  
     xlim = range(breaks), ylim = NULL,		`#xlim即x轴范围`  
     xlab = xname, ylab,					`#xlab即x轴标签`  
     axes = TRUE, plot = TRUE, labels = FALSE,  
     nclass = NULL, warn.unused = TRUE, ...)

### 频率密度图
>plot(density(x))            `#density(x)是函数，表示计算x的密度`  
    plot(x)  
    boxplot(x,y)  `#箱图`  
    boxplot(time~sex) `#时间、性别分别为x、y轴`  
    qqnorm(x)  
    qqline(x)  
    qqplot(x,y)  

# Lecture 2
## Understanding Dataset
### single value
  * logical 
  * numeric
  * character
### vector
又可称为`一维数组`，使用函数是`组合函数c()`

  * logical  逻辑值  
    >a = c(True, True, False)
  * numeric  数字  
    >b = c(1,2,3,-4,5)
  * character  字符
    >c = c("One","Two","Three")
  * when multiple types are put into one vector, all of the data are changed into one type. For example,
    > c("a", 5, 1==2)  
    ```
	[1]a,5,"FALSE" #此时，"False"是一串字符，而不是逻辑值  
    ```
    This means all of the three data are changed as characters.
### matrix  
又可称为`两维数组`，使用函数是`矩阵函数matrix()`，其中元素是`同一种类型`的数据。nrow即行数，ncol即列数，byrow即是否按行填充。  

>x = matrix(1:20,nrow = 4, ncol = 5,byrow = TRUE) #按行填充1到20  
x  
```
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    2    3    4    5
[2,]    6    7    8    9   10
[3,]   11   12   13   14   15
[4,]   16   17   18   19   20
```

>x = matrix(1:20,nrow = 4, ncol = 5,byrow = FALSE)  #按列填充  
x
```
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    5    9   13   17
[2,]    2    6   10   14   18
[3,]    3    7   11   15   19
[4,]    4    8   12   16   20
```
> x[2,]  #输出`第2行`  
```
[1]  2  6 10 14 18
```  
> x[,2]  #输出`第2列`    
```
[1] 5 6 7 8  
```
> x[1,2]  #输出`第1行第2列`的元素  
```
[1] 5  
```
> x[1,c(2,3)]  #输出`第1行第1，3列`的元素  
```
[1] 5 9  
```
> x[1:3,4]  #输出`第1到3行第4列`的元素  
```
[1] 13 14 15
```
为行、列标签命名：
>rnames = c("1st","2nd","3rd","4th")  
cnames = c("a","b","c","d","e")  
rownames(x) = rnames  
colnames(x) = cnames  
x  
```
    a b  c  d  e
1st 1 5  9 13 17
2nd 2 6 10 14 18
3rd 3 7 11 15 19
4th 4 8 12 16 20
```
### array  
是`多维矩阵`，多于二维。使用函数`array()`  
>dim1 = c("d11","d12","d13")  
dim2 = c("d21","d22","d23","d24")  
dim3 = c("d31","d32")  
dim4 = c("d41","d42","d43","d44","d45")  
z = array(1:120, c(3,4,2,5),dimnames = list(dim1,dim2,dim3,dim4))  
z[,,1,1]  #此处表示`第3维中第一个`且`第4维第一个`的`第1维与第2维所有元素  
```
    d21 d22 d23 d24
d11   1   4   7  10
d12   2   5   8  11
d13   3   6   9  12
```

### data frame
是多维矩阵，使用函数`data.frame()`
>patientID = c(1,2,3,4)  
age = c(25,34,28,52)  
diabetes = c("t1","t2","t2","t1")  
status = c("poor","improved","excellent","poor")  
patientdata = data.frame(patientID,age,diabetes,status)  `#此处将这四个vector组合成一个data frame`  
patientdata 
```
  patientID age diabetes    status
1         1  25       t1      poor
2         2  34       t2  improved
3         3  28       t2 excellent
4         4  52       t1      poor
```
> patientdata[1,]  `#输出第1行`
```
  patientID age diabetes status
1         1  25       t1   poor
```
> patientdata[1]  `输出第1列，含列标签`
```
  patientID
1         1
2         2
3         3
4         4
```
> patientdata[,1]  `输出第1列，仅数据`
```
[1] 1 2 3 4
```
导入和清除data frame
>attach(x)  `#导入x`  
detach(x)  `#清除x`  

### list
较为复杂的数据类型，可以储存多种类型的数据，没有维度限制
>mylist = list(patientdata,x)  
mylist
```
[[1]]
  patientID age diabetes    status
1         1  25       t1      poor
2         2  34       t2  improved
3         3  28       t2 excellent
4         4  52       t1      poor

[[2]]
  dim1 dim2 dim3
1    1    a    5
2    2    b    6
3    3    c    7
4    4    d    8
```
>mylist[1] `#取mylist中的第一个“元素”，包括vector/matrix/array等,但所得不等于vector/matrix/array`  
```
[[1]]
  patientID age diabetes    status
1         1  25       t1      poor
2         2  34       t2  improved
3         3  28       t2 excellent
4         4  52       t1      poor
```
## Graphs
### Graphical parameters
常用于拼图的函数`par()`
>par(mfrow=c(2,2))
plot(rnorm(50),pch=17)
plot(rnorm(20),type="l",lty=5)
plot(rnorm(100),cex=0.5)
plot(rnorm(200),lwd=2)

输出4张图在2行2列
