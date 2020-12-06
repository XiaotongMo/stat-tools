---
title: '卫生统计及SAS应用（四）统计描述及分布类型'
date: 2020-12-05 02:54:38
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


# 4. Lesson 4 统计描述及分布类型

## 4.1. 统计描述

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

### 4.1.2. proc univariate

> proc univariate过程：极端值的描述、分位数的计算、生成分布图、生成频数表、正态性检验
>
> 选项有：ALL, ALPHA, ANNOTATE, CIBASIC, CIPCTLDF, CIPCTLNORMAL, CIQUANTDF, CIQUANTNORMAL, DATA, DEBUG, EXCLNPWGT, FREQ, GOUT, LOCCOUNT, MODE, MODES,MU0, NEXTROBS, NEXTRVAL, NOBYPLOT, NOPRINT, NORMAL, NOTABCONTENTS, NOVARCONTENTS,OUTTABLE, PCTLDEF, PLOT, PLOTSIZE, ROBUSTSCALE, ROUND, SUMMARYCONTENTS, TRIMMED,VARDEF, WINSORIZED.
```sas
proc univariate data=a;
var age1;
run;
```

### 4.1.3. proc freq

```sas
proc freq data=a;
tables sex anemia_ana;
run;
proc freq data=a;
tables sex*anemia_ana;
run;
```


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