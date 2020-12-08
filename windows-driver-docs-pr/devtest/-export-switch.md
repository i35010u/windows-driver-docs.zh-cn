---
title: /Export 开关
description: 增强的存储证书管理工具的/Export 开关将指定的证书从身份验证接收器证书 (ASC) 存储导出到文件
keywords:
- /Export 交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /Export
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 816c0ade00eb04e0a8c8764ddd05a71314d5be3a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785243"
---
# <a name="export-switch"></a>/Export 开关


增强的存储证书管理工具的 **/export** 开关将指定的证书从身份验证接收器证书（ (ASC) 存储区1667中的 ASC 存储）导出到文件。 此开关还支持将 (CSR) 的证书签名请求导出到文件。

**注意**  在本主题中，指定的与 IEEE 1667 兼容的 USB 存储设备称为 *目标设备*。

 

```
    EhStorCertMgrCmd
    /Export
     -Volume:
    VolumeName  -Path:PathToFile [-Certificate  -Index:IndexValue [-NoType]] [-Request]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span>**-Volume：**   
目标设备的卷名。 有关此参数的格式的详细信息，请参阅 [增强的存储证书管理工具概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**注意**  要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令提示符下键入 **EhStorCertMgrCmd/list** ，然后按 enter。

 

<span id="_______-Path______"></span><span id="_______-path______"></span><span id="_______-PATH______"></span>**-路径**   
将包含导出的证书或 CSR 的文件的完整路径和名称。

<span id="_______-Certificate_______"></span><span id="_______-certificate_______"></span><span id="_______-CERTIFICATE_______"></span>**-Certificate：**   
此开关指定请求导出证书。 以下开关与此类请求一起使用：

<span id="-Index"></span><span id="-index"></span><span id="-INDEX"></span>**-Index**  
ASC 存储中的索引，将从目标设备导出证书。 此开关是必需的。

<span id="-NoType"></span><span id="-notype"></span><span id="-NOTYPE"></span>**-NoType**  
如果指定此参数，则该工具不会将证书类型附加到使用 **-Path** 参数指定的文件名。

此开关是可选的，并且必须仅与 **-Certificate** 参数一起使用。

<span id="_______-Request______"></span><span id="_______-request______"></span><span id="_______-REQUEST______"></span>**-请求**   
此开关指定请求导出 CSR。 通常会将 CSR 发送到证书颁发机构 (CA) 为目标设备创建 ASC 主机 (ASCh) 证书。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

如果请求从设备的 ASC 存储中导出证书，则必须指定索引。 如果指定的索引不包含证书，则该工具将报告错误。

如果指定 **-certificate** 参数，则该工具会自动将表示证书类型的字符串追加到通过 **-Path** 参数指定的文件名。 下表定义了各种证书类型的字符串：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">证书类型字符串</th>
<th align="left">描述</th>
<th align="left">索引</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>"ASCm"</p></td>
<td align="left"><p>身份验证接收器证书 (ASC) 制造商。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>"ASCh"</p></td>
<td align="left"><p>用于向主机验证证书身份验证接收器的 ASC 主机证书。</p></td>
<td align="left"><p>大于1的任何索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"HCh"</p></td>
<td align="left"><p>用于向证书身份验证接收器验证主机的主机证书。</p></td>
<td align="left"><p>大于1的任何索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PCp</p></td>
<td align="left"><p>在管理命令序列中用于预配和管理证书身份验证接收器的设置证书。</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Sch-m</p></td>
<td align="left"><p>用于定义主机信任的证书的签名者证书。 此可信证书是 ASCh 证书的链和零个或多个 Sch-m 证书。</p></td>
<td align="left"><p>大于1的任何索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p>无效</p></td>
<td align="left"><p>位于指定索引处的证书类型未知。</p></td>
<td align="left"><p>不适用</p></td>
</tr>
</tbody>
</table>

 

例如，以下从目标设备导出 PCp 证书的命令将生成一个名为 c： \\ MyCertificates myCertPCp 的文件 \\ ：

```
EhStorCertMgrCmd /export -Certificate -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:1 -Path:c:\MyCertificates\myCert.cer
```

如果使用 **-Certificate** 参数指定 **-NoType** 参数，则该工具不会将证书类型的字符串追加到通过 **-Path** 参数指定的文件名。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何从目标设备中的 ASC 存储区导出索引1处的证书：

```
EhStorCertMgrCmd /export -Certificate -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:1 -Path:c:\MyCertificates\myCert.cer
```

 

 

