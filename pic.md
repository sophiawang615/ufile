# 增值服务

{{indexmenu_n>5}}

## 海外专线服务

对于在海内外都有UFile上传、下载业务需求的客户，可以申请开通海外专线服务。

### 使用场景

#### 1、从国内访问海外地域的UFile Bucket

国内访问海外bucket时将解析到广州的IP，再通过UFile海外专线到海外的bucket进行上传下载处理，保障业务的稳定。

从国内访问香港地域bucket，开通海外专线服务即可。
访问海外其他地域的bucket，在申请开通海外专线服务时还需提交专线转发配置需求。

#### 2、从海外访问国内地域的UFile Bucket

海外访问国内bucket时将解析到香港的IP，再通过UFile海外专线到国内的bucket进行上传下载处理，保障业务的稳定。

从海外访问广州地域bucket，开通海外专线服务即可。
访问国内其他地域的bucket，在申请开通海外专线服务时还需提交专线转发配置需求。

### 开通方式

UFile海外专线服务默认关闭，需要开通的用户请提交工单申请。如需配置专线转发，请在工单中一并提交。

工单内容：bucket名称、地域、bucket绑定的自定义域名、专线转发方向(非必需)

PS：开通专线后。若新增的自定义域名需使用专线访问源站，请联系技术支持进行添加。

### 专线价格

