---
title: '卫生统计及SAS应用（二）数据集的管理'
date: 2020-12-05 02:50:39
tags: [SAS,biostat]
published: true
hideInList: false
feature: 
isTop: false
---
硕士课程《卫生统计及SAS应用》 

笔记工具
- Visual Studio Code
- 软件内下载Markdown插件 *Markdown TOC* 插入目录

 笔记内容包括6个部分：  
[x]  Lesson 1 数据集的建立  
[ ]  Lesson 2 数据集的管理  
[ ]  Lesson 3 SAS实用函数  
[ ]  Lesson 4 统计描述及分布类型  
[ ]  Lesson 5 正态性检验 & t检验  
[ ]  Lesson 6 卡方检验  


# 2. Lesson 2 数据集的管理
## 2.1. 纵向合并与横向合并

|纵向合并|横向合并|
|--|--|
|增加个案数|增加变量数|
|set|merge|
|纵向合并可能需要考虑个案的来源|横向合并可能需要考虑到：索引变量匹配、存在缺失变量时筛选变量齐全的个案|

- 纵向合并

```SAS
data s1;
input id gender age;
cards;
1 1 12
2 1 24
3 2 13
;
proc print;
run;
data s2;
input id gender age;
cards;
4 1 15
5 2 22
6 1 20
;
proc print;
run;
data s;
set s1(in= a1) s2(in=a2); /*set将s1与s2纵向合并，即增加个案数；数据集选项in=a1表示对于s1数据集的a1参数为1，同理s2数据集的a2参数为1，标记数据来源 */
by id; /*by表示排序依据，默认为升序，在变量前加descending表示降序*/
c1=a1; /*a1为临时变量，故将其赋值到c1中*/
c2=a2; 
proc print;
run;
```

s1

| Obs  | id   | gender | age  |
| ---- | ---- | ------ | ---- |
| 1    | 1    | 1      | 12   |
| 2    | 2    | 1      | 24   |
| 3    | 3    | 2      | 13   |

s2 

| Obs  | id   | gender | age  |
| ---- | ---- | ------ | ---- |
| 1    | 4    | 1      | 15   |
| 2    | 5    | 2      | 22   |
| 3    | 6    | 1      | 20   |

s

| Obs  | id   | gender | age  | c1   | c2   |
| ---- | ---- | ------ | ---- | ---- | ---- |
| 1    | 1    | 1      | 12   | 1    | 0    |
| 2    | 2    | 1      | 24   | 1    | 0    |
| 3    | 3    | 2      | 13   | 1    | 0    |
| 4    | 4    | 1      | 15   | 0    | 1    |
| 5    | 5    | 2      | 22   | 0    | 1    |
| 6    | 6    | 1      | 20   | 0    | 1    |

- 横向合并

```sas
data m1;
input id gender;
cards;
1 1
2 1
3 2
4 1
5 2
6 1
;
data m2;
input id age;
cards;
1 12
2 24
3 13
4 15
5 22
6 20
data m;
merge m1(in=a1) m2(in=a2);
by id; /*by表示索引变量为id*/
c1=a1; 
c2=a2;
if c1=1 and c2=1; /*if条件语句用于判断个案是否包含来自m1和m2的数据，从而筛选保留数据来源齐全的个案*/
proc print;
run;
```

m1 

| Obs  | id   | gender |
| ---- | ---- | ------ |
| 1    | 1    | 1      |
| 2    | 2    | 1      |
| 3    | 3    | 2      |
| 4    | 4    | 1      |
| 5    | 5    | 2      |
| 6    | 6    | 1      |

m2

| Obs  | id   | age  |
| ---- | ---- | ---- |
| 1    | 1    | 12   |
| 2    | 2    | 24   |
| 3    | 3    | 13   |
| 4    | 4    | 15   |
| 5    | 5    | 22   |
| 6    | 6    | 20   |

m

| Obs  | id   | gender | age  | c1   | c2   |
| ---- | ---- | ------ | ---- | ---- | ---- |
| 1    | 1    | 1      | 12   | 1    | 1    |
| 2    | 2    | 1      | 24   | 1    | 1    |
| 3    | 3    | 2      | 13   | 1    | 1    |
| 4    | 4    | 1      | 15   | 1    | 1    |
| 5    | 5    | 2      | 22   | 1    | 1    |
| 6    | 6    | 1      | 20   | 1    | 1    |

