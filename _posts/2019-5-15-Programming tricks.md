---
layout: post
title: Programming tricks
---


- grep a list of sites against a large file

**Input**  
```
$ cat pos_list.txt  
pos1  
pos2  
posN  

$ head -n test.vcf
chr pos1 info...  
chr pos2 info...  
chr pos3 info...  
chr pos4 info...  
...
chr pos(N-1) info...  
chr posN info...  

```


```
awk 'FNR==NR {hash[$1]; next} $2 in hash' pos_list.txt test.vcf > match.vcf
# FNR: 浏览文件的记录数，NR: 已读的记录数， **二者区别在于awk每读入一个新文件时，FNR会对当前行数从0开始重新计数，而NR的行数则累计**。`FNR==NR`为真时，判断当前读入的是第一个文件，为假时判断读入了第二个文件。
# hash[$1]将pos_list.txt文件的每行记录都存入数组hash，并使用$1第一个字段作为下标引用。
# `$2 in hash`用于判断test.vcf文件的第二个字段是否和hash数组的字段匹配，匹配的结果存入match.vcf。  
```

**Output**  
```
$ cat match.vcf
chr pos1 info...  
chr pos2 info...  
chr posN info...  
```