海外专线服务收费请参考：[产品价格](https://docs.ucloud.cn/storage_cdn/ufile/bill) —
海外专线计费说明。

## 图片处理服务

图片处理服务是UCloud对外提供的海量、安全、低成本高可靠的图片处理服务。用户将原始图片上传保存在对象存储空间中，用户可以在任何时间、任何地点、任何设备上对图片进行处理。

图片处理服务仅在下载时触发。

图片处理服务提供以下功能：

1、基本图片信息获取

2、EXIF信息获取

3、图片缩放

4、图片裁剪

5、图片旋转

6、水印

7、图片格式转换

8、管道顺序调用多种图片处理功能

### 基本图片信息获取

图片基本信息包括图片格式、图片大小。

在图片下载URL后附加imageinfo指示符（区分大小写），即可获取JSON格式的图片基本信息。

| 参数名    | 值         | 解释  |
| ------ | --------- | --- |
| iopcmd | imageinfo | 主命令 |

### EXIF信息获取

EXIF（EXchangeable Image File
Format）是专门为数码相机的照片设定的可交换图像文件格式，通过在图片下载URL后附加exif指示符（区分大小写）获取。

注意：缩略图等经过处理的新图片不支持该方法。

| 参数名    | 值    | 解释  |
| ------ | ---- | --- |
| iopcmd | exif | 主命令 |

### 图片缩放

| 参数名     | 值            | 解释                                                                      |
| ------- | ------------ | ----------------------------------------------------------------------- |
| iopcmd  | thumbnail    | 主命令                                                                     |
| type    | 1            | 按比例缩放                                                                   |
| type    | 2            | 宽度不变,高度按百分比缩放                                                           |
| type    | 3            | 高度不变,宽度按百分比缩放                                                           |
| type    | 4            | 指定宽度 ,高度等比缩放                                                            |
| type    | 5            | 指定高度,宽度等比缩放                                                             |
| type    | 6            | widthXheight,限定长边，短边自适应缩放                                               |
| type    | 7            | widthXheight,限定短边，长边自适应缩放                                               |
| type    | 8            | widthXheight,指定高和宽的最小尺寸,等比缩放,如只指定高或宽,则未指定边按照指定数值进行裁剪.但是超出指定矩形会被居中裁剪     |
| type    | 9            | 以大的缩放比例进行等比缩放，缩放后可以小于指定的矩形，如高的缩放比例更大，以高为准等比缩放                           |
| type    | 10           | 以小的缩放比例进行等比缩放，缩放后可以大于指定的矩形, 如宽的缩放比例更小，以宽为准等比缩放                          |
| type    | 11           | 使用指定的宽和高，会导致图像拉伸                                                        |
| type    | 12           | 原图尺寸小于widthXheight目标尺寸，原图居中，四周补color颜色                                  |
| type    | 13           | 等比缩放，一边先缩到目标值，另一边居中裁剪，传widthXheight                                     |
| type    | 14           | 等比缩放，目标会小于等于widthXheight                                                |
| type    | 15           | 等比缩放，目标会等于widthXheight,不足的边，补color颜色                                    |
| color   | 十六进制或颜色名red等 |                                                                         |
| scale   | 最大10000      | 缩放百分比                                                                   |
| gifmode |              | 该参数只对gif图片有效。若不传，则该参数默认为1                                               |
| gifmode | 1            | 返回连续的图像帧，如果不能处理全部的图像帧则只返回部分，同3                                          |
| gifmode | 2            | 返回第一帧静态图片，图像格式仍为gif                                                     |
| gifmode | 3            | 在系统处理的超时时间内，返回连续的图像帧，如果不能处理全部的图像帧则只返回部分                                 |
| gifmode | 4            | 在系统处理的超时时间内，如果不能处理全部的图像帧，则返回部分跳跃的图像帧，图像帧平均分布                            |
| gifmode | 5            | 在系统处理的超时时间内，如果不能处理全部的图像帧，则返回部分跳跃的图像帧，图像帧平均分布，同时用前一帧填充跳跃的帧，保持处理前后总帧数数量不变 |
| gifmode | 6            | 在系统处理的超时时间内，如果不能处理全部的图像帧，则返回部分跳跃的图像帧，图像帧平均分布，同时修改图像帧的延迟时间，使播放速度和原图相同    |

### 图片裁剪

| 参数名     | 值                                                                    | 解释                         |
| ------- | -------------------------------------------------------------------- | -------------------------- |
| iopcmd  | crop                                                                 | 主命令                        |
| width   | 0-10000                                                              | 裁剪后宽度                      |
| height  | 0-10000                                                              | 裁剪后高度                      |
| ax      | 0-10000                                                              | 锚点 x 坐标                    |
| ay      | 0-10000                                                              | 锚点 y 坐标                    |
| gravity | NorthWest/North/NorthEast/West Center/East/SouthWest/South/SouthEast | 位置偏移指示符,可以和锚点同时指定(比锚点优先使用) |

### 图片旋转

| 参数名    | 值         | 解释        |
| ------ | --------- | --------- |
| iopcmd | rotate    | 主命令       |
| degree | \[0,360\] | 旋转度数(顺时针) |

### 水印

| 参数名         | 值                                                                    | 解释                                                                         |
| ----------- | -------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| iopcmd      | watermark                                                            | 主命令                                                                        |
| type        | 1=文字水印,2=图片水印                                                        | 水印类型                                                                       |
| gravity     | NorthWest/North/NorthEast/West Center/East/SouthWest/South/SouthEast | 位置偏移指示符,可以和锚点同时指定(比锚点优先使用)                                                 |
| opacity     | 1-100,缺省为100(完全不透明)                                                  | 透明度                                                                        |
| ax          | 小于原图宽度,默认为10                                                         | 锚点 x 坐标                                                                    |
| ay          | 小于原图高度,默认为10                                                         | 锚点 y 坐标                                                                    |
| text        |                                                                      | base64 URL encode 后的水印文字，支持 UTF-8。                                         |
| imageurl    |                                                                      | 可访问的图片资源URI，水印图片，必须是可以访问的资源地址，经过 base64 URL encode。                        |
| font        |                                                                      | base64 URL encode 后的字体名称                                                   |
| fontsize    | 1-100                                                                | 水印文字大小，缺省为10，字体大小。                                                         |
| direction   | 1=RightToLeft,2=LeftToRight                                          | 水印文字方向                                                                     |
| fill        |                                                                      | RGB 颜色编码表，base64 URL encode 后的RGB格式，可以是颜色名称（比如red）或十六进制（比如\#FF0000），缺省为白色。 |
| SimSun      |                                                                      | 宋体                                                                         |
| angle\_type | 1=左上角，2=右上角，3=右下角，4=左下角                                              | 九宫格中水印图片位置，默认为左上角。                                                         |

### 图片格式转换

| 参数名    | 值                | 解释                                                             |
| ------ | ---------------- | -------------------------------------------------------------- |
| iopcmd | convert          | 主命令                                                            |
| dst    | jpg/png/bmp/webp | 目标格式                                                           |
| Q      | 0-100            | 图片压缩质量（绝对压缩比），目标格式为jpg,webp时有效                                 |
| q      | 0-100            | 图片压缩质量（相对压缩比），即在图片原有压缩基础上按此比例进行压缩，目标格式为jpg,webp时有效，Q与q同时出现时，取Q |
| fr     | 0.0-1.0          | 需要格式转换的图像帧在图像总帧中的位置，默认为0.0                                     |

### 管道顺序调用多种图片处理功能

管道顺序是一种可以实现多种图片处理任务顺序执行的机制。用户可以通过管道顺序在一次下载时中按照顺序完成对图像的不同处理。

如：

<blockquote>
<code>
http://demobucket.ufile.ucloud.com.cn/here-for-example.jpg?iopcmd=rotate&degree=180|iopcmd=thumbnail&type=1&scale=40
</code></blockquote>

上述请求会将demobucket这个空间中的here-for-example.jpg文件先旋转180度，然后按比例缩放为原来的40%大小。

注意：如果请求当前不支持的iopcmd，则会报错，不会返回原图。