- 延伸：
1-  1if语句筛选后删除符合条件的个案

```sas
if <条件（表达式）> then delete;
```

- where 也可作为**数据集选项**

```sas
input m1(where= a1);
```


## 2.2. 拆分为若干个子集

### 2.2.1. 对观测个案的选择 if/where  firstobs/obs
- 条件语句：if语句、where语句或选项
- 

#### 2.2.1.1. 条件：if语句、where （选项 或者 语句）

```sas
/*if语句的写法*/
if 表达式 then 表达式;
else 表达式;
/*if语句的另一种写法*/
if 表达式;
/*where语句的写法*/
set cf0;
where gender="m" and age>40;
/*where选项*/
set cf0(where=(gender="m" and age>40));
```



```sas
data cf0;
input id gender$ age;
cards;
1 f 21
2 m 15
3 f 34
4 f 25
5 m 42
6 m 50
;
data cf1;
<条件语句>
proc print ;
run;

/*第一种：if语句*/
set cf0;
if gender="m" and age>40;
/*第二种：where语句*/
set cf0;
where gender="m" and age>40;
/*where选项*/
set cf0(where=(gender="m" and age>40));
```

#### 2.2.1.2. obs与firstobs（数据集选项）
通过设定所选个案的 ==起始点（firstobs=）== 和==结束点（obs=）==。

| obs             | firstobs        |
| --------------- | --------------- |
| 末位obs（包含） | 起始obs（包含） |

```sas
/*选择观测1-5*/
data pop;
do id=1 to 10;
output;
end;
;
data sam;
set pop(obs=5);
proc print;
run;
/*选择观测3-7*/
data pop;
do id=1 to 10;
output;
end;
;
data sam;
set pop(firstobs=3 obs=7);
proc print;
run;
/*选择观测6-10*/
data pop;
do id=1 to 10;
output;
end;
;
data sam;
set pop(firstobs=6);
proc print;
run;
```

### 2.2.2. 对变量选择 drop keep

#### 2.2.2.1. **drop 与keep**（数据集选项 或者 语句）

```sas
/*用作选项*/set 数据集(drop=变量);
/*用作语句*/drop 变量;

/*用作选项*/set 数据集(keep=变量);
/*用作语句*/keep 变量;
```



```sas
/*数据ht包含8个变量*/
data ht;
input id name$ gender age date1: yymmdd9. height1 date2: yymmdd9. height2;
format date1 date2 yymmdd10.;
cards;
1 LVJI 1 15 20110401 151 20120401 155
2 LXJU 2 16 20110401 153 20120402 155
3 LYJI 2 15 20110402 160 20120403 163
4 WAJI 2 17 20110401 149 20120401 154
5 JHYU 1 16 20110402 162 20120402 166
;
/*删除变量gender*/
/*方法一*/
data ht1;
set ht;
drop gender;
proc print;
/*方法二*/
data ht1x;
set ht(drop=gender);
proc print;
/*保留变量id与name*/
/*方法一*/
data ht2;
set ht;
proc print;
/*方法二*/
data ht2x;
set ht(keep=id name);
proc print;
run;
```


## 2.3. 排序proc sort

```sas
proc sort <out= 数据集名> <nodupkey> <nouniquekey>;
by <descending> 变量1 变量2 ...;
run;
```

排序处理在过程步（proc）。proc sort语句调用排序过程。

|选项|含义|
|-------|------|
|<**out=数据集**>|指定排序后的数据集名。因为排序后数据发生了变化，因此可指定该选项将排序后的数据存放到一个新的数据集中。如果不加该选项，排序后的数据集将覆盖原有数据集，这样你就找不回原有的未排序的数据了。|
| <**nodupkey**| 表示如果by语句指定的排序变量有重复值，则**删除重复值（保留唯一值）**。如按id排序，如果id有重复值，则只保留重复值中的第一个值，删除其它值。|
|<**nouniquekey**>|跟nodupkey正好相反，用于**删除唯一值（保留重复值）**如果by语句指定的排序变量都是唯一值，则将其删除。如按id排序，如果id没有有重复值，则全部删除。|

