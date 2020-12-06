---
title: '卫生统计及SAS应用（六）卡方检验'
date: 2020-12-05 02:57:56
tags: [biostat,SAS]
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



# 6. Lesson 6 卡方检验

### 6.0.1. 基本方法

| 资料类型                                        | 目的                     | 检验方法             |
| ----------------------------------------------- | ------------------------ | -------------------- |
| 独立资料四格表、R*C列联表                       | 关联性：比较两组阳性率   | 卡方检验             |
| 配对四格表                                      | 关联性：比较两方法阳性率 | McNemar检验          |
| R*C列联表且**分组变量为等级**，指标变量为二分类 | 趋势                     | Cochran-Armitage检验 |
| R*C列联表且分组变量为二分类，**指标变量为等级** | 趋势                     | 秩和检验             |



## 6.1. sas程序实现


### 6.1.1. proc freq < option >

```sas
Proc freq <选项>;
Table 行*列/<选项>; 
Test 统计量关键字；
Weight 权重变量;
By 分层变量;
Run;
```


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


#### 6.1.1.2. test 统计量关键字;

| test统计量关键字 | 作用                                                 |
| ---------------- | ---------------------------------------------------- |
| kapp             | 对一致性系数（Kappa系数）进行统计学检验              |
| measures         | 对tabled语句中measures选项输出的所有关联系数进行检验 |
| pcorr            | 对Pearson相关系数进行检验                            |
| scorr            | 对Spearman相关系数进行检验                           |


#### 6.1.1.3. weight 权重变量;


#### 6.1.1.4. by 分层变量;


