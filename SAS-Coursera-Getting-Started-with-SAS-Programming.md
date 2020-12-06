<span id="jump">**SAS courses contents**</span>
  


<!-- TOC -->

- [1. essential (skipped)](#1-essential-skipped)
- [2. Accessing data](#2-accessing-data)
    - [2.1. required column attributes for SAS tables](#21-required-column-attributes-for-sas-tables)
    - [2.2. check the table](#22-check-the-table)
    - [2.3. libname](#23-libname)
    - [2.4. importing unstructured data](#24-importing-unstructured-data)
- [3. Exploring data](#3-exploring-data)
    - [3.1. Explore and validate data with SAS procedures](#31-explore-and-validate-data-with-sas-procedures)
    - [3.2. Filter rows in a report](#32-filter-rows-in-a-report)
    - [3.3. Replace text in a program using SAS macro variables](#33-replace-text-in-a-program-using-sas-macro-variables)
    - [3.4. Format data values in results](#34-format-data-values-in-results)
    - [3.5. Sort a table](#35-sort-a-table)
    - [3.6. Identify and remove duplicate rows in a table](#36-identify-and-remove-duplicate-rows-in-a-table)
- [4. preparing data](#4-preparing-data)
    - [4.1. Reading and filtering data](#41-reading-and-filtering-data)
    - [4.2. computing new columns](#42-computing-new-columns)
    - [4.3. conditional processing](#43-conditional-processing)
- [5. Analyzing and reporting data](#5-analyzing-and-reporting-data)
    - [5.1. Enhancing reports with titles, footnotes, and labels](#51-enhancing-reports-with-titles-footnotes-and-labels)
    - [5.2. Creating frequency reports](#52-creating-frequency-reports)
        - [5.2.1. Creating Frequency Reports and Graphs](#521-creating-frequency-reports-and-graphs)
        - [5.2.2. Creating Two-Way Frequency Reports](#522-creating-two-way-frequency-reports)
    - [5.3. Creating summary reports and data](#53-creating-summary-reports-and-data)
        - [5.3.1. Summary](#531-summary)
- [6. Exporting Results and SQL in SAS](#6-exporting-results-and-sql-in-sas)
    - [6.1. Exporting Results - Exporting data](#61-exporting-results---exporting-data)
    - [6.2. Exporting Results - Exporting reports](#62-exporting-results---exporting-reports)
    - [6.3. Structured Query Language(SQL) in SAS](#63-structured-query-languagesql-in-sas)
        - [6.3.1. SQL basic syntax - PROC SQL](#631-sql-basic-syntax---proc-sql)
        - [6.3.2. filter and sort data](#632-filter-and-sort-data)
        - [6.3.3. create and delete tables in SQL](#633-create-and-delete-tables-in-sql)
        - [6.3.4. join tables](#634-join-tables)

<!-- /TOC -->

[Back to Data Science TOC](/data-science/)

<a id="markdown-1-essential-skipped" name="1-essential-skipped"></a>
# 1. essential (skipped)
please use search engine to find ways to install SAS
<a id="markdown-2-accessing-data" name="2-accessing-data"></a>
# 2. Accessing data

<a id="markdown-21-required-column-attributes-for-sas-tables" name="21-required-column-attributes-for-sas-tables"></a>
## 2.1. required column attributes for SAS tables
- name
Column names:
  - 1~32 characters.
  - cannot begin with numbers.    eg. *6month*
  - cannot have spaces.   eg.*month 6*
  - cannot have special marks like hash marks.   eg.*month#6*

- type
  - numeric
  including data
  0 = Jan 1,1960
  
  - character
  
  |numeric|character|
  | ----- | ----- |
  |digits 0~9                            |letters|
  |minus sign                            |numbers|
  |decimal point                         |    special characters|
  |scientific notations(the power of 10) |   blanks             |
  |.(a period) = missing                 |  (a space) = missing |
  
- length
  - numeric
    - 8 bytes(~16 significant digits)
  - character
    - 1~32,767 bytes(1 byte = one character)

<a id="markdown-22-check-the-table" name="22-check-the-table"></a>
## 2.2. check the table
- proc contents data = (tablename);


<a id="markdown-23-libname" name="23-libname"></a>
## 2.3. libname
- create library  
```LIBNAME libref engine "path";```
  - the name of the library'libref':
    - 8 character maximum
    - starts with letter or underscore
    - continues with letters, numbers, or underscores
  - engine
    - .xlsx, .access, .txt, .sas7bdat
- delete library  
```LIBNAME libref clear;```

- read other types of files  
```sas
LIBNAME libref XLSX "path/file-name.xlsx";
```  
- get rid of spaces in the column names
```sas
OPTIONS validvarname = v7/* means getting rid of the spaces in the names of the columns */
```

ref:https://support.sas.com/documentation/cdl/en/acpcref/63181/HTML/default/viewer.htm#n1wvmggexroxgyn17rp61jml3cvn.htm

<a id="markdown-24-importing-unstructured-data" name="24-importing-unstructured-data"></a>
## 2.4. importing unstructured data 
- proc import
```sas
proc import datafile="path/filename" dbms=filetype
            out=output-table<replace;
  <guessingrows=n|max;>/*检查前n行来判断列的数据类型*/
run;
```

- method comparison of accessing data: 
*data "..." vs proc  import datafile="..."*  
1. data "..."
```sas
data libref xlsx "path";
```
2. proc import datafile="..."
```sas
proc import datafile="path" 
    dbms=xlsx 
    out=libcopy 
    replace;
run;
```
|data libref xlsx "path";|proc import datafile="path" dbms=xlsx out=libcopy replace;</p>run;|
| --------- | --------- |
|data is always correct|data is copied and maybe changed|

[Contents](#jump)


<a id="markdown-3-exploring-data" name="3-exploring-data"></a>
# 3. Exploring data

<a id="markdown-31-explore-and-validate-data-with-sas-procedures" name="31-explore-and-validate-data-with-sas-procedures"></a>
## 3.1. Explore and validate data with SAS procedures
Several procedures can be applied to data exploration.
- proc print
```
proc print data=(datasetname) ;
   <options>;*var (variable-name) means showing variables listed
run;
```
- proc means
```sas
proc means data=(datasetname);
   <options>;*var (variable-name) means showing variables listed
run;
```
- proc univariate
```sas
proc univariate data=(datasetname) ;
   <options>;*var (variable-name) means showing variables listed
run;
```
- proc freq   
--!!!  table
```sas
proc freq data=(datasetname) ;
   <options>;*table (variable-name) means showing variables listed
run;
```

<a id="markdown-32-filter-rows-in-a-report" name="32-filter-rows-in-a-report"></a>
## 3.2. Filter rows in a report
- option in procedure: <span id="where"> where </span> 
--!!! where also ...
  - <span id="whereref">ref</span>  
    -  https://v8doc.sas.com/sashtml/lgref/z0202951.htm  
    -  https://documentation.sas.com/?docsetId=lestmtsref&docsetTarget=n1xbr9r0s9veq0n137iftzxq4g7e.htm&docsetVersion=9.4&locale=en#n13ffalz5o6yyxn19qql699bykad
```sas
proc ...;* print
    where where-expression;
    where also where-expression;*also means two where statement work simultaneously
run;
```
  - expression(see sas docs [ref](#whereref))
  - special expression
    - missing item: **missing**
    ```sas
    where var is missing;
    where var is not misssing;
    ```
    - pattern pairing: **like " _ %"**, *"..." is case sensitive*
    ```sas
    where var like "New%";
    /*the result would be New York, New Delhi etc.
    % is for a string*/   
    where var like "Sant_ %";
    /*the result would be Santo Clara, Santa Cruz etc.
    _ is for a single letter*/
    ```
    - contains: *"..." is case sensitive*
    ```sas
    where var contains "...";
    /*相当于 where var like "%...%";*/
    ```
    where usages:
    |   运算符    |    含义  | 使用方法 |
    | ----------- | ------- | -------- |
    | like        | 类似（开头是，中间是，结尾是） |where var like "...%"或者where var like "%...%"或者where var like "%..."|
    | contains    | 包含  | where var contains "..."  |
    | ne或者not = | 不是 | where var ne "..."或者where var not = "..." |
    | in          | 在某几个范围中 | where var in ('A','B','C')|
    | and         | 并且 | where 条件1 and 条件2 |
    | also        | 同时 |已有第一个where之后，必须 where also 条件2|
    

    
<a id="markdown-33-replace-text-in-a-program-using-sas-macro-variables" name="33-replace-text-in-a-program-using-sas-macro-variables"></a>
## 3.3. Replace text in a program using SAS macro variables
macro variables help to replace the values of  ***the same varibale*** used in several procedures.  
macro variable must be given at the beginning.  
macro variable makes the program dynamic.


```sas
%let cartype=wagon; *%let*
proc print...;
  where type="&cartype"; *"&..."*
  var type make model msrp;
run;
proc means...;
  where type="&cartype";
  var type make model msrp;
run;
proc freq...;
  where type="&cartype";
  var type make model msrp;
run;

```

<a id="markdown-34-format-data-values-in-results" name="34-format-data-values-in-results"></a>
## 3.4. Format data values in results
- format statement: *did not change* the data
  ```sas
  proc print data=...;
      format col-name(s) format;
      /*format is composed this way:  <$>format-name<w>.<d>
      - $ means character format
      - <w> means total width including decimals and special characters
      - . is a required delimiter
      - <d> is for numeric variables and means number of decimal places */
  run;

  /*the variable n_of_trees is numeric*/
  format n_of_trees notf 5.0;

  ```
|format name|example value|format applied|formatted value|decimal|actual width|maximal width|
|-|-|-|-|-|-|-|
|w.d|12345.67|5.|12345|0|5|5|
|w.d|12345.67|8.1|12345.7|5|7|8|
|COMMAw.d|12345.67|comma8.1|12,345.7|1|8|8|
|w.d|12345.67|comma7.1||||
|DOLLARw.d|12345.67|dollar10.2|$12,345.67|1|10|10|
|DOLLARw.d|12345.67|dollar10.|$12,346|0|7|10|
|YENw.d|12345.67|yen7.|\12,346|0|7|7|
|EUROw.d|12345.67|euro10.2|E12,345.67|2|10|10|
***\*where there is a currency symbol,  there is a comma***  
表示方式优先考虑的顺序是：  
1. w（总宽度，当实际小数位小于d则四舍五入；当整数位大于d，则四舍五入并用科学记数法E）--> 
2. 整数位（原有的整数位）--> 
3. d（小数位，当实际小数位超出则四舍五入，不足则补零在后）--> 
4. 货币符号（当仍未达到总宽度，可加上）--> 
5. comma（整数每三位加逗号，加则全都加，不加则全都不加
- Zw.d
```sas
data score;
    input Student $ StudentNumber;
    format studentnumber z4.;/*z4. pads right-justified output with zero instead of spaces*/
   datalines;
Capalleti 545
Engles    1167
Krupski   2527
McBane    674
Nguyen    886
Si        4915
;
proc print data=score;
run;
```
output is added ***zero before the value*** if the width of the value is not the longest
```
观测	Student	StudentNumber
1	Capalleti	0545
2	Engles	1167
3	Krupski	2527
4	McBane	0674
5	Nguyen	0886
6	Si	4915
```


- common formats for date value
when the value is 21199

|format|formatted value|
|-|-|
|date7.|15JAN18|
|date9.|15JAN2018|
|mmddyy10.|01/15/2018|
|ddmmyy8.|15/01/18|
|monyy7.|JAN2018|
|monname.|January|
|weekdate.|Monday, January 15, 2018|


<a id="markdown-35-sort-a-table" name="35-sort-a-table"></a>
## 3.5. Sort a table
proc sort
```sas
proc sort data=.. <out=..>;
  by <descending> var-name;
run;

*example
proc sort data=..;
  by name descending score;
run;
```


<a id="markdown-36-identify-and-remove-duplicate-rows-in-a-table" name="36-identify-and-remove-duplicate-rows-in-a-table"></a>
## 3.6. Identify and remove duplicate rows in a table
options in **PROC SORT** --NODUPRECS  DUPOUT=...
- remove the duplicates
  - the rest are in OUTPUT
  - the removed are in DUPOUT
```sas
PROC SORT DATA=input-table  
          < OUT=output-table >
          NODUPRECS < DUPOUT=output-table >;
    BY _ALL_;
RUN;
```
options in **PROC SORT** -- NODUPKEY DUPOUT=...
- keep only first occurrence of each unique value
```sas
PROC SORT DATA=input-table  
          < OUT=output-table >
          NODUPKEY < DUPOUT=output-table >;
    BY < DESCENDING > col-name(s);
RUN;
```
[Contents](#jump)

<a id="markdown-4-preparing-data" name="4-preparing-data"></a>
# 4. preparing data

<a id="markdown-41-reading-and-filtering-data" name="41-reading-and-filtering-data"></a>
## 4.1. Reading and filtering data
-  Using DATA step to create a SAS data set
```sas
data output-table;
  set input-table;
run;
```
-  DATA step processing
     - DATA step is excuted ***row by row.***
     - statements: 
       - where: [where usage](#where)
       - keep/drop variable-name(s);
      only keep or delete the variables(columns)
```sas
data myclass;
    set sashelp.class;
    keep name age height;    *drop sex weight;
run;
```
```sas
-  build a permanent data set
/* way 1 */
data "/folders/myfolders/EPG194/output/storm_cat5";
	set pg1.storm_summary;
run;

/* way 2 */
libname test "/folders/myfolders/EPG194/output";
data test.storm_cat5;
	set pg1.storm_summary;
run;
```
<a id="markdown-42-computing-new-columns" name="42-computing-new-columns"></a>
## 4.2. computing new columns
- Using expression to create new columns

```sas
DATA output-table;
    SET input-table;
    new-column = expression;
RUN;
```

- Using summary functions

|function|meaning|
|--|--|
|sum(n1,n2,...)|sum of n1,n2,...|
|mean(n1,n2,...)|mean of n1,n2,...|
|median(n1,n2,...)|median of n1,n2,...|
|range(n1,n2,...)|range of n1,n2,...|

- Using character functions

|function|meaning|before|after|
|--|--|--|--|
|upcase(char)</br>lowcase(char)|change to uppercase or lowercase|upcase(aBc)</br>lowcase(aBc)|ABC</br>abc|
|propcase(char,< delimiters >)|change 1st letter to uppercase and other letters to lowercase|propcase(aBc)|Abc|
|CATS(char1,char2,...)|concatenates character strings and removes leading and trailing blanks from each argument|cats(aBc, Anything)|aBcAnything|
|substr(char,position,< length>)|return a substring from  a character string|substr(aBc,3,2)</br>substr(aBc,2,2)</br>substr(aBc,1,2)|Bc</br>aB</br>a|


- Using date functions

|function|meaning|before|after|
|--|--|--|--|
|month(SAS-date)|1~12 representing the month|
|year(SAS-date)|4-digit|||
|day(SAS-date)|1~31 representing the day|||
|weekday(SAS-date)|1~7 representing the weekday|||
|today()||||
|mdy(month,day,year)|returns a SAS date value from numeric month, day, and year values|||
|yrdif(startdate,endate,'AGE')|calculates a precise age between two dates|||


<a id="markdown-43-conditional-processing" name="43-conditional-processing"></a>
## 4.3. conditional processing
- IF...THEN...;ELSE < IF...THEN... >;
```sas
...
if number < 10 then group=1;
else of number <20 then group=2;
else group =3;
...
```
- IF...THEN DO;...;END;(do与end搭配)
data step 可以有两个数据集（表格）
```SAS
data under40 over40;
  set sashelp.cars;
  keep make model msrp cost_group;
  if msrp<20000 then do;
    cost_group = 1;
    output under40;
  end;
  else do;
    cost_group = 2;
    output over40;
  end;
run;
```

- Length
```sas
length var $ number;
```


<a id="markdown-5-analyzing-and-reporting-data" name="5-analyzing-and-reporting-data"></a>
# 5. Analyzing and reporting data
<a id="markdown-51-enhancing-reports-with-titles-footnotes-and-labels" name="51-enhancing-reports-with-titles-footnotes-and-labels"></a>
## 5.1. Enhancing reports with titles, footnotes, and labels
```
***********************************************************;
*  Enhancing Reports                                      *; 
***********************************************************;
*  Syntax and Example                                     *;
*                                                         *;
*    TITLEn "title-text";                                 *;
*    FOOTNOTEn "footnote-text";                           *;
*		                                                      *;
*    LABEL col-name="label-text"                          *;
*          col-name="label-text";                         *;
*                                                         *;
*    Grouped Reports (sort first):                        *;
*    PROC procedure-name;                                 *;
*        BY col-name;                                     *; 
*    RUN;                                                 *;
***********************************************************;  
```
- title & footnote  
  - creat...
  ```sas
  title<n> "title-text";
  footnote<n> "footnote-text";
  ```      
  - clear... = null
  ```sas
  title;/* clear all the titles*/
  footnote;/* clear all the footnotes*/
  ```

- label
  - in PROC MEANS
  ```sas
  proc means ...;
  ...;
  label <var-name> = <column-label>;
  ```  
  - in PROC PRINT  
  **放一个label 在proc的后面！！**
  ```sas
  proc print.. label;
    ...;
    label <var-name> = <column-label>;
  ```
  - in DATA  
  **permanent label**

- by
  - in PROC SORT  
  **by a variable** means that the variable(s) will be sorted in order of **increasing** value  
  **by descending a variable**means that the variable(s) will be sorted in order of **descending** value 

  - in PROC FREQ  
  **by a variable** means that the table will be seperated by the variable into several tables according to the types of the variable  
  **ONE VARIABLE**


<a id="markdown-52-creating-frequency-reports" name="52-creating-frequency-reports"></a>
## 5.2. Creating frequency reports
- **PROC FREQ**
```sas
proc freq ...<proc options>;
  tables var ... / <options>;
  <options>;
run;
```
<a id="markdown-521-creating-frequency-reports-and-graphs" name="521-creating-frequency-reports-and-graphs"></a>
### 5.2.1. Creating Frequency Reports and Graphs
```
***********************************************************;
*  Creating Frequency Reports and Graphs                  *;
***********************************************************;
*  Syntax and Example                                     *;
*                                                         *;
*    ODS GRAPHICS ON;                                     *;
*    PROC FREQ DATA=input-table <proc-options>;           *;
*        TABLES col-name(s) / options;                    *;
*    RUN;                                                 *;
*                                                         *;
*    PROC FREQ statement options:                         *;
*        ORDER=FREQ|FORMATTED|DATA                        *;
*        NLEVELS                                          *;
*    TABLES statement options:                            *;
*        NOCUM                                            *;
*        NOPERCENT                                        *;
*        PLOTS=FREQPLOT                                   *;
*           (must turn on ODS Graphics)                   *;
*        OUT=output-table                                 *;
***********************************************************;
```
- basic frequency reports
```sas
proc freq data=..;
  tables var1 var2; /*分别输出以这两个变量计算频率的表格*/
run;
```
- order = freq nlevels /*以上表格按照频率从大到小排序*/
```sas
proc freq data=.. order = freq nlevels ;
  tables var1 var2; 
run;
```
- no cumulative percent and frequenciess  
  / nocum
```sas
proc freq data=.. ;
  tables var1 var2 / nocum; 
run;
```
- change date to month  
  format var monname.  
```sas
proc freq data=.. ;
  tables var1 var2; 
  label var1 monname.;
run;
```
- output a graph
```sas
ods graphics on;
ods noproctitle;
proc freq data=pg1.storm_final order=freq nlevels;
	tables BasinName startdate / nocum plots = freqplot(orient=horizontal scale=percent);/*一般默认最后一个变量，该行则是startdate*/
	format startdate monname.;
	label startdate = "storm month"
	basinname = "basin";
run;
title;
ods proctitle;
```
<a id="markdown-522-creating-two-way-frequency-reports" name="522-creating-two-way-frequency-reports"></a>
### 5.2.2. Creating Two-Way Frequency Reports 
```
***********************************************************;
*  Creating Two-Way Frequency Reports                     *;
***********************************************************;
*  Syntax and Example                                     *;
*                                                         *;
*    PROC FREQ DATA=input-table;                          *;
*        TABLES col-name*col-name </ options>;            *;
*    RUN;                                                 *;
*                                                         *;
*    PROC FREQ statement options:                         *;
*        NOPRINT                                          *;
*    TABLES statement options:                            *;
*        NOROW, NOCOL, NOPERCENT                          *;
*        CROSSLIST, LIST                                  *;
*        OUT=output-table                                 *;
***********************************************************;
```



<a id="markdown-53-creating-summary-reports-and-data" name="53-creating-summary-reports-and-data"></a>
## 5.3. Creating summary reports and data
**PROC MEANS**
```
***********************************************************;
*  Creating Summary Statistics Reports                    *;
***********************************************************;
*  Syntax and Example                                     *;
*                                                         *;
*    PROC MEANS DATA=input-table stat-list;               *;
*        VAR col-name (s);                                *;
*        CLASS col-name (s);                              *;
*        WAYS n;                                          *;
*    RUN;                                                 *;
***********************************************************;
```
- 计算统计量：proc options:mean median min max etc.
- 不输出
- 按类别归组分类：class statement   
一个或多个变量、呈现方式有多个变量可选择。
- 输出sas表格
  ```sas
  proc means data=pg1.storm_final mean median min max maxdec=0;
    var MaxWindMPH;
    class basinname stormtype;
    ways 0 1 2;/*呈现方式*/
    output out=<new name> <new column name>='...';
  run;
  ```

<a id="markdown-531-summary" name="531-summary"></a>
### 5.3.1. Summary
procedure  | procedure statement               | inside statement                                   | attentions
-----------|-----------------------------------|----------------------------------------------------|-----------
PROC PRINT | label(required if labeled),                      | label,                                             |
PROC FREQ  | out=freq/formatted/data, nlevels, | label,</p> tables< /option>,</p> by(grouping, one) | tabels-options: norow,</p> nocol,</p> nopercent,</p> crosslist,</p> list,</p> out=...,</p> plots=freqplot(groupby=... orient=... scale=...) **(ODS graphics on!!!)**
PROC MEANS | < stat-list>n, mean,              | label,</p> var,</p>  class,</p>  ways,             |
PROC SORT  | noduprec,</p> nodupkey,</p>       | by(sorting, one or more)                                |
**DATA     |                                   | label(permanent),                                       |


[Contents](#jump)

<a id="markdown-6-exporting-results-and-sql-in-sas" name="6-exporting-results-and-sql-in-sas"></a>
# 6. Exporting Results and SQL in SAS



<a id="markdown-61-exporting-results---exporting-data" name="61-exporting-results---exporting-data"></a>
## 6.1. Exporting Results - Exporting data
- PROC EXPORT
    ```sas
    proc export data=input-table 
                outfile="output-file" 
                <DBMS=identifier> 
                <replace>;
    run;
    ```
    proc option  | content
    -------------|----------------------------
    outfile=".." | the path of the output file
    dbms=..      | csv, tab, dlm, xlsx

- LIBNAME + DATA STEP
  - exporting data to an excel
    ```sas
    ***********************************************************;
    *  Exporting Data to an Excel Workbook                    *;
    ***********************************************************;
    *  Syntax and Example                                     *;
    *                                                         *;
    *    LIBNAME libref XLSX "path/file.xlsx";                *;
    *      <use libref for output table(s)>                   *;
    *    LIBNAME libref CLEAR;                                *;
    ***********************************************************;

    /*设置原有的xlsx表格作为新的逻辑库myxl*/
    libname myxl xlsx "&outpath/cars.xlsx"; 
    /*在myxl中新建名为asiacars的表格页*/
    data myxl.asiacars;
      /*复制sashelp中的cars表格作为上述新的表格*/
      set sashep.cars;
      /*筛选origin变量的值为Asia的个案*/
      where origin='Asia';
    run;
    /*删除myxl*/
    libname myxl clear;
    ```

  - exporting data to a csv (similar to xlsx)
      ```sas
    LIBNAME libref csv "path/file.csv";
    <use libref for output table(s)>
    LIBNAME libref CLEAR;                 
    ```
  - exporting data to a text
    ```sas
    LIBNAME libref tab "path/file.txt";
    <use libref for output table(s)>
    LIBNAME libref CLEAR;                 
    ```



<a id="markdown-62-exporting-results---exporting-reports" name="62-exporting-results---exporting-reports"></a>
## 6.2. Exporting Results - Exporting reports
- Output Delivery System
  ```sas
  ODS <destination> <specifications>;
  /*sas code that produces output*/
  ODS <destination> close;
  ``` 

  - Exporting Results to CSV
    ```sas
    ods csvall file="...";
    <!-- proc -->
    ods csvall close;
    ```
  - Exporting Results to Excel
    ```sas
    ***********************************************************;
    *  Exporting Results to Excel                             *;
    ***********************************************************;
    *  Syntax and Example                                     *;
    *                                                         *;
    *    ODS EXCEL FILE="filename.xlsx" <STYLE=style>         *;
    *              <OPTIONS (SHEET_NAME='label')>;            *;
    *        /* SAS code that produces output */              *;
    *    ODS EXCEL OPTIONS (SHEET_NAME='label');              *;
    *        /* SAS code that produces output */              *;
    *    ODS EXCEL CLOSE;                                     *;
    ***********************************************************;
    ```
    ods option                   | meaning
    -----------------------------|--------
    OPTIONS (SHEET_NAME='label') | 表格页名称
    STYLE=style                  | proc template;</p>list styles;</p>run;</p>（查询styles）

  - Exporting Results to PowerPoint 
      ```sas
      ods powerpoint file="..." style=...;
      <!-- proc -->
      ods powerpoint close;
      ```
  - Exporting Results to Microsoft Word(rich text format )
    ```sas
    ods rtf file="..." startpage=no;/*startpage=no means no new page are inserted before each procedure*/
    <!-- proc -->
    ods rtf close;
    ```

  - Exporting Results to PDF
    ```sas
    ***********************************************************;
    *  Exporting Results to PDF                               *;
    ***********************************************************;
    *  Syntax                                                 *;
    *                                                         *;
    *    ODS PDF FILE="filename.xlsx" STYLE=style             *;
    *            STARTPAGE=NO PDFTOC=1;                       *;
    *    ODS PROCLABEL "label";                               *;
    *        /* SAS code that produces output */              *;
    *    ODS PDF CLOSE;                                       *;
    ***********************************************************;
    ods pdf file="..." startpage=no pdftoc=n;/*pdftoc=n controls the level of the bookmarks that are open*/
    ods proclabel"label";/*ods proclabel"label" label the bookmark for procedure*/
    <!-- proc -->
    ods pdf close;
    ```

<a id="markdown-63-structured-query-languagesql-in-sas" name="63-structured-query-languagesql-in-sas"></a>
## 6.3. Structured Query Language(SQL) in SAS
SQL
- used to
  - prepare data
  - analyze and report data
- provide an alternative paradigm: processing and reporting on tabular data
- advantages
  - to query, manipualte and report on tables 
  - available in SAS as PROC SQL
  - alternative to DATA step and some PROC steps

<a id="markdown-631-sql-basic-syntax---proc-sql" name="631-sql-basic-syntax---proc-sql"></a>
### 6.3.1. SQL basic syntax - PROC SQL

```sas
****************************
*PROC SQL;                 *
*  SELECT clause           *
*   FROM clause            *
*     <WHERE clause>       *
*       <ORDER BY clause (desc)>; *
*QUIT;                     *
****************************;
proc sql;
  select name, age, height*2.54 as heightcm format=5.1, birthday format=date9.
    from pg1.class_birthdate;
quit;
```
<a id="markdown-632-filter-and-sort-data" name="632-filter-and-sort-data"></a>
### 6.3.2. filter and sort data
```sas
***********************************************************;
*  Reading and Filtering Data with SQL                    *;
***********************************************************;
*  Syntax and Example                                     *;
*                                                         *;
*    PROC SQL;                                            *;
*        SELECT col-name, col-name FORMAT=fmt             *;
*        FROM input-table                                 *;
*        WHERE expression                                 *;
*        ORDER BY col-name <DESC>;                        *;
*    QUIT;                                                *;
*                                                         *;
*    New column in SELECT list:                           *;
*    expression AS col-name                               *;
***********************************************************;
proc sql;
  select * /* * means all columns and all rows */
    from pg1.storm_final;
quit;


proc sql;
*Add SELECT statement;
	select Season, propcase(Name) as name, StartDate format=mmddyy10., MaxWindMPH
		from pg1.storm_final
	where maxwindmph > 156 and season > 2000
	order by maxwindmph desc, name;
quit;
```

<a id="markdown-633-create-and-delete-tables-in-sql" name="633-create-and-delete-tables-in-sql"></a>
### 6.3.3. create and delete tables in SQL
  - create...
  ```sas
  PROC SQL;
  CREATE TABLE table-name AS   /* create part is prior to those below*/
    SELECT ...
      FROM ...;
  QUIT;
  ```
  - delete...
  ```sas
  PROC SQL;
    DROP TABLE table-name;
  QUIT;
  ```
  - practice
  ```sas
  ***********************************************************;
  *  Activity 7.03                                          *;
  *    1) Modify the query to create a temporary table      *;
  *       named TOP_DAMAGE.                                 *;
  *    2) Add an additional query in the same PROC SQL step *;
  *       to generate a report that lists all the columns   *;
  *       for the first 10 storms in the top_damage table.  *;
  *    3) Add a TITLE statement before the second query to  *;
  *       display the following text: Top 10 Storms by      *;
  *       Damage Cost.                                      *;
  *    4) How many of the top 10 storms occurred in 2005?   *;
  ***********************************************************;
  *Two ways to query top n in a variable*;
  **************;
  * 1st answer *;
  **************;
  proc sql;
  *Modify the query to create a table;
  create table top_damage as
  select Event, Date format=monyy7., Cost format=dollar16., monotonic() as id
      from pg1.storm_damage
      order by Cost desc;
      *Add a title and query to create a top 10 report;
      title "Top 10 Storms by Damage Cost";
      select Event, Date format=monyy7., Cost format=dollar16.
        from TOP_DAMAGE
      where id<11;
  quit;
  title;

  **************;
  * 2nd answer *;
  **************;
  proc sql;
  create table top_damage as
  select Event, 
        Date format=monyy7.,
        Cost format=dollar16.
        from pg1.storm_damage
        order by Cost desc;
  title "Top 10 Storms by Damage Cost";
      select *
          from top_damage(obs=10);
  quit;
  ```

<a id="markdown-634-join-tables" name="634-join-tables"></a>
### 6.3.4. join tables

compare two ways to join tables
meanings              | data step | proc sql
----------------------|-----------|-----------
increase variables    | merge     | inner join
increase observations | set       | -
-                     | -         | left join
-                     | -         | outer join
-                     | -         | right join

```sas
***********************************************************;
*  Joining Tables with PROC SQL                           *;
***********************************************************;
*  Syntax and Example                                     *;
*                                                         *;
*    PROC SQL;                                            *;
*        SELECT col-name, col-name                        *;
*        FROM input-table1 INNER JOIN input-table2        *;
*        ON table1.col-name=table2.col-name;              *;
*    QUIT;                                                *;
***********************************************************;
PROC SQL;
SELECT grade, age, teacher, class_update.name 
/*qualifying column name 当多个table中存在相同的变量名时，使用此table的变量名*/
  FROM pg1.class_update INNER JOIN pg1.class_teacher
    ON class_update.name = class_teacher.name;
QUIT;
*****************;
* using aliases **********************;
* table-name ==> table-name AS alias **********************;
***********************************************************;
*  Syntax                                                 *;
*     FROM table1 AS alias1 INNER JOIN table2 AS alias2   *;
*     ON alias1.column = alias2.column                    *;
***********************************************************;
PROC SQL;
SELECT grade, age, teacher, class_update.name 
  FROM pg1.class_update AS u INNER JOIN pg1.class_teacher AS t
    ON u.name = t.name;
QUIT;
```



[Contents](#jump)