|搭配语句|含义|
|-------|------|
|**by...                                        < descending >**|指定排序的变量，可以指定多个。**选项< descending >**表示按降序排序，如果不加该选项，默认的是按升序排序。|


### 2.3.1. 排序

```sas
/*数据集ht包含5名学生的编号、姓名、性别、年龄、身高、日期*/
data ht;
input id name$ gender age date: yymmdd9. height;
format date yymmdd10.;
cards;
1	LVJI	1	15	20110401	151
2	LXJU	2	.	20110401	153
3	LYJI	2	15	20110402	160
4	WAJI	2	17	20110401	149
5	JHYU	1	16	20110402	162
;

proc sort out=ht_height;
by date descending age;
proc print data=ht_height;
run;

```


### 2.3.2. 查找重复值
```sas
data dup;
input name$ gender age;
cards;
Tony 1 31
Sam 1 30
Frank 2 29
Larry 1 29
Frank 2 29
Sam 2 30
;
```


#### 2.3.2.1. 仅保留不重复值 **nodupkey**
注意重复值中仅保留第一个个案

```sas
proc sort out=norep nodupkey;
by name;
proc print data=norep;
run;
```


#### 2.3.2.2. 仅保留重复值 **nouniquekey**

```sas
proc sort out=rep nouniquekey; 
by name;
proc print data=rep;
```


## 2.4. 转置 proc transpose

```sas
proc transpose <out=数据集> <name=第一列的变量名> <prefix=前缀名>;
by <descending> 变量1 <descending> 变量2 ……;
id 变量1 变量2 ……;
var 变量1 变量2 ……;
run;
```

proc transpose语句调用转置命令。

**注意选项name、prefix 和 id语句的用法的鉴别**



|选项|含义|
|-------|------|
|**<out=数据集>**|表示将转置后的数据输出到指定的数据集中；数据转置后，原来的变量名会变为转置后的变量值|
| **<name=变量名>** |为转置后的**第一列变量**起名，如果忽略该选项，默认名为_NAME_|
| **<prefix=前缀名>**| 表示为转置后的**第二列及以后列变量统一加前缀名**，前缀名后为1/2/3/4/... |

|搭配语句|含义|
|-------|------|
|**by语句**| 指定一个或多个变量，在每一变量内部进行转置，by语句指定的变量不进行转置。 |
|**id语句** |指定转置前数据集中的一个变量，将其值作为**转置后的第二列及以后列变量名**。省略该语句时，默认转置后的变量名依次为_NAME_、COL1、COL2、COL3、……。|

```sas
data vas;
input name$ id group vas1-vas3;  
cards;
LIXM 1 1 5 5 6
ZHMI 2 2 8 5 5
FEND 3 2 7 4 5
LIMZ 4 1 6 6 3
WAXF 5 2 6 7 5
DOCX 6 1 6 5 5
;
```

| Obs  | name | id   | group | vas1 | vas2 | vas3 |
| ---- | ---- | ---- | ----- | ---- | ---- | ---- |
| 1    | LIXM | 1    | 1     | 5    | 5    | 6    |
| 2    | ZHMI | 2    | 2     | 8    | 5    | 5    |
| 3    | FEND | 3    | 2     | 7    | 4    | 5    |
| 4    | LIMZ | 4    | 1     | 6    | 6    | 3    |
| 5    | WAXF | 5    | 2     | 6    | 7    | 5    |
| 6    | DOCX | 6    | 1     | 6    | 5    | 5    |


#### 2.4.0.3. 单纯转置
```sas
proc transpose;                
proc print;
run;
```
转置后
| Obs  | _NAME_ | COL1 | COL2 | COL3 | COL4 | COL5 | COL6 |
| ---- | ------ | ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | id     | 1    | 2    | 3    | 4    | 5    | 6    |
| 2    | group  | 1    | 2    | 2    | 1    | 2    | 1    |
| 3    | vas1   | 5    | 8    | 7    | 6    | 6    | 6    |
| 4    | vas2   | 5    | 5    | 4    | 6    | 7    | 5    |
| 5    | vas3   | 6    | 5    | 5    | 3    | 5    | 5    |

