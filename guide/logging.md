# 日志管理

{{indexmenu_n>4}}

## 设置日志存储

用户在访问UFile文件时，会产生大量的访问日志，为了方便用户查询，可以开启日志管理功能。开启功能后该空间的访问日志，会以小时为单位，按照固定的命名，存储到用户指定的空间中。  
选择对应空间，在右侧操作中点击日志管理按钮  
![](/images/guide/进入日志管理界面.png)

点击开启\[日志存储功能\]按钮  
![](/images/guide/开启日志存储功能.png)

选择日志存储空间和填写日志前缀，日志存储空间默认为当前空间，日志前缀默认"ufile-log/"，前缀可以为空。  
例：填写前缀为"ufile-log/2019/"，日志生成后将被存储在该填写的目录下。  

## 日志命名规则

\<TargetPrefix\>\<SourceBucket\>-YYYY-mm-DD-HH-UniqueString  
命名规则中:  
TargetPrefix由用户指定，表示存储访问日志记录的名称前缀，可以为空。  
YYYY-mm-DD-HH-分别是该日志被创建时的阿拉伯数字的年、月、日、小时。  
UniqueString为系统生成的8位字符串，用于唯一标识该Log文件。  
存储空间访问日志的名称例子如下：  
ufile-log/SourceBucket-2018-10-22-08-00000000
