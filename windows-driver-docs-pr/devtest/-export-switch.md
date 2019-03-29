---
title: /Export 开关
description: 增强型存储证书管理工具的 /Export 开关将身份验证接收器证书 (ASC) 存储中指定的证书导出到文件
ms.assetid: 00612a63-057a-4ff9-baef-d44de0280cb5
keywords:
- /Export 开关驱动程序开发工具
topic_type:
- apiref
api_name:
- /Export
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47737642b2140960f35982b761febda96d9da59a
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463809"
---
# <a name="export-switch"></a>/Export 开关


**/Export**增强存储证书管理工具的开关将 IEEE 1667 合规的 USB 存储设备中的身份验证接收器证书 (ASC) 存储中指定的证书导出到文件。 此开关也支持证书签名请求 (CSR) 文件的导出。

**请注意**在本主题中，指定的 IEEE 1667 合规 USB 存储设备称为*目标设备*。

 

```
    EhStorCertMgrCmd
    /Export
     -Volume:
    VolumeName  -Path:PathToFile [-Certificate  -Index:IndexValue [-NoType]] [-Request]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-卷：**   
目标设备的卷名称。 此参数的格式的详细信息，请参阅[增强存储证书管理工具的概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**请注意**若要生成的 IEEE 1667 合规 USB 存储设备的当前连接到计算机的卷名称的列表，请键入**EhStorCertMgrCmd /List**在命令提示符，然后按 Enter。

 

<span id="_______-Path______"></span><span id="_______-path______"></span><span id="_______-PATH______"></span> **-Path**   
完整路径和将包含导出的证书或 CSR 文件的名称。

<span id="_______-Certificate_______"></span><span id="_______-certificate_______"></span><span id="_______-CERTIFICATE_______"></span> **-Certificate:**   
此开关指定请求的导出的证书。 与此类型的请求使用以下开关：

<span id="-Index"></span><span id="-index"></span><span id="-INDEX"></span>**-Index**  
该证书从目标设备的导出的 ASC 存储区中的索引。 此开关是必需的。

<span id="-NoType"></span><span id="-notype"></span><span id="-NOTYPE"></span>**-NoType**  
如果指定此参数，则该工具不将证书类型附加到使用指定的文件名称 **-路径**参数。

此开关是可选的必须仅可用于 **-证书**参数。

<span id="_______-Request______"></span><span id="_______-request______"></span><span id="_______-REQUEST______"></span> **-Request**   
此开关指定请求的导出的 CSR。 CSR 通常发送到创建的目标设备的 ASC 主机 (ASCh) 证书的证书颁发机构 (CA)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

如果从设备的 ASC 存储请求的导出的证书，则必须指定一个索引。 如果指定的索引不包含证书，该工具将报告错误。

如果 **-证书**指定为参数时，该工具会自动将表示通过指定的文件名称的证书类型的字符串 **-路径**参数。 下表定义不同的证书类型的字符串：

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
<td align="left"><p>用于进行身份验证到主机的证书身份验证接收器 ASC 主机证书。</p></td>
<td align="left"><p>任何大于 1 的索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"HCh"</p></td>
<td align="left"><p>用于进行身份验证的证书身份验证接收器到主机的主机证书。</p></td>
<td align="left"><p>任何大于 1 的索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p>"PCp"</p></td>
<td align="left"><p>管理命令中使用的设置证书序列预配和管理证书身份验证接收器。</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"SCh"</p></td>
<td align="left"><p>用于定义主机的受信任的证书签名者证书。 此受信任的证书是 ASCh 证书和零个或多个 SCh 证书的链。</p></td>
<td align="left"><p>任何大于 1 的索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p>"无效"</p></td>
<td align="left"><p>未知的证书类型是位于指定索引处。</p></td>
<td align="left"><p>不适用</p></td>
</tr>
</tbody>
</table>

 

例如，以下命令，将从目标设备中导出 PCp 证书，生成的文件，名为 c:\\MyCertificates\\myCertPCp.cer:

```
EhStorCertMgrCmd /export -Certificate -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:1 -Path:c:\MyCertificates\myCert.cer
```

如果指定 **-NoType**参数与 **-证书**参数，该工具不追加到通过指定的文件名称的证书类型的字符串 **-路径**参数。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何从目标设备中的 ASC 存储区中导出证书位于索引 1 处：

```
EhStorCertMgrCmd /export -Certificate -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:1 -Path:c:\MyCertificates\myCert.cer
```

 

 

