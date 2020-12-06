---
title: '卫生统计及SAS应用（一）数据集的建立'
date: 2020-12-05 02:19:04
tags: []
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
[ ]  Lesson 5 正态形检验 & t检验  
[ ]  Lesson 6 卡方检验  

<!-- TOC -->

- [1. Lesson 1 数据集的建立](#1-lesson-1-数据集的建立)
  - [1.1. 简介](#11-简介)
  - [1.2. 数据集的基本输入方式（数据步）](#12-数据集的基本输入方式数据步)
  - [1.3. 数据变量类型](#13-数据变量类型)
    - [1.3.1. 字符型character](#131-字符型character)
    - [1.3.2. 数值型numeric](#132-数值型numeric)
  - [1.4. 变量输入和输出格式](#14-变量输入和输出格式)
    - [1.4.1. 字符型](#141-字符型)
    - [1.4.2. 数值型](#142-数值型)
    - [1.4.3. 日期型](#143-日期型)
    - [1.4.4. 自定义输入和输出格式：proc  format](#144-自定义输入和输出格式proc--format)
  - [1.5. 特殊变量的输入](#15-特殊变量的输入)
    - [1.5.1. 给定宽度，是否取空格为字符](#151-给定宽度是否取空格为字符)
    - [1.5.2. 数据集中有==缺失值==](#152-数据集中有缺失值)
    - [1.5.3. 有规律的变量](#153-有规律的变量)
    - [1.5.4. 是否换行输入](#154-是否换行输入)
      - [1.5.4.1. 输入重复测量数据](#1541-输入重复测量数据)
    - [1.5.5. 产生新变量](#155-产生新变量)
      - [1.5.5.1. 宽度限制](#1551-宽度限制)
  - [1.6. 数据集的导入和导出](#16-数据集的导入和导出)
  - [1.7. 建立和调用永久性数据集](#17-建立和调用永久性数据集)
    - [1.7.1. 建立永久性数据集](#171-建立永久性数据集)
    - [1.7.2. 调用永久性数据集](#172-调用永久性数据集)

<!-- /TOC -->


<a id="markdown-1-lesson-1-数据集的建立" name="1-lesson-1-数据集的建立"></a>
# 1. Lesson 1 数据集的建立
<a id="markdown-11-简介" name="11-简介"></a>
## 1.1. 简介
**程序的基本组成**

1 数据步

```SAS
data 数据集名; /*新建数据集，导入储存数据*/
```
2 过程步

```SAS
proc 操作 <options>; /*处理数据*/
run;/*结束语*/
```

<a id="markdown-12-数据集的基本输入方式数据步" name="12-数据集的基本输入方式数据步"></a>
## 1.2. 数据集的基本输入方式（数据步）

1 在SAS直接输入

```sas
data ma.fsh;                     /*数据集起名为ma.fsh，ma是逻辑库名，fsh是ma中的某一数据集名*/
input age weight height;         /*数据集中输入3个变量，命名为age、weight、height*/
cards;                           /*标志着后面就是数据输入；或者用 dataline */
26 62 171
28 58 166
;
```

**注意事项**

> 任何语句的结束需要加一个分号“;”，必须是英文状态下的分号。
> 数据输入后，分号要另起一行，不能紧接在数据后输入。
> 输入的字母不区分大小写
> 输入格式不要求必须左对齐或右对齐
> 初学者尽量不要把多个语句放在一行。如：
>     Input id age;  cards; 1 23; 初学者最好不要用这种输入方式
> SAS数据集名或变量名太长时，可加下划线，如:
>      Data drinking_in_beijing;       Input test_score;

2 引用外部数据

文件--导入数据


<a id="markdown-13-数据变量类型" name="13-数据变量类型"></a>
## 1.3. 数据变量类型

SAS中的变量只有两种类型：字符型（character）和数值型（numeric）。

日期是被看作是数值型，所有日期型变量被作为是输入日期与1960年1月1日之差。如1980-1-1， SAS会认为这个值是7305。

不同类型的变量在input语句输入时需要指定相应的格式


<a id="markdown-131-字符型character" name="131-字符型character"></a>
### 1.3.1. 字符型character

```sas
data fh;
input gender$;    
/*$表示gender变量是个字符型,字符型变量一定要在变量后面加一个$符号，变量和$之间加不加空格均可。*/
cards;
female
male
;
```


<a id="markdown-132-数值型numeric" name="132-数值型numeric"></a>
### 1.3.2. 数值型numeric

包括数值与日期

- 数值

如果你想让SAS有选择地读取你的数值，可以在变量后加上w.d的格式。其中，w表示数值的位数（包括小数点），如2.3的位数是3；d表示数值的小数点位数。

```sas
data fh;
input x 4.2;      /*变量后的4.2表示变量x的宽度共4位，其中小数点2位*/
cards;
12
2.1
15.6
23.46
;
proc print;
run;
```

- 日期

| SAS日期格式 | 举例      | SAS日期格式 | 举例       |
| ----------- | --------- | ----------- | ---------- |
| DDMMYY6.    | 280713    | DDMMYY8.    | 28/07/13   |
| MMDDYY6.    | 072813    | MMDDYY8.    | 07/28/13   |
| YYMMDD6.    | 130728    | YYMMDD8.    | 13/07/28   |
| DDMMYY8.    | 28072013  | DDMMYY10.   | 28/07/2013 |
| MMDDYY8.    | 07282013  | MMDDYY10.   | 07/28/2013 |
| YYMMDD8.    | 20130728  | YYMMDD10.   | 2013/07/28 |
| DATE7.      | 28JUL13   | MONYY5.     | JUL13      |
| DATE9.      | 28JUL2013 | MONYY7.     | JUL2013    |



<a id="markdown-14-变量输入和输出格式" name="14-变量输入和输出格式"></a>
## 1.4. 变量输入和输出格式

**输入格式是给SAS读的，输出是给使用者读的。**

| 变量类型       | 输入格式 | 输出格式 |
| -------------- | -------- | -------- |
| 数值型非日期型 |          |          |
| 数值型日期型   |          |          |
| 字符型         |          |          |




- 1 输入格式

见上述。使用**input**或**input搭配informat**。不想改变输入值，不要在输入格式中定义宽度。

```sas
data test;
/*使用input*/
input date yymmdd10.;
/*使用input+informat*/
input date;
informat date yymmdd10.;
```
- 2 输出格式

大致同输入格式。在data步，在input语句与cards之间使用**format**。

```sas
data test;
input x;
format yymmdd10.;
cards;
20100101
20111103
;
```


<a id="markdown-141-字符型" name="141-字符型"></a>
### 1.4.1. 字符型

完整的格式应该是$ < w. >。

必须在变量名后加"$"；w表示字节数（1个中文占2个字节）。

| 输入格式                           | 输出格式       |
| ---------------------------------- | -------------- |
| $ < w. >                           | $ < w. >       |
| 默认只读取前8位，超出8位必加上“w.” | 不限制输出位数 |

```sas
data city;
input city$ code$;
format city $4. code $2.; /*city的输出格式为字符型且字节数为4；code的输出格式为字符型且字节数为2*/
cards;
北京市 110000
天津市 120000
上海市 310000
;
proc print;
run;
```
结果为：

| Obs  | city | code |
| ---- | ---- | ---- |
| 1    | 北京 | 11   |
| 2    | 天津 | 12   |
| 3    | 上海 | 31   |


<a id="markdown-142-数值型" name="142-数值型"></a>
### 1.4.2. 数值型

| 输入格式 | 输出格式   |含义|
| -------- | ---------- |---|
| w.d      | w.d        |总位数w，其中小数点后位数d（小数点算1bit）|
|          | commaw.d   |+ 整数部分加逗号（逗号算1bit）|
|          | percentw.d |+ 百分数形式（%算3bit）|

**w.d**的理解：

- w是指数值从左到右读取的位数，**包括小数点、逗号**！
- d是指小数点后的位数！
- **整数若不带有小数点，则在读取时被认为小数部分。**

**comma**w.d 可将数值的整数部分自右向左每三位用逗号隔开，当数值位数较多时，这是比较标准的表示方式。

```sas
data wt;
input num cost;
format num 5.2 cost comma12.1; /*num共5位其中2位小数；cost共12位其中1位小数，且用逗号每3位分隔*/
cards;
50 10205600
45 9580000
;
proc print;
run;
```

例如，输出格式为**comma7.1**时。

| 输入 | 输出  |
| ---- | ----- |
| 111  | 111.0 |
|1111|1,111.0|
|11111|11111.0|
|111111|111111|
|1111111|1111111|
|11111111|1.111E7|

<a id="markdown-143-日期型" name="143-日期型"></a>
### 1.4.3. 日期型

日期有两种类型：数字、日期格式。

| 输入格式 | 输出格式 |
| -------- | -------- |
| 日期格式 | 日期格式 |
|          | 分隔符   |

日期型变量输入格式与输出格式大致相同，但**输出格式允许**在宽度值前加一个字母，表示日期的分隔符号。**但不能用于date7.或date9.等格式。**

**日期格式**

| 日期格式  | 举例      | 日期格式  | 举例       |
| -------- | --------- | --------- | ---------- |
| DDMMYY6. | 280713    | DDMMYY8.  | 28/07/13   |
| MMDDYY6. | 072813    | MMDDYY8.  | 07/28/13   |
| YYMMDD6. | 130728    | YYMMDD8.  | 13/07/28   |
| DDMMYY8. | 28072013  | DDMMYY10. | 28/07/2013 |
| MMDDYY8. | 07282013  | MMDDYY10. | 07/28/2013 |
| YYMMDD8. | 20130728  | YYMMDD10. | 2013/07/28 |
| **DATE7.** | 28JUL13   | **MONYY5.** | JUL13      |
| **DATE9.** | 28JUL2013 | **MONYY7.** | JUL2013    |

**分隔符号**

| 字母 | 含义 |日期输出格式 | 结果显示 |
| ---- | ---- |------------ | -------- |
|s|slash(/)|YYMMDDs8.    | 13/07/28 |
|d|dash(-)|YYMMDDd8.    | 13-07-28 |
|p|point(.)| YYMMDDp8.    | 13.07.28 |
|c|colon(:)|YYMMDDc8.    | 13:07:28 |
|b|blank( )|YYMMDDb8.    | 13 07 28 |
|n|nothing()|YYMMDDn8.    | 20130728 |


<a id="markdown-144-自定义输入和输出格式proc--format" name="144-自定义输入和输出格式proc--format"></a>
### 1.4.4. 自定义输入和输出格式：proc  format

- 自定义值的内容的输入与输出格式 **invalue 与 value**

invalue 输入看“**原值**”

value 输出看“**新值**”

```sas
proc format;
invalue <$> variable_name range/value = self-defined value.../*自定义输入格式*/
value <$> variable_name range/value = self-defined value.../*自定义输出格式*/
picture module_name < range >;
```

|  | 原值   | 新值   | 语句 |
| --------- | ------ | ------ | ---- |
| 输入      | 字符型 | **数值型** |invalue grade "a"-"g"=1 other=2|
| 输入      | 字符型 | **字符型** |invalue **$grade** "a"-"g"="fair"  "o","u"="other"|
| 输入      | 数值型 | **数值型** |invalue lxfmt 1-4=_same_ 99=.;      1-4则保持不变，99则改为缺失值|
| 输入      | 数值型 | **字符型** |invalue **$gender** 1="male" 2="female" |

|  | 原值   | 新值   | 语句 |
| --------- | ------ | ------ | ---- |
| 输出      | **字符型** | 字符型|value **$grade** "a"-"g"="fair"      |
|输出|**字符型**|数值型|value **$grade** "a"-"g"="fair"  "o","u"="other"|
|输出|**数值型**|字符型||
|输出|**数值型**|数值型||

- 自定义值的形式的格式 **picture**

```sas
picture 格式名 原值=新格式(prefix="￥");/*prefix表示加前缀*/

proc format;
/*对所有数值，定义格式要求：前缀为￥，每满三位数加逗号“,”*/
picture gs1 low-high="0,000,000"(prefix="￥");
/**/
picture gs2 low-high="09.99%";
run;
data profit;
input profit prop;
format profit gs1. prop gs2.;
cards;
298000 16.72
458992 21.30
;
proc print;
run;

```

结果为：

| Obs  | profit    | prop   |
| ---- | --------- | ------ |
| 1    | ￥298,000 | 16.72% |
| 2    | ￥458,992 | 21.30% |

说明一下，"09.99%"的理解是：

1. 先对齐小数点；
2. 再根据小数点前多少位数就保留多少位数
3. 整数部分从个位开始，小数点前多少位就保留多少位数
4. 倘若不只有一个小数点，那么先对齐最末尾的小数点；
5. 末尾加上符号（**不是把原值改为等值的百分数形式！！无论是什么符号都可以！！**）


<a id="markdown-15-特殊变量的输入" name="15-特殊变量的输入"></a>
## 1.5. 特殊变量的输入

<a id="markdown-151-给定宽度是否取空格为字符" name="151-给定宽度是否取空格为字符"></a>
### 1.5.1. 给定宽度，是否取空格为字符

```sas
data test;
input id$8. gender$1. city$7.;
cards;
12345678 m beijing
;
proc print;
run;
```

所得结果为：

|obs| id       | gender | city    |
|---| -------- | ------ | ------- |
|1| 12345678 |        | m beiji |

原因是**指定宽度后，空格也成为字符的一部分**。修改方式如下：

- 需要指定多个变量的宽度
  - 改变输入格式中的宽度
    ```sas
    input id$9. gender$2. city$7.
    ```

  - 改变变量的读取位置（+1表示往后1个字符读取）

    ```sas
    input id$8.+1 gender$1.+1 city$7.;
    ```

  - 利用**冒号（:）**来正确读取（冒号表示**识别前后的空格是分隔符号**，不作为字符内容；否则空格也是字符的一部分）

    冒号（:）的作用是告诉SAS，如果要读取下一个数据，需要满足下面任一条件：
    - 遇到空格；
    - 指定的变量宽度已满；
    - 数据行结束。

    ```sas
    input id:$8. gender:$1. city:$7.;
    ```

- 数据集中有空格

  **&**读取 **空格**作为字符的一部分，而**<u>多个空格则作为分隔符</u>**

  （变量名后加 “**&**”。同时cards后的不同变量之间需要**至少2个**空格。）

  ```sas
  data fh;
  input name&:$50. city&:$50.; /*变量名后加 $ */
  cards;
  Peter Parker  山东省 蓬莱市  /*两个变量之间至少2个空格*/
  Ross Geller  山东省 青岛市 市南区  
  ;
  proc print;
  run;
  ```


<a id="markdown-152-数据集中有缺失值" name="152-数据集中有缺失值"></a>
### 1.5.2. 数据集中有==缺失值==

  缺失值用 “**.** ”表示。

  ```sas
  data fh;
  input id day: yymmdd8. city:$20.; 
  format day yymmddp10.;  
  cards;
  37 980515 .
  . 120607 shanghai
  39 . nanjing
  ;
  proc print;
  run;
  ```

  结果为
|obs|id|day|city|
|--|--|--|--|
|1|37|1998.05.15||
|2|.|2012.06.07|shanghai|
|3|39|.|nanjing|


<a id="markdown-153-有规律的变量" name="153-有规律的变量"></a>
### 1.5.3. 有规律的变量

  用do循环输入数据

  ```sas
  data test;
  do count=3 to 9 by 2；
  <语句>
  end；
  run；
  ```

  其中的语句若使用input，则必须加上output。

  例如1-12月是连续加1的规律。

  未使用do循环时：

  ```sas
  data test;
  input count time;
  cards;
  1 23
  2 29
  3 49
  4 64
  5 87
  6 96
  ;
  proc print;
  run;
  ```

  由于count具有加1的规律，使用do循环后：

  ```sas
  data test;
  do count=1 to 6; /*使用do循环输入count的值*/
  input time;
  output; /*必须*/
  end; /*必须*/
  cards; /*省略count的输入*/
  23
  29
  49
  64
  87
  96
  ;
  proc print;
  run;
  ```


<a id="markdown-154-是否换行输入" name="154-是否换行输入"></a>
### 1.5.4. 是否换行输入

  用@符号

  - @@与@符号的区别：

    - @@强制保持当前记录，不管data步中有没有其他语句
    - @如果data步中没有其他语句，就hold不住当前记录，仍然转到下一记录，如果有第二个input语句，就可以hold住当前记录，等待第二个input顺序读取

  - ==@@== 强行保持当前行。所输入数据均作为**某一变量**的值

    - CASE 1——录入单一变量

    ```sas
    data test;
    input weigh@@;
    cards;
    1 2 3 
    4 5 6
    ;
    proc print;
    run;
    ```

    ​	结果为：

    | Obs  | weigh |
    | ---- | ----- |
    | 1    | 1     |
    | 2    | 2     |
    | 3    | 3     |
    | 4    | 4     |
    | 5    | 5     |
    | 6    | 6     |

    

    - CASE 2——输入列联表

    | |吸烟（1）|不吸烟（2）|
    | ---- | ---- | ---- |
    | 男（1）     |100      |150      |
    |女（2）|10|140|

    ```sas
    /*常规输入*/
    data a;
    input gender smoking;
    cards; /*每一行表示一个个案的资料*/
    1 2
    2 1
    1 1
    1 1
    ...
    ;
    proc print;
    run;
    /*用@@输入*/
    data a;
    do gender= 1 to 2;
    do smoking= 1 to 2; /*先进行小循环，后进行大循环*/
    input x@@; /*x为频数*/
    output;
    end;
    end;
    cards;
    100 150
    10 140
    ;
    run;
    ```

    ​	结果：

    | Obs  | gender | smoking |
    | ---- | ------ | ------- |
    | 1    | 1      | 2       |
    | 2    | 2      | 1       |
    | 3    | 1      | 1       |
    | 4    | 1      | 1       |

    

  - **@** 保持当前行

    ```SAS
    data test;
    /*<几种不同的input方式>;*/
    cards;
    1 2 3 4
    5 6 7 8
    ;
    proc print;
    run;
    
    /*1*/
    input x@@;
    /*2*/
    input x;
    input y;
    /*3*/
    input x@;
    input y;
    /*4*/
    input x y;
    ```

    结果分别为：

    <1>通过@@强制将所有数据录入为值

    | Obs  | x    |
    | ---- | ---- |
    | 1    | 1    |
    | 2    | 2    |
    | 3    | 3    |
    | 4    | 4    |
    | 5    | 5    |
    | 6    | 6    |
    | 7    | 7    |
    | 8    | 8    |

     <2>x与y分别在两行，各取一个值

    ```sas
    /*2*/
    input x;
    input y;
    ```

    | Obs  | x    | y    |
    | ---- | ---- | ---- |
    | 1    | 1    | 5    |

     <3>通过@保留原排列并认为第一、二列分别是x、y变量

    ```sas
    /*3*/
    input x@;
    input y;
    ```

    | Obs  | x    | y    |
    | ---- | ---- | ---- |
    | 1    | 1    | 2    |
    | 2    | 5    | 6    |

     <4>第一、二列分别是x、y变量

    ```sas
    /*4*/
    input x y;
    ```

    | Obs  | x    | y    |
    | ---- | ---- | ---- |
    | 1    | 1    | 2    |
    | 2    | 5    | 6    |


<a id="markdown-1541-输入重复测量数据" name="1541-输入重复测量数据"></a>
#### 1.5.4.1. 输入重复测量数据

    ```sas
    /*常规输入*/
    data test1;
    input id time score;
    cards;
    1 1 86
    1 2 89
    1 3 90
    2 1 89
    2 2 87
    2 3 91
    ...
    ;
    proc print;
    run;
    /*利用@符号输入*/
    data test2;
    input id@;
    do time= 1 to 3; /*对于每个id，都有time从1到3取值*/
    input score@@; /*对于每个id与time的组合，都有一个score相对应*/
    output;
    end;
    cards;
    1 86 89 90
    2 89 87 91
    ...
    ;
    proc print;
    run;
    ```




<a id="markdown-155-产生新变量" name="155-产生新变量"></a>
### 1.5.5. 产生新变量
```sas
新变量 = 表达式 或者 函数
```
|算术运算符|比较运算符|逻辑运算符|
|--|--|--|
|+ （加）|=（等于）、 ^=（不等于）|&或and（表示2个表达式同时成立）|
|- （减）|>（大于）、 <（小于）| \|或or（表示2个表达式任一成立） |
|* （乘）|>=（大于等于）、 <=（小于等于）||
|/ （除）| in(范围)（属于其中）grade in(2,4,6)表示只要是grade为2、4、6中的其中一个就算符合条件 ||
|**          （幂次方）|dept not in(“A”, “B”)表示只要dept不是“A”或“B”就算成立||


<a id="markdown-1551-宽度限制" name="1551-宽度限制"></a>
#### 1.5.5.1. 宽度限制

产生新变量前，对其进行宽度限定，使用length

```sas
data bonus;
input id g1 g2 bonus;
length g $6.;  /*定义字符变量g的长度为6，若无该语句，则宽度受第一个值的影响*/
if g1>=70 and g2>=70 then g="合格";
else g="不合格";
if g="合格" then bonus=bonus*1;
else bonus=bonus*0.5;
cards;
1 67 74 10000
2 80 85 11000
3 89 87 11000
4 78 69 10000
;
proc print;
run;
```

无length语句：

| Obs  | id   | g1   | g2   | bonus | g    |
| ---- | ---- | ---- | ---- | ----- | ---- |
| 1    | 1    | 67   | 74   | 5000  | 不合 |
| 2    | 2    | 80   | 85   | 11000 | 合格 |
| 3    | 3    | 89   | 87   | 11000 | 合格 |
| 4    | 4    | 78   | 69   | 5000  | 不合 |

有length语句：

| Obs  | id   | g1   | g2   | bonus | g      |
| ---- | ---- | ---- | ---- | ----- | ------ |
| 1    | 1    | 67   | 74   | 5000  | 不合格 |
| 2    | 2    | 80   | 85   | 11000 | 合格   |
| 3    | 3    | 89   | 87   | 11000 | 合格   |
| 4    | 4    | 78   | 69   | 5000  | 不合格 |




<a id="markdown-16-数据集的导入和导出" name="16-数据集的导入和导出"></a>
## 1.6. 数据集的导入和导出


<a id="markdown-17-建立和调用永久性数据集" name="17-建立和调用永久性数据集"></a>
## 1.7. 建立和调用永久性数据集

SAS数据都是存放在资源管理器的逻辑库中。逻辑库中有SAS自带的6个文件夹，用来存放不同类型的数据。
理论上，我们在用data语句起名字时，还需要告诉SAS建立的数据集是放在哪个文件夹里。如，data sasuser.fh;表示建立数据集fh，放在sasuser这个文件夹，再如data work.fh;表示建立数据集fh，放在work这个文件夹。
SAS默认，如果data语句中没有加文件夹名字，就是**默认为存放到临时文件夹work**中，也就是说，data fh;与data work.fh;是完全等同的。当关闭sas时work内的数据集将清空。


<a id="markdown-171-建立永久性数据集" name="171-建立永久性数据集"></a>
### 1.7.1. 建立永久性数据集

相当于把建立的数据集存放到硬盘的一个文件夹中。具体主要包括三个步骤：

- 在电脑硬盘建立一个文件夹，准备用来存放数据集；
- 在SAS的资源管理器中也新建一个文件夹，起个自己喜欢的英文名字；
- 把这两个文件夹关联起来。

**方式一：菜单中新建**
[1]在本地硬盘建立一个文件夹作为数据集存放处（假设路径为g盘目录下的mysasfile文件夹）
[2]逻辑库处右键新建新库并命名（假设是mydir），路径浏览选择上述文件夹
[3]编辑器处添加数据集

```sas
data mydir.test; /*在mydir库中添加名为test的新数据集*/
input id day: yymmdd8. city:$20.;    
format day yymmddp10.;  
cards;
370685 980515 shandong
;
run; /*运行后，在g盘目录下的mysasfile文件夹中会出现test数据集*/
```
**方式二：编辑器中新建，并与逻辑库关联**
[1]同上
[2]编辑器中新建新库，并添加数据集

```sas
libname mydir "g:\mysasfile"; /*新建名为mydir的新库，并与路径中的文件夹相关联*/
data mydir.test; /*在mydir库中添加名为test的新数据集*/
input id day: yymmdd8. city:$20.;    
format day yymmddp10.;  
cards;
370685 980515 shandong
;
run; /*运行后，在g盘目录下的mysasfile文件夹中会出现test数据集*/
```

**方式三：编辑器中新建**

```sas
data "g:\mysasfile\first";/*在g:\mysasfile\中新建一个名为first的数据集*/
input id day: yymmdd8. city:$20.;    
format day yymmddp10.;  
cards;
370685 980515 shandong
;
run;
```


<a id="markdown-172-调用永久性数据集" name="172-调用永久性数据集"></a>
### 1.7.2. 调用永久性数据集

调用硬盘上的SAS数据集
[1]首先要知道硬盘上的文件夹位置及名称
[2]]利用libname语句读取相应位置的文件夹中的文件

```sas
libname mydir "g:\mysasfile"; 
proc print data= mydir.test;
run;
```