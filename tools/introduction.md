{{indexmenu_n>1}}

# 管理工具

## 空间管理

空间管理工具可帮助用户获取存储相关信息并进行空间管理，支持创建存储空间、删除存储空间、存储空间信息查看与修改和存储空间文件列表查询。

### 下载链接

[bucketmgr-win32](http://tools.ufile.ucloud.com.cn/bucketmgr-win32.zip)

[bucketmgr-win64](http://tools.ufile.ucloud.com.cn/bucketmgr-win64.zip)

[bucketmgr-linux64](http://tools.ufile.ucloud.com.cn/bucketmgr-linux64.tar.gz)

[bucketmgr-mac](http://tools.ufile.ucloud.com.cn/bucketmgr-mac.tar.gz)

### 使用说明

Linux/Mac用户请在terminal执行，Windows用户请在cmd终端执行。使用前请修改当前目录下的配置文件config.cfg，把API密钥加入到配置项：

```
{
   "public_key" : "paste your public key here",
   "private_key" : "paste your private key here",
   "api_host" : "api.spark.ucloud.cn"  
}
```

注：

API密钥可以在控制台的“API密钥”页面获得。将public\_key和private\_key分别填入config.cfg文件的对应位置，客户端工具通过此密钥完成鉴权。请妥善保管好API密钥，避免泄露。

#### 创建存储空间

创建存储空间建议使用控制台。

```
./bucketmgr --action CreateBucket --bucket bucketname --type public --region region --project-id project-id
参数说明:
--bucket: 需要创建的存储空间名
--type: 需要创建的空间类型，公开空间（public）或私有空间（private）
--region: 需要创建的存储空间所属地区，默认北京
--project-id: 需要创建的空间所属项目组ID
```

示例：

在org-mutvtj项目下创建uclouddemo存储空间：

```
./bucketmgr --action CreateBucket --bucket uclouddemo --type public --region cn-bj --project-id org-mutvtj
```

#### 删除存储空间

删除存储空间建议使用控制台。

```
./bucketmgr --action DeleteBucket --bucket bucketname --project-id project-id
参数说明:
--bucket: 需要删除的存储空间名
--project-id: 需要删除的空间所属项目组ID
```

#### 获取空间信息

```
./bucketmgr --action DescribeBucket --project-id project-id
参数说明:
--bucket: 需要查询的存储空间名
--project-id: 需要获取的空间所属项目组ID
```

#### 获取文件列表

```
./bucketmgr --action GetFileList --bucket bucketname --limit limit --pattern pattern --format format
参数说明:
--bucket: 需要拉取列表的存储空间名
--limit : 需要查询的记录数（默认取全部）
--pattern: 需要查询记录的模板，支持POSIX正则表达式
--format: 格式化查询记录
```

## 文件管理

文件管理工具可帮助用户进行存储空间内文件的管理操作，包括：

1、上传单个文件：普通上传（PUT），秒传（UPLOAD-HIT），分片上传（MPUT），表单方式上传。

2、上传文件夹：普通上传（PUT），分片上传（MPUT），增量上传（SYNC）。

3、下载文件/文件夹：普通下载（DOWNLOAD）, 分片下载（MDOWNLOAD）, 批量下载（BATCH-DOWNLOAD）

4、删除文件/文件夹: 普通删除（DELETE）, 批量删除（BATCH-DELETE）

5、计算etag（ETAG）

6、检查文件是否存在（CHECK）

7、获取文件url（FETCHURL）

8、拉取文件列表（GETFILELIST）

### 下载链接

[filemgr-win32](http://tools.ufile.ucloud.com.cn/filemgr-win32.zip)

[filemgr-win64](http://tools.ufile.ucloud.com.cn/filemgr-win64.zip)

[filemgr-linux64](http://tools.ufile.ucloud.com.cn/filemgr-linux64.tar.gz)

[filemgr-mac](http://tools.ufile.ucloud.com.cn/filemgr-mac.tar.gz)

<WRAP center round important 60%>
普通上传（PUT）、表单上传方式、秒传文件（UPLOAD-HIT）的文件大小不能超过
1GB，要上传大小超过 1GB 的文件必须使用分片上传（MPUT）方式。 </WRAP>

### 使用说明

该工具用于在命令行做上传/下载/删除等针对文件的操作，如果有需要动态上传文件的场景，请使用API进行内容管理操作。
上传超过100MB大小的文件，网络条件较差，和UFile的服务器之间的连接经常断开的场景请使用工具中的分片上传（MPUT）。
使用前请修改当前目录下的配置文件config.cfg，把API密钥加入到配置项：

```
{
   "public_key" : "paste your public key here",
   "private_key" : "paste your private key here",
   "proxy_host" : "www.cn-bj.ufileos.com",
   "api_host" : "api.spark.ucloud.cn"
}
```

不同地域的proxy\_host是不一样的，具体如下:

```
北京
外网：www.cn-bj.ufileos.com 
B机房内网：www.ufile.cn-north-02.ucloud.cn
C机房内网: www.ufile.cn-north-03.ucloud.cn
D机房内网: www.ufile.cn-north-04.ucloud.cn
上海二
外网: www.cn-sh2.ufileos.com
内网: www.internal-cn-sh2-01.ufileos.com
香港
外网：www.hk.ufileos.com
内网：www.internal-hk-01.ufileos.com
广东
外网：www.cn-gd.ufileos.com
内网：www.internal-cn-gd-02.ufileos.com
美国
外网：www.us-ca.ufileos.com
内网：www.internal-us-ca-01.ufileos.com
雅加达
外网：www.idn-jakarta.ufileos.com
内网：www.internal-idn-jakarta-01.ufileos.com
新加坡
外网：www.sg.ufileos.com
内网：www.internal-sg-01.ufileos.com
尼日利亚：
外网：www.afr-nigeria.ufileos.com
内网：www.internal-afr-nigeria.ufileos.com
台北：
外网：www.tw-tp.ufileos.com
内网:www.internal-tw-tp.ufileos.com
圣保罗：
外网：www.bra-saopaulo.ufileos.com 
内网：www.internal-bra-saopaulo.ufileos.com
迪拜：
外网：www.uae-dubai.ufileos.com
内网：www.internal-uae-dubai.ufileos.com
越南：
外网：www.vn-sng.ufileos.com
内网：www.internal-vn-sng.ufileos.com
孟买：
外网：www.ind-mumbai.ufileos.com
内网：www.internal-ind-mumbai.ufileos.com
全球化
外网：<bucket_name>.up.ufileos.com
```

API密钥可以在控制台的“API密钥”页面获得。将public\_key和private\_key分别填入config.cfg文件的对应位置，客户端工具通过此密钥完成鉴权。请妥善保管好API密钥，避免泄露。

对于命令行工具，Linux/Mac用户请在terminal执行，Windows用户请在cmd终端执行。  
注：当工具在后台执行时，请加上参数 `--nobar=true`

#### 分片上传单个文件

当文件较大时请使用分片上传，分片上传允许在某个分片失败情况下进行续传，并且可以多个分片并发上传，适合较大文件的场景。

```
./filemgr --action mput --bucket demobucket --key key --file filename [--threads threads] [--retrycount retrycount] [--speedlimit speedlimit]
参数说明:
   --bucket: 需要上传至的 bucket 名称         
   --key: 上传至 bucket 中的文件名称--file : 需要上传的本地文件路径       
   --file: 需要上传的本地文件路径
   --threads: 分片上传并发数，默认为5
   --retrycount: 分片上传失败重试次数，默认10，大文件上传建议配置大些
   --speedlimit: 上传限速，单位bytes/s 
   --storageclass: 文件存储类型，分别是标准、低频、归档，对应有效值：STANDARD, IA, ARCHIVE； 文件默认类型，继承于Bucket默认类型。（Bucket默认类型为STANDARD）
```

示例：

以分片上传方式上传一个本地文件 hello.avi 至名为 demobucket 的存储空间中并且命名为 world.avi：

```
./filemgr --action mput --bucket demobucket --key world.avi --file /opt/video/hello.avi --threads 10 --retrycount 20  --speedlimit 1024
```

注：

filemgr支持对分片上传失败的文件进行自动续传，只需要在执行失败时重新执行命令即可。只能运行单个进程，多进程会导致上传失败。如需并发上传，请选择目录上传或者增量上传。

#### 分片上传文件夹

对于文件夹中大文件较多的情况分片上传文件夹相比普通上传文件夹要快。

```
./filemgr --action mput --bucket demobucket  --dir localdir [--threads threads] [--trimpath trimpath] [--prefix prefix] [--retrycount retrycount] [--speedlimit speedlimit]       
 参数说明:           
   --bucket: 需要上传至的 bucket 名称         
   --dir: 需要上传的本地文件夹
   --threads: 分片上传并发数，默认为5
   --trimpath: 截掉绝对路径的部分路径
   --prefix: 生成文件的Key时使用的前缀，指定该参数时生成的Key是 prefix+base（filename）
   --retrycount: 分片上传失败重试次数，默认10，大文件上传建议配置大些
   --speedlimit: 上传限速，单位bytes/s
   --storageclass: 文件存储类型，分别是标准、低频、归档，对应有效值：STANDARD, IA, ARCHIVE； 文件默认类型，继承于Bucket默认类型。（Bucket默认类型为STANDARD）
```

注：

只能运行单个进程，多进程会导致上传失败。

#### 普通上传单个文件(大于4M文件请使用上述分片上传)

```
./filemgr --action put --bucket bucketname --key key --file filename [--speedlimit speedlimit]
参数说明:
  --bucket: 需要上传至的存储空间
  --key: 上传至存储空间中的文件名
  --file: 需要上传的本地文件路径
  --speedlimit: 上传限速，单位bytes/s 
  --storageclass: 文件存储类型，分别是标准、低频、归档，对应有效值：STANDARD, IA, ARCHIVE； 文件默认类型，继承于Bucket默认类型。（Bucket默认类型为STANDARD）
```

示例：

把一个本地文件 ucloud.jpg 上传至名称为 uclouddemo 的bucket中，并命名为 logo.jpg ：

```
./filemgr --action put --bucket uclouddemo --key logo.jpg --file /home/yours/pictures/ucloud.jpg
```

#### 普通上传文件夹

```
./filemgr --action put --bucket bucketname --dir dirname [--trimpath trimpath] [--prefix prefix] [--speedlimit speedlimit]
参数说明:
   --bucket: 需要上传至的存储空间名
   --dir: 需要上传的本地文件夹
   --trimpath: 截掉绝对路径的部分前缀
   --prefix: 生成文件的Key时使用的前缀，指定该参数时生成的Key是 prefix+base（filename）
   --speedlimit: 上传限速，单位bytes/s
   --storageclass: 文件存储类型，分别是标准、低频、归档，对应有效值：STANDARD, IA, ARCHIVE； 文件默认类型，继承于Bucket默认类型。（Bucket默认类型为STANDARD）
```

用文件夹方式上传的文件默认会使用文件夹内文件所在的绝对路径来命名Key，如果想指定特殊的前缀请使用--prefix参数。

示例1: 将 $HOME/files 这个文件夹下的所有文件上传至名为 demobucket 的存储空间中，并且 key 的名称使用 demo/
作为前缀

如果该文件夹下有一个名为1.jpg
的文件并且空间属性为public，则上传完成后可以通过 <http://demobucket.ufile.ucloud.com.cn/demo/1.jpg> 访问该文件

```
./filemgr --action put --dir ~/files --bucket demobucket --prefix demo/
```

如果您不希望使用绝对路径来作为Key，可以使用--trimpath截掉部分路径名。如下：

```
./filemgr --action put --dir ~/files --bucket demobucket --prefix demo/ --trimpath /root/test
```

示例2:

假设有个目录名为 /some/dir/cutoff/files/，下面有 a.jpg、b.txt两个文件，则以下的处理会使得保存在 UFILE
的文件名为 files/a.jpg、files/b.txt。

```
./filemgr --action put --dir ~/files --bucket demobucket --trimpath /some/dir/cutoff/
```

#### 增量上传

增量上传仅上传新增或有发生修改的整个文件。

```
./filemgr --action sync --bucket demobucket --dir syncdir [--speedlimit speedlimit] [--prefix prefix] [--excludeptn pattern] [--includeptn pattern]
 参数说明:           
   --bucket : 需要同步至远端的 bucket 名称
   --dir    : 需要同步的本地文件夹
   --threads : 上传并发数
   --speedlimit : 上传限速(byte/s)
   --prefix : 生成文件的 key 时使用的前缀
   --excludeptn: 需要排除上传的文件模式，支持 POSIX 正则表达式
   --includeptn: 需要包含上传的文件模式，支持 POSIX 正则表达式
```

示例：

```
把本地文件夹${HOME}/go 同步到名为 demobucket 的存储空间中
> $./filemgr --action sync --bucket demobucket --dir ~/go
Syncing...
Sync Successed[ src/pkg/math/sqrt_amd64.s ] => demobucket : src/pkg/math/sqrt_amd64.s
Sync Successed[ src/lib9/fmt/dofmt.c ] => demobucket : src/lib9/fmt/dofmt.c
Sync Successed[ src/pkg/runtime/runtime_linux_test.go ] => demobucket : src/pkg/runtime/runtime_linux_test.go
...
...
(忽略中间输出)
...
...

结果如下

|total|succ|fail|
|4556 |4556| 0  |

继续检查是否还有文件需要更新
$./filemgr --action sync --bucket demobucket --dir ~/go
```

注：

只能运行单个进程，多进程会导致上传失败。

#### 秒传文件

```
./filemgr --action upload-hit --bucket demobucket --key key --file filename
参数说明:
  --bucket: 需要上传至的 bucket 名称
  --key : 上传至 bucket 中的文件名称
  --file : 需要上传的本地文件路径
```

示例:

尝试秒传本地文件 falcon.avi 至存储空间 nfl2014 命名为 2014-superbow.avi

```
./filemgr --action upload-hit --bucket demobucket --key 2014-superbow.avi --file falcon.avi
```

#### 普通下载单个文件

```
./filemgr --action download --bucket demobucket --key key --file filename
参数说明:
  --bucket : 需要下载的文件所在的 bucket 名称
  --key : 需要下载的文件 key 名称
  --file : 需要保存在本地的文件路径
  --speedlimit: 下载限速，单位bytes/s
```

示例:

获取一个名为 demobucket 的存储空间中一个名为ucloud.png的文件并且保存为/opt/data/ucloud.png

```
./filemgr --action download --bucket demobucket --key ucloud.png --file /opt/data/ucloud.png
```

#### 分片下载单个文件(适合大文件下载)

```
./filemgr --action mdownload --bucket demobucket --key key --file filename [--threads threads] [--retrycount retrycount] [--speedlimit speedlimit]
参数说明:
  --bucket : 需要下载的文件所在的 bucket 名称
  --key : 需要下载的文件 key 名称
  --file : 需要保存在本地的文件路径
  --threads: 分片下载并发数，默认为5
  --retrycount: 分片下载失败重试次数，默认10，大文件上传建议配置大些
  --speedlimit: 下载限速，单位bytes/s
```

注：

只能运行单个进程，多进程会导致下载失败。如需并发下载，请选择批量下载。

#### 批量下载

```
./filemgr --action batch-download --bucket demobucket --pattern pattern --dir localdir [--threads threads] [--speedlimit speedlimit]
参数说明:
  --bucket : 需要下载的文件所在的 bucket 名称
  --pattern : 需要下载的文件模板，支持POSIX正则表达式
  --dir : 需要保存在本地的文件目录
  --threads: 下载并发数，默认为5
  --speedlimit: 下载限速，单位bytes/s
```

注：

只能运行单个进程，多进程会导致下载失败。

#### 删除文件

```
./filemgr --action delete --bucket demobucket --key key
参数说明:
--bucket: 需要删除的文件所在的 bucket 名称
--key : 需要删除的文件在 bucket 中的名称
```

示例:

删除一个名为 demobucket 的存储空间中名为 20140201.blog 的文件

```
./filemgr --action delete --bucket demobucket --key 20140201.blog
```

#### 批量删除

```
./filemgr --action batch-delete --bucket demobucket --pattern pattern
参数说明:
  --bucket : 需要删除的文件所在的 bucket 名称
  --pattern : 需要删除的文件模板，支持POSIX正则表达式
```

#### 计算文件ETag

该选项用于计算使用ufile特殊算法得到的文件哈希值

```
./filemgr --action etag --file filename
参数说明:
--file: 需要计算哈希的本地文件路径
```

示例：

计算本地文件 sniff-the-rose.pdf 的 ETag：

```
./filemgr --action etag --file /opt/tiger/sniff-the-rose.pdf
```

#### 检查文件

该选项用于检查文件是否存在于ufile对应空间

```
./filemgr --action check --bucket bucketname --key key
参数说明:
  --bucket: 需要检查的文件所在的 bucket 名称
  --key: 需要检查的文件名
```

#### 获取文件URL

该选项用于获取文件的URL

```
./filemgr --action fetchurl --bucket bucketname --key key --method method [--expires expires]
参数说明:
  --bucket: 需要检查的文件所在的 bucket 名称
  --key: 需要获取url的文件名
  --method: 需要获取url的请求方式（GET或者HEAD）
  --expires: url使用的过期时间点（时间戳）
```

示例：

获取一个名为 demobucket 的存储空间中一个名为 QQ.pkg 的文件在5分钟内的有效下载 URL ：

```
./filemgr --action fetchurl --bucket demobucket --key QQ.pkg --method get --expires 300
URL为：
http://demobucket.ufile.ucloud.com.cn/QQ.pkg%3DUCloudPublicKey%3Ducloudtesting%40ucloud.cn13998635452068156091%26Signature%3DjFQFLtoAUhgOodpvfu8uLUDnzLg%3D%26Expires%3D1420010439
```

#### 获取文件列表

该选项用于获取ufile存储空间的文件列表

```
./filemgr --action getfilelist --bucket bucketname [--limit limit] [--marker marker] [--prefix prefix] [--pattern pattern] [--format format]
参数说明:
  --bucket: 需要检查的文件所在的 bucket 名称
  --limit: 需要获取文件列表的数量，默认获取全部
  --marker: 需要获取文件列表的标记点
  --prefix: 获取对应前缀的文件列表
  --pattern: 需要获取文件列表的模板，支持POSIX正则表达式
  --format: 格式化输出的文件格式
```

#### filemgr版本更新

该选项用于更新工具版本

```
./filemgr --update
```
