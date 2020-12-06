硕士课程《卫生统计及SAS应用》

## 目录
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
        - [1.5.2. 数据集中有**缺失值**](#152-数据集中有缺失值)
        - [1.5.3. 有规律的变量](#153-有规律的变量)
        - [1.5.4. 是否换行输入](#154-是否换行输入)
            - [1.5.4.1. 输入重复测量数据](#1541-输入重复测量数据)
        - [1.5.5. 产生新变量](#155-产生新变量)
            - [1.5.5.1. 宽度限制](#1551-宽度限制)
    - [1.6. 数据集的导入和导出](#16-数据集的导入和导出)
    - [1.7. 建立和调用永久性数据集](#17-建立和调用永久性数据集)
        - [1.7.1. 建立永久性数据集](#171-建立永久性数据集)
        - [1.7.2. 调用永久性数据集](#172-调用永久性数据集)
- [2. Lesson 2 数据集的管理](#2-lesson-2-数据集的管理)
    - [2.1. 纵向合并与横向合并](#21-纵向合并与横向合并)
    - [2.2. 拆分为若干个子集](#22-拆分为若干个子集)
        - [2.2.1. 对观测个案的选择 if/where  firstobs/obs](#221-对观测个案的选择-ifwhere--firstobsobs)
            - [2.2.1.1. (1) 条件：if语句、where （选项 或者 语句）](#2211-1-条件if语句where-选项-或者-语句)
            - [2.2.1.2. (2) obs与firstobs（数据集选项）](#2212-2-obs与firstobs数据集选项)
        - [2.2.2. 对变量选择 drop keep](#222-对变量选择-drop-keep)
            - [2.2.2.1. **drop 与keep**（数据集选项 或者 语句）](#2221-drop-与keep数据集选项-或者-语句)
    - [2.3. 排序proc sort](#23-排序proc-sort)
        - [2.3.1. (1) 排序](#231-1-排序)
        - [2.3.2. (2) 查找重复值](#232-2-查找重复值)
            - [2.3.2.1. [1]仅保留不重复值 nodupkey](#2321-1仅保留不重复值-nodupkey)
            - [2.3.2.2. [2]仅保留重复值 nouniquekey](#2322-2仅保留重复值-nouniquekey)
    - [2.4. 转置 proc transpose](#24-转置-proc-transpose)
            - [2.4.0.3. 单纯转置](#2403-单纯转置)
            - [2.4.0.4. 加上by语句，限定某一变量不转置](#2404-加上by语句限定某一变量不转置)
            - [2.4.0.5. 修改列名](#2405-修改列名)
    - [2.5. 对比多个数据集是否一致 proc compare](#25-对比多个数据集是否一致-proc-compare)
    - [2.6. 修饰](#26-修饰)
            - [2.6.0.6. 对变量名的注释](#2606-对变量名的注释)
            - [2.6.0.7. 对变量的值的注释](#2607-对变量的值的注释)
    - [2.7. 输出样式  proc print](#27-输出样式--proc-print)
- [3. Lesson 3 SAS实用函数](#3-lesson-3-sas实用函数)
    - [3.1. （1）与数值有关的函数](#31-1与数值有关的函数)
        - [3.1.1. 数值运算](#311-数值运算)
        - [3.1.2. 数值舍入](#312-数值舍入)
    - [3.2. （2）与统计有关的函数](#32-2与统计有关的函数)
        - [3.2.1. 统计描述](#321-统计描述)
            - [3.2.1.1. 函数表达形式](#3211-函数表达形式)
            - [3.2.1.2. 统计描述函数与算数函数的用法区别：](#3212-统计描述函数与算数函数的用法区别)
    - [3.3. （3）与字符有关的函数](#33-3与字符有关的函数)
        - [3.3.1. 字符转换  input 与 put](#331-字符转换--input-与-put)
        - [3.3.2. 改变大小写](#332-改变大小写)
        - [3.3.3. 字符或字符串的连接](#333-字符或字符串的连接)
        - [3.3.4. 计算变量或字符串的长度lengthn (变量或字符串)](#334-计算变量或字符串的长度lengthn-变量或字符串)
        - [3.3.5. 提取变量或字符串中的字符](#335-提取变量或字符串中的字符)
        - [3.3.6. 查找变量或字符串中的字符 find 与findc](#336-查找变量或字符串中的字符-find-与findc)
        - [3.3.7. 去除变量或字符串中的字符](#337-去除变量或字符串中的字符)
        - [3.3.8. 替换变量或字符串中的字符](#338-替换变量或字符串中的字符)
        - [3.3.9. 查找缺失值](#339-查找缺失值)
    - [3.4. （4）与日期有关的函数](#34-4与日期有关的函数)
        - [3.4.1. 日期提取](#341-日期提取)
        - [3.4.2. 日期间隔函数](#342-日期间隔函数)
    - [3.5. 其他：lag 与dif](#35-其他lag-与dif)
- [4. Lesson 4 统计描述及分布类型](#4-lesson-4-统计描述及分布类型)
    - [4.1. 统计描述](#41-统计描述)
        - [4.1.1. proc means](#411-proc-means)
        - [4.1.2. proc univariate](#412-proc-univariate)
        - [4.1.3. proc freq](#413-proc-freq)
    - [4.2. 正态分布检验](#42-正态分布检验)
- [5.](#5)
- [6. Lesson 5 正态形检验 & t检验](#6-lesson-5-正态形检验--t检验)
- [7. Lesson 6 卡方检验](#7-lesson-6-卡方检验)
        - [7.0.1. 基本方法](#701-基本方法)
    - [7.1. sas程序实现](#71-sas程序实现)
        - [7.1.1. proc freq < option >](#711-proc-freq--option-)
            - [7.1.1.1. table 行*列/< 选项 >](#7111-table-行列-选项-)
            - [7.1.1.2. test 统计量关键字;](#7112-test-统计量关键字)
            - [7.1.1.3. weight 权重变量;](#7113-weight-权重变量)
            - [7.1.1.4. by 分层变量;](#7114-by-分层变量)

<!-- /TOC -->

[Back to Data Science TOC](/data-science/)

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
### 1.5.2. 数据集中有**缺失值**

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

  - **@@** 强行保持当前行。所输入数据均作为**某一变量**的值

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



<a id="markdown-2-lesson-2-数据集的管理" name="2-lesson-2-数据集的管理"></a>
# 2. Lesson 2 数据集的管理

<a id="markdown-21-纵向合并与横向合并" name="21-纵向合并与横向合并"></a>
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



<a id="markdown-22-拆分为若干个子集" name="22-拆分为若干个子集"></a>
## 2.2. 拆分为若干个子集

<a id="markdown-221-对观测个案的选择-ifwhere--firstobsobs" name="221-对观测个案的选择-ifwhere--firstobsobs"></a>
### 2.2.1. 对观测个案的选择 if/where  firstobs/obs

<a id="markdown-2211-1-条件if语句where-选项-或者-语句" name="2211-1-条件if语句where-选项-或者-语句"></a>
#### 2.2.1.1. (1) 条件：if语句、where （选项 或者 语句）

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
<a id="markdown-2212-2-obs与firstobs数据集选项" name="2212-2-obs与firstobs数据集选项"></a>
#### 2.2.1.2. (2) obs与firstobs（数据集选项）

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

<a id="markdown-222-对变量选择-drop-keep" name="222-对变量选择-drop-keep"></a>
### 2.2.2. 对变量选择 drop keep

<a id="markdown-2221-drop-与keep数据集选项-或者-语句" name="2221-drop-与keep数据集选项-或者-语句"></a>
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



<a id="markdown-23-排序proc-sort" name="23-排序proc-sort"></a>
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



<a id="markdown-231-1-排序" name="231-1-排序"></a>
### 2.3.1. (1) 排序

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

<a id="markdown-232-2-查找重复值" name="232-2-查找重复值"></a>
### 2.3.2. (2) 查找重复值
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

<a id="markdown-2321-1仅保留不重复值-nodupkey" name="2321-1仅保留不重复值-nodupkey"></a>
#### 2.3.2.1. [1]仅保留不重复值 nodupkey
注意重复值中仅保留第一个个案

```sas
proc sort out=norep nodupkey;
by name;
proc print data=norep;
run;
```

<a id="markdown-2322-2仅保留重复值-nouniquekey" name="2322-2仅保留重复值-nouniquekey"></a>
#### 2.3.2.2. [2]仅保留重复值 nouniquekey

```sas
proc sort out=rep nouniquekey; 
by name;
proc print data=rep;
```

<a id="markdown-24-转置-proc-transpose" name="24-转置-proc-transpose"></a>
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

<a id="markdown-2403-单纯转置" name="2403-单纯转置"></a>
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


<a id="markdown-2404-加上by语句限定某一变量不转置" name="2404-加上by语句限定某一变量不转置"></a>
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

<a id="markdown-2405-修改列名" name="2405-修改列名"></a>
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



<a id="markdown-25-对比多个数据集是否一致-proc-compare" name="25-对比多个数据集是否一致-proc-compare"></a>
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



<a id="markdown-26-修饰" name="26-修饰"></a>
## 2.6. 修饰

<a id="markdown-2606-对变量名的注释" name="2606-对变量名的注释"></a>
#### 2.6.0.6. 对变量名的注释

```sas
label 变量1= 标签1 变量2=标签2 ...;
```

<a id="markdown-2607-对变量的值的注释" name="2607-对变量的值的注释"></a>
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



<a id="markdown-27-输出样式--proc-print" name="27-输出样式--proc-print"></a>
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



<a id="markdown-3-lesson-3-sas实用函数" name="3-lesson-3-sas实用函数"></a>
# 3. Lesson 3 SAS实用函数





<a id="markdown-31-1与数值有关的函数" name="31-1与数值有关的函数"></a>
## 3.1. （1）与数值有关的函数

<a id="markdown-311-数值运算" name="311-数值运算"></a>
### 3.1.1. 数值运算

| 函数     | 用途                    |
| -------- | ----------------------- |
| mod(x,y) | 返回x除以y的余数        |
| abs(x)   | 返回x的绝对值           |
| exp(x)   | 返回x的指数值           |
| log(x)   | 返回x的自然对数值       |
| log10(x) | 返回x的以10为底的对数值 |
| sqrt(x)  | 返回x的平方根           |



<a id="markdown-312-数值舍入" name="312-数值舍入"></a>
### 3.1.2. 数值舍入

| 函数     | 用途             |
| -------- | ---------------- |
| ceil(x)  | 返回≥x的最小整数 |
| floor(x) | 返回≤x的最大整数 |
| int(x)   | 返回x的整数部分  |

<a id="markdown-32-2与统计有关的函数" name="32-2与统计有关的函数"></a>
## 3.2. （2）与统计有关的函数

<a id="markdown-321-统计描述" name="321-统计描述"></a>
### 3.2.1. 统计描述

| 函数    | 用途                 | 函数     | 用途         |
| ------- | -------------------- | -------- | ------------ |
| n       | 求例数（不含缺失值） | sum      | 求和         |
| nmiss   | 求缺失例数           | stderr   | 求标准误     |
| mean    | 求均数               | min      | 求最小值     |
| median  | 求中位数             | max      | 求最大值     |
| geomean | 求几何均数           | smallest | 求第几小的值 |
| std     | 求标准差             | largest  | 求第几大的值 |
| range   | 求全距               | pctl     | 求百分位数   |
| iqr     | 求四分位数间距       |          |              |
|         |                      |          |              |

<a id="markdown-3211-函数表达形式" name="3211-函数表达形式"></a>
#### 3.2.1.1. 函数表达形式

- 第一类：<u>**函数smallest、largest、pctl**</u>：**函数(k,x1,x2,x3,…xn) 或 函数(k,of x1-xn)**
  其中，k表示第k小（smallest）、第k大（largest）或第k%的值（pctl）

```sas
/*从小到大排序，第k个*/
smallest(k,x1,x2,x3);
smallest(k,of x1-x3);
/*从大到小排序，第k个*/
largest(k,x1,x2,x3);
smallest(k,of x1-x3);
/*第k%的值*/
pctl(k,of x1-x3);
pctl(k,x1,x2,x3);
```

- 第二类：除上述3种函数以外，其余函数的基本用法都是相同的，通常可以写成两种方式：
  **函数(x1,x2,x3,…xn) 或 函数(of x1-xn)**

<a id="markdown-3212-统计描述函数与算数函数的用法区别" name="3212-统计描述函数与算数函数的用法区别"></a>
#### 3.2.1.2. 统计描述函数与算数函数的用法区别：

统计描述函数的计算功能可以由算术函数完成：

```sas
a=mean(of x1-x5);
b=(x1+x2+x3+x4+x5)/5;
```

**统计描述函数**是针对**每个观测的多个变量**进行计算的，而不是针对**某个变量的多个观测**进行计算。（**即计算行的平均值）**
如果想用这些函数求某一变量的多个观测的统计描述指标，可以先利用**proc transpose**将数据转置，然后再用函数求出。

**proc means**可以计算**每个变量的多个观测**的均值。**（即计算列的平均值）**



<a id="markdown-33-3与字符有关的函数" name="33-3与字符有关的函数"></a>
## 3.3. （3）与字符有关的函数

<a id="markdown-331-字符转换--input-与-put" name="331-字符转换--input-与-put"></a>
### 3.3.1. 字符转换  input 与 put

| 函数                  | 变量类型要求                                                 | 作用                                                         |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| input(变量,输入格式); | 变量必须为字符变量。                                         | 除可以将字符型转为数值型外，也可以将字符型转为其它格式的字符型。 |
| put(变量,输出格式);   | 变量可以是字符变量，也可以是数值变量。但它的输出的一定是个字符变量。 | 将数值型变量转换为字符型，也可以将字符变量转换为自己定义的其它格式的字符变量。 |

```sas
/*将看似日期格式的字符型变量转换为真正的日期型变量。
假定有如下数据集，三个变量均为字符型*/
data char;
input sn:$10. d1:$10. d2:$10.;
newd1=input(d1,yymmdd8.);
newd2=input(d2,date9.);
cards;
123 20091012 21oct1999
1235 20130325 06apr2009
;
proc contents;
run;
```

结果为：

| 按字母排序的变量和属性列表 |       |      |      |
| -------------------------- | ----- | ---- | ---- |
| #                          | 变量  | 类型 | 长度 |
| 2                          | d1    | 字符 | 10   |
| 3                          | d2    | 字符 | 10   |
| 4                          | newd1 | 数值 | 8    |
| 5                          | newd2 | 数值 | 8    |
| 1                          | sn    | 字符 | 10   |

```sas
/*将日期转为字符型。*/
data birth;
input id birthday yymmdd8.;         /*输入birthday为数值型，格式为yymmdd8. */
birth=put(birthday,yymmdd10.);    /*将birthday转换为字符型，格式为yymmdd10. */
cards;
1 19800126
2 19781006
3 19790709
4 19811213
5 19801125
;
proc print;
run;
Proc contents;
Run;
```

结果为：

| Obs  | id   | birthday | birth      |
| ---- | ---- | -------- | ---------- |
| 1    | 1    | 7330     | 1980-01-26 |
| 2    | 2    | 6853     | 1978-10-06 |
| 3    | 3    | 7129     | 1979-07-09 |
| 4    | 4    | 8017     | 1981-12-13 |
| 5    | 5    | 7634     | 1980-11-25 |

| 按字母排序的变量和属性列表 |          |      |      |
| -------------------------- | -------- | ---- | ---- |
| #                          | 变量     | 类型 | 长度 |
| 3                          | birth    | 字符 | 10   |
| 2                          | birthday | 数值 | 8    |
| 1                          | id       | 数值 | 8    |



- 使用注意事项：
  - 转换后的变量最好是赋值**给一个新变量**，而不要用原变量名。
  - proc contents; 显示变量类型

<a id="markdown-332-改变大小写" name="332-改变大小写"></a>
### 3.3.2. 改变大小写

| 函数                   | 作用                       |
| ---------------------- | -------------------------- |
| upcase(变量或字符串);  | 作用是将所有字母改为大写。 |
| lowcase(变量或字符串); | 作用是将所有字母改为小写。 |

<a id="markdown-333-字符或字符串的连接" name="333-字符或字符串的连接"></a>
### 3.3.3. 字符或字符串的连接

| 格式                         | 作用                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| cat (变量或字符串1,…)        | 合并几个变量或字符串，**包括空格**                           |
| cats (变量1,…)               | 合并几个变量或字符串，**去除空格**                           |
| catx(分隔符,变量或字符串1,…) | 合并几个变量或字符串，**可插入自定义分隔符**（必须加**双引号**） |

<a id="markdown-334-计算变量或字符串的长度lengthn-变量或字符串" name="334-计算变量或字符串的长度lengthn-变量或字符串"></a>
### 3.3.4. 计算变量或字符串的长度lengthn (变量或字符串)

length(变量或字符串)

计算变量或字符串长度，包括空格，对空值返回0

<a id="markdown-335-提取变量或字符串中的字符" name="335-提取变量或字符串中的字符"></a>
### 3.3.5. 提取变量或字符串中的字符

substrn(变量,起始位置<,提取长度>);
起始位置表示开始提取的位置，如果该值为非正值，则从第一位开始提取。
提取长度表示提取多少位，如果该值为非正值，则提取0位，也就是不提取任何字符；如果不加该参数，默认提取从起始位置以后的所有字符。

```sas
data iden;
input iden $18.; /*输入iden，定义其长度为18*/
if length(iden)=18 then birth=substrn(iden,7,8);
else birth=substrn(iden,7,6); /*根据iden的字符数判断截取的位数*/

cards;
36053319720613591x
360533801215791
360533198208254537
360533851009229
;
proc print;
run;
```

结果为

| Obs  | iden               | birth    |
| ---- | ------------------ | -------- |
| 1    | 36053319720613591x | 19720613 |
| 2    | 360533801215791    | 801215   |
| 3    | 360533198208254537 | 19820825 |
| 4    | 360533851009229    | 851009   |

<a id="markdown-336-查找变量或字符串中的字符-find-与findc" name="336-查找变量或字符串中的字符-find-与findc"></a>
### 3.3.6. 查找变量或字符串中的字符 find 与findc 



这两个函数的意思都是从某变量或字符串中，根据指定的起始位置，查找相应的内容。**如果找到，就返回找到的位置；如果找不到，返回0。find()与findc()类似于逻辑算符**。
如果不加起始位置，默认从第一个字符开始查找。修饰符i的意思是忽略大小写，这样即使你录入和查找的内容大小写不同，也一样可以找到。

find和findc函数都是查找字符，返回其位置，但当指定查找内容是多个字符的时候，它们会有很大差异。

|函数|查找多字符时存在差异|
|---|----|
|find(变量或字符串,查找内容<,“i"> <,起始位置>)|必须是所有字符都完全匹配才算找到|
|findc(变量或字符串,查找内容<,“i"> <,起始位置>)|只要找到字符中的任意一个就算找到|


<a id="markdown-337-去除变量或字符串中的字符" name="337-去除变量或字符串中的字符"></a>
### 3.3.7. 去除变量或字符串中的字符

compress(变量或字符串<,欲去除的字符><,"修饰符">)
该函数的作用是从变量或字符串中去掉“欲去除的字符”，如果不指定“欲去除的字符”，默认是去除空格。

该函数还可以指定不同的修饰符实现相应的作用，常用的修饰符主要有以下几个：

|修饰符|作用|
|---|---|
|a|去掉变量或字符串中的所有字母|
|d|去掉变量或字符串中的所有数字|
|s|去掉变量或字符串中的所有空格|
|i|忽略大小写|

<a id="markdown-338-替换变量或字符串中的字符" name="338-替换变量或字符串中的字符"></a>
### 3.3.8. 替换变量或字符串中的字符

tranwrd(变量或字符串,查找值,替换值)

<a id="markdown-339-查找缺失值" name="339-查找缺失值"></a>
### 3.3.9. 查找缺失值

missing(变量)
其作用就是判断指定的变量是否存在缺失值，**是则返回1，不是返回0。相当于逻辑变量。**该变量既可以是字符型变量也可以是数值型变量。





<a id="markdown-34-4与日期有关的函数" name="34-4与日期有关的函数"></a>
## 3.4. （4）与日期有关的函数

<a id="markdown-341-日期提取" name="341-日期提取"></a>
### 3.4.1. 日期提取

| 函数                   | 作用                                     |
| ---------------------- | ---------------------------------------- |
| year(日期变量)         | 返回日期变量或日期值的年                 |
| month(日期变量)        | 返回日期变量或日期值的月                 |
| day(日期变量)          | 返回日期变量或日期值的日                 |
| qtr(日期变量)          | 返回日期变量或日期值的季度               |
| week(日期变量)         | 返回日期变量或日期值的周数（第几周）     |
| weekday(日期变量)      | 返回日期变量或日期值的周（周几）         |
| datepart(日期时间变量) | 返回日期时间变量中的日期部分             |
| timepart(日期时间变量) | 返回日期时间变量中的时间部分             |
| mdy(月,日,年)          | 将月、日、年合并为一个日期格式的值或变量 |

补充：日期时间变量的格式有 **ymdttm**

```sas
data miss;
input date: yymmdd10. time: ymddttm30.;     /*指定time为ymddttm格式 */
cards;
2009/6/25	2009/6/26:11:00:00.00
2009/6/24	2009/6/25:19:00:00.00
2009/6/23	2009/6/24:13:00:00.00
2009/6/23	2009/6/24:14:00:00.00
2009/6/25	2009/6/26:13:00:00.00
;
data miss;
set miss;
date1=datepart(time); /*提取time的日期部分 */
time1=timepart(time); /*提取time的时间部分 */
year=year(date1); /*提取date1的年 */
month=month(date1); /*提取date1的月 */
week=week(date1); /*提取date1的周 */
format time datetime30.; /*指定time的输出格式为datetime */
format date date1 yymmdd10.; /*指定date、date1的输出格式为yymmdd */
format time1 time12.; /*指定time1的输出格式为time */
proc print;
run;
```

结果为

| Obs  | date       | time               | date1      | time1    | year | month | week |
| ---- | ---------- | ------------------ | ---------- | -------- | ---- | ----- | ---- |
| 1    | 2009-06-25 | 26JUN2009:11:00:00 | 2009-06-26 | 11:00:00 | 2009 | 6     | 25   |
| 2    | 2009-06-24 | 25JUN2009:19:00:00 | 2009-06-25 | 19:00:00 | 2009 | 6     | 25   |
| 3    | 2009-06-23 | 24JUN2009:13:00:00 | 2009-06-24 | 13:00:00 | 2009 | 6     | 25   |
| 4    | 2009-06-23 | 24JUN2009:14:00:00 | 2009-06-24 | 14:00:00 | 2009 | 6     | 25   |
| 5    | 2009-06-25 | 26JUN2009:13:00:00 | 2009-06-26 | 13:00:00 | 2009 | 6     | 25   |



<a id="markdown-342-日期间隔函数" name="342-日期间隔函数"></a>
### 3.4.2. 日期间隔函数

yrdif (开始日期,结束日期, “actual")
该函数返回从“开始日期”到“结束日期”的实际差值（单位为年），根据不同的“计算依据”，会得到不同的计算结果。
“actual” 意思是根据当年的实际天数来计算（考虑到当年是否闰年等情况）。

```sas
data dm;
input start: yymmdd8. end: yymmdd8.; 
life=yrdif(start,end);  /*计算两个日期之间的实际年数，比较有无actual的结果 */
lifea=yrdif(start,end,"actual");
format start end yymmdd10.; cards;
20090613 20111225
20080916 20120106
20100408 20120909
20111031 20120318
;
proc print;
run;
```

| Obs  | start      | end        | lifea（有actual） | life（无actual） |
| ---- | ---------- | ---------- | ----------------- | ---------------- |
| 1    | 2009-06-13 | 2011-12-25 | 2.53425           | 2.53425          |
| 2    | 2008-09-16 | 2012-01-06 | 3.30601           | 3.30685          |
| 3    | 2010-04-08 | 2012-09-09 | 2.42277           | 2.42192          |
| 4    | 2011-10-31 | 2012-03-18 | 0.38025           | 0.37808          |

<a id="markdown-35-其他lag-与dif" name="35-其他lag-与dif"></a>
## 3.5. 其他：lag 与dif

|函数|作用|
|---|---|
|lag函数|作用是返回指定变量的前一个（或前几个）记录|
|dif函数|返回当前记录与前一个（或前几个）记录的差值|
lag(变量)、lag2(变量)、lag3(变量)、……
dif(变量)、dif2(变量)、dif3(变量)、……
这两个函数在处理动态数据、追踪数据方面几乎是必备的

计算年度环比

```sas
data dm;
input year profit;
plag=lag(profit);        /*返回profit变量的前一个记录 */
pdif=dif(profit);        /*返回profit变量当前记录与前一个记录的差值 */
pratio=profit/plag;    /*计算profit变量当前记录与前一个记录的比值 */
cards;
2008 989
2009 1002
2010 1023
2011 1022
2012 1065
2013 1112
;
proc print;
run;	
```

结果：

| Obs  | year | profit | plag | pdif | pratio  |
| ---- | ---- | ------ | ---- | ---- | ------- |
| 1    | 2008 | 989    | .    | .    | .       |
| 2    | 2009 | 1002   | 989  | 13   | 1.01314 |
| 3    | 2010 | 1023   | 1002 | 21   | 1.02096 |
| 4    | 2011 | 1022   | 1023 | -1   | 0.99902 |
| 5    | 2012 | 1065   | 1022 | 43   | 1.04207 |
| 6    | 2013 | 1112   | 1065 | 47   | 1.04413 |



<a id="markdown-4-lesson-4-统计描述及分布类型" name="4-lesson-4-统计描述及分布类型"></a>
# 4. Lesson 4 统计描述及分布类型

<a id="markdown-41-统计描述" name="41-统计描述"></a>
## 4.1. 统计描述

<a id="markdown-411-proc-means" name="411-proc-means"></a>
### 4.1.1. proc means

> proc means过程：均值、标准差、标准误、方差、变异系数、极差、t值、偏度系数、峰度系数、可信区间上下限。

```sas
data a;
set ysc.anemia;
run;
proc means data=a;
var age1 hb;
run;
-----------------------------
proc means data=a maxdec=3 mean range clm alpha=0.05;
/*maxdec小数位数为3*/
var age1 hb;
class sex;
run;
-----------------------------
proc sort data=a;
by sex; run;
proc means data=a maxdec=3 mean range clm alpha=0.05;
var age1 hb; by sex; run;
```

<a id="markdown-412-proc-univariate" name="412-proc-univariate"></a>
### 4.1.2. proc univariate

> proc univariate过程：极端值的描述、分位数的计算、生成分布图、生成频数表、正态性检验
>
> 选项有：ALL, ALPHA, ANNOTATE, CIBASIC, CIPCTLDF, CIPCTLNORMAL, CIQUANTDF, CIQUANTNORMAL, DATA, DEBUG, EXCLNPWGT, FREQ, GOUT, LOCCOUNT, MODE, MODES,MU0, NEXTROBS, NEXTRVAL, NOBYPLOT, NOPRINT, NORMAL, NOTABCONTENTS, NOVARCONTENTS,OUTTABLE, PCTLDEF, PLOT, PLOTSIZE, ROBUSTSCALE, ROUND, SUMMARYCONTENTS, TRIMMED,VARDEF, WINSORIZED.
```sas
proc univariate data=a;
var age1;
run;
```

<a id="markdown-413-proc-freq" name="413-proc-freq"></a>
### 4.1.3. proc freq

```sas
proc freq data=a;
tables sex anemia_ana;
run;
proc freq data=a;
tables sex*anemia_ana;
run;
```

<a id="markdown-42-正态分布检验" name="42-正态分布检验"></a>
## 4.2. 正态分布检验
```sas
/*绘制直方图*/
proc gchart data=ysc.anemia;
title1 'histogram';
pattern color=black value=empty;
vbar age1 hb;
run;
/*正态性检验*/
proc univariate data=ysc.anemia normal;
vbar age1 hb;
run;
```



<a id="markdown-6-lesson-5-正态形检验--t检验" name="6-lesson-5-正态形检验--t检验"></a>
# 5. Lesson 5 正态形检验 & t检验

<a id="markdown-7-lesson-6-卡方检验" name="7-lesson-6-卡方检验"></a>
# 6. Lesson 6 卡方检验

<a id="markdown-701-基本方法" name="701-基本方法"></a>
### 6.0.1. 基本方法

| 资料类型                                        | 目的                     | 检验方法             |
| ----------------------------------------------- | ------------------------ | -------------------- |
| 独立资料四格表、R*C列联表                       | 关联性：比较两组阳性率   | 卡方检验             |
| 配对四格表                                      | 关联性：比较两方法阳性率 | McNemar检验          |
| R*C列联表且**分组变量为等级**，指标变量为二分类 | 趋势                     | Cochran-Armitage检验 |
| R*C列联表且分组变量为二分类，**指标变量为等级** | 趋势                     | 秩和检验             |



<a id="markdown-71-sas程序实现" name="71-sas程序实现"></a>
## 6.1. sas程序实现

<a id="markdown-711-proc-freq--option-" name="711-proc-freq--option-"></a>
### 6.1.1. proc freq < option >

```sas
Proc freq <选项>;
Table 行*列/<选项>; 
Test 统计量关键字；
Weight 权重变量;
By 分层变量;
Run;
```

<a id="markdown-7111-table-行列-选项-" name="7111-table-行列-选项-"></a>
#### 6.1.1.1. table 行*列/< 选项 >

| table选项    | 作用                                                         | 统计方法                          |
| ------------ | ------------------------------------------------------------ | --------------------------------- |
| chisq        | 可输出Pearson *χ**2*检验、似然比检验、Mantel-Haenszel检验、phi系数、列联系数等值。   四格表还可输出连续校正*χ**2*检验和Fisher确切检验 | 卡方检验                          |
| relrisk      | 输出相对危险度，仅限于四格表资料                             |                                   |
| trend        | 输出**Cochran-Armitage趋势检验结果**，仅限于2×C表或R×2表     | 趋势卡方检验                      |
| measures     | 计算一系列关联性指标及其渐近标准误，如Pearson相关系数、Spearman相关系数、Kendalls’tau-b值、Gamma系数等 |                                   |
| aggree       | 仅限于R×R表（即行列数相同），可输出**一致性系数**。对配对四格表还给出McNemar配对检验结果，对R×R表给出Boeker对称性检验结果 | 一致性检验；配对四格表McNemar检验 |
| cmh          | 计算Cochran-Mantel-Haenszel统计量，对于多维列联表，可计算校正后的行变量与列变量的关联程度 |                                   |
| nopercent    | 不显示总数的百分比                                           |                                   |
| norow        | 不显示行合计的百分比                                         |                                   |
| nocol        | 不显示列合计的百分比                                         |                                   |
| **expected** | 显示理论数                                                   |                                   |
| fisher       | 输出Fisher确切概率                                           |                                   |
| binomial     | 输出单组的百分比及其可信区间                                 |                                   |

<a id="markdown-7112-test-统计量关键字" name="7112-test-统计量关键字"></a>
#### 6.1.1.2. test 统计量关键字;

| test统计量关键字 | 作用                                                 |
| ---------------- | ---------------------------------------------------- |
| kapp             | 对一致性系数（Kappa系数）进行统计学检验              |
| measures         | 对tabled语句中measures选项输出的所有关联系数进行检验 |
| pcorr            | 对Pearson相关系数进行检验                            |
| scorr            | 对Spearman相关系数进行检验                           |

<a id="markdown-7113-weight-权重变量" name="7113-weight-权重变量"></a>
#### 6.1.1.3. weight 权重变量;

<a id="markdown-7114-by-分层变量" name="7114-by-分层变量"></a>
#### 6.1.1.4. by 分层变量;