proc transpose**只对数值型变量转置**，不转置字符型变量；
原数据集中的变量名转置后成为变量值，命名为_NAME_；
原数据集中的每一个观测转置后都成为一个新变量，依次命名为COL1、COL2、……。



#### 2.4.0.4. 加上by语句，限定某一变量不转置
```sas
proc transpose; 
by  id;
proc print;
run;
```
结果为
| Obs  | id   | _NAME_ | COL1 |
| ---- | ---- | ------ | ---- |
| 1    | 1    | group  | 1    |
| 2    | 1    | vas1   | 5    |
| 3    | 1    | vas2   | 5    |
| 4    | 1    | vas3   | 6    |
| 5    | 2    | group  | 2    |
| 6    | 2    | vas1   | 8    |
| 7    | 2    | vas2   | 5    |
| 8    | 2    | vas3   | 5    |
| 9    | 3    | group  | 2    |
| 10   | 3    | vas1   | 7    |
| 11   | 3    | vas2   | 4    |
| 12   | 3    | vas3   | 5    |
| 13   | 4    | group  | 1    |
| 14   | 4    | vas1   | 6    |
| 15   | 4    | vas2   | 6    |
| 16   | 4    | vas3   | 3    |
| 17   | 5    | group  | 2    |
| 18   | 5    | vas1   | 6    |
| 19   | 5    | vas2   | 7    |
| 20   | 5    | vas3   | 5    |
| 21   | 6    | group  | 1    |
| 22   | 6    | vas1   | 6    |
| 23   | 6    | vas2   | 5    |
| 24   | 6    | vas3   | 5    |


#### 2.4.0.5. 修改列名
```sas
proc transpose data=vas name=vars; /*此处的name不是人为的变量名，而是sas本身对转置后第一列的变量名的固定称呼*/
id name; /*此处的id不是人为的变量名，而是sas本身对转置后第一行第2个及之后的值的固定称呼；此处的name是转置前的人为的变量name*/
proc print;
run;
```
结果为
| Obs  | vars  | LIXM | ZHMI | FEND | LIMZ | WAXF | DOCX |
| ---- | ----- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | id    | 1    | 2    | 3    | 4    | 5    | 6    |
| 2    | group | 1    | 2    | 2    | 1    | 2    | 1    |
| 3    | vas1  | 5    | 8    | 7    | 6    | 6    | 6    |
| 4    | vas2  | 5    | 5    | 4    | 6    | 7    | 5    |
| 5    | vas3  | 6    | 5    | 5    | 3    | 5    | 5    |



## 2.5. 对比多个数据集是否一致 proc compare

```sas
proc compare <base=数据集 compare=数据集> <nosummary> ;
by 变量1 变量2 ……;
```

proc compare语句调用数据比较过程。

|选项|含义|
|-------|------|
|base|指定比较的数据集|
|compare|指定被比较的数据集|
|nosummary|作用是不显示一些概括性的结果|

|搭配语句|含义|
|-------|------|
|by|指定的变量有点类似于**“索引”**的作用，通常指定id号。如果两个数据集的观测数不同，利用by语句可以保证它们比较的仍然是同一个id号，而不会出现错位比较的情况|

```sas
data a1;
input id gender age height weight;
cards;
1 2 24 165 55
2 2 24 160 48
3 2 28 160 60
4 2 27 155 48
5 2 25 165 59
;
data a2;
input id gender age height weight;
cards;
1 2 24 165 55
2 2 24 160 48
3 2 25 162 60
4 2 27 155 48
5 2 25 162 59
;
proc compare base=a1 compare=a2 nosummary;
run;
```

结果为：

```sas
                                           COMPARE 过程
                                      比较 WORK.A1 与 WORK.A2
                                          (METHOD=EXACT)

NOTE: 下列 2 个变量的值经比较不相等: age height


                                          变量的值比较结果

                    __________________________________________________________
                               ||       基准       比较
                          观测 ||        age        age       差异    差异(%)
                     ________  ||  _________  _________  _________  _________
                               ||
                            3  ||    28.0000    25.0000    -3.0000   -10.7143
                    __________________________________________________________


                    __________________________________________________________
                               ||       基准       比较
                          观测 ||     height     height       差异    差异(%)
                     ________  ||  _________  _________  _________  _________
                               ||
                            3  ||   160.0000   162.0000     2.0000     1.2500
                            5  ||   165.0000   162.0000    -3.0000    -1.8182
                    __________________________________________________________
```




## 2.6. 修饰

#### 2.6.0.6. 对变量名的注释

```sas
label 变量1= 标签1 变量2=标签2 ...;
```

#### 2.6.0.7. 对变量的值的注释

```sas
/*制定自定义格式*/
proc format;
invalue <$>格式名 变量或范围1=输入格式1 ...;
value <$>格式名 变量或范围1=输入格式1 ...;
--------
/*应用自定义的格式*/
format 变量 <$>格式名.; /*自定义的格式名需要在末尾加英文句号*/
```

| invalue                                                      | value                             |
| ------------------------------------------------------------ | --------------------------------- |
| 输入格式                                                     | 输出格式                          |
| 若invalue的目标数据是字符型，则无论数据本身是数值或是字符都作为字符输入 | 若源数据是字符，则需要在变量名前加$ |

```sas
proc format;
value first 1-2="male" 3="female";
value $second "a"-"g"="fair" "o","u"="other";
data test;
input x y$;
format x first.;
format y second.; /*两个变量分开两行设定格式*/
cards;
1 a
2 b
1 o
2 u
3 g
1 i
;
proc print;
run;
```

原本数据

| Obs  | x    | y    |
| ---- | ---- | ---- |
| 1    | 1    | a    |
| 2    | 2    | b    |
| 3    | 1    | o    |
| 4    | 2    | u    |
| 5    | 3    | g    |
| 6    | 1    | i    |

修饰结果

| Obs  | x      | y     |
| ---- | ------ | ----- |
| 1    | male   | fair  |
| 2    | male   | fair  |
| 3    | male   | other |
| 4    | male   | other |
| 5    | female | fair  |
| 6    | male   | i     |




## 2.7. 输出样式  proc print

```sas
proc print <data=> <label> <noobs> ;
by <descending> 变量1 <descending> 变量2 …;
var变量1 变量2 … < style >;
sum 变量1 变量2 … < style >;
```

proc print调用输出过程。

|选项|含义|
|-------|------|
|< data= >|指定要输出的数据集，如果不指定，默认为最近一次使用的数据集|
|< label >|要求显示用label语句指定的变量标签。前提在data步已有label语句。|
|< noobs >|要求不显示最左侧的obs列。|

|搭配语句|含义|
|-------|------|
|by|**分组**：将数据集按指定的变量分开显示。使用by语句之前，最好先用proc sort排一下序|
|var|**指定**需要**输出**的变量，如果不写，默认为全部输出|
|sum|给出指定数值变量的求和。这四个语句中的style选项均同proc print语句|

```sas
data baseline;
input id gender$ age height weight; 
label gender="性别"; 
cards;
1 female 36 160 60
2 female 43 168 56
3 male 51 171 73
4 female 60 160 50
5 male 66 172 55
;
proc print;
```
原本数据：

| Obs  | id   | gender | age  | height | weight |
| ---- | ---- | ------ | ---- | ------ | ------ |
| 1    | 1    | female | 36   | 160    | 60     |
| 2    | 2    | female | 43   | 168    | 56     |
| 3    | 3    | male   | 51   | 171    | 73     |
| 4    | 4    | female | 60   | 160    | 50     |
| 5    | 5    | male   | 66   | 172    | 55     |


输出修饰：
```sas
proc sort; 
by gender;
proc print data=baseline noobs label; 
by gender; sum height weight; 
run;
```

结果为：

性别=female

| id     | age  | height | weight |
| ------ | ---- | ------ | ------ |
| 1      | 36   | 160    | 60     |
| 2      | 43   | 168    | 56     |
| 4      | 60   | 160    | 50     |
| gender |      | 488    | 166    |

性别=male

| id     | age  | height | weight |
| ------ | ---- | ------ | ------ |
| 3      | 51   | 171    | 73     |
| 5      | 66   | 172    | 55     |
| gender |      | 343    | 128    |
|        |      | 831    | 294    |


