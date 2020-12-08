---
title: /Add 开关
description: 增强的存储证书管理工具的/Add 交换机将证书添加到 (ASC) 存储在指定 USB 设备上的身份验证接收器证书。
keywords:
- /Add 交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /Add
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 214b7bdc8520252aa3270181739465a3d3fd21aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828185"
---
# <a name="add-switch"></a>/Add 开关


增强的存储证书管理工具的 **/add** 交换机将证书添加到 (ASC) 存储设备1667上的身份验证接收器证书。

**注意**  在本主题中，指定的与 IEEE 1667 兼容的 USB 存储设备称为 *目标设备*。

 

```
    EhStorCertMgrCmd 
    /Add
     -Volume:
    VolumeName  -Type:CertificateType  -Validation:{None|Basic|Extended} [-Index:IndexValue] [[-Store:Certificate]|[-File:PathToFile]|
[-New:PathToIniFile]]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume______"></span><span id="_______-volume______"></span><span id="_______-VOLUME______"></span>**-卷**   
目标设备的卷名。 有关此参数的格式的详细信息，请参阅 [增强的存储证书管理工具概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**注意**  要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令提示符下键入 **EhStorCertMgrCmd/list** ，然后按 **enter**。

 

<span id="_______-Type______"></span><span id="_______-type______"></span><span id="_______-TYPE______"></span>**-Type**   
要添加到目标设备中的 ASC 存储区的证书类型。 下表定义了有效的证书类型。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">类型值</th>
<th align="left">描述</th>
<th align="left">索引</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ASCh</strong></p></td>
<td align="left"><p>身份验证接收器证书 (ASC) 用于向主机验证证书身份验证接收器的主机证书。</p></td>
<td align="left"><p>大于1的任何索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>HCh</strong></p></td>
<td align="left"><p>主机证书 (HCh) ，用于向证书身份验证接收器验证主机的身份。</p></td>
<td align="left"><p>大于1的任何索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>PCp</strong></p></td>
<td align="left"><p>设置证书 (PCp) ，在管理命令序列中用于预配和管理证书身份验证接收器。</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Sch-m</strong></p></td>
<td align="left"><p>签名者证书 (Sch-m) ，用于定义主机信任的证书。 此可信证书是 ASCh 证书的链和零个或多个 Sch-m 证书。</p></td>
<td align="left"><p>大于1的任何索引。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-Validation______"></span><span id="_______-validation______"></span><span id="_______-VALIDATION______"></span>**-验证**   
在目标设备中，可寻址命令目标 (ACT) 执行的证书验证过程的类型。 下表定义正确的验证类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">验证值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>无</strong></p></td>
<td align="left"><p>证书未经过验证。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>基本</strong></p></td>
<td align="left"><p>证书通过 IEEE 1667 标准中定义的基本验证策略进行验证。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>扩展</strong></p></td>
<td align="left"><p>证书通过 IEEE 1667 标准中定义的扩展验证策略进行验证。</p></td>
</tr>
</tbody>
</table>

 

**注意**  如果未指定-验证：参数，则该工具将使用验证值 **None**。

 

<span id="_______-Index______"></span><span id="_______-index______"></span><span id="_______-INDEX______"></span>**-Index**   
ASC 存储区中保存证书的位置的索引。 如果指定的索引包含证书，则该证书将被替换。 索引值必须大于零。

<span id="_______-Store______"></span><span id="_______-store______"></span><span id="_______-STORE______"></span>**-存储**   
主机上证书存储区中的证书名称。 如果在证书存储中找到该证书，则该工具会将其添加到目标设备中。

有关详细信息，请参阅 [从 Windows 证书存储中导入证书](importing-certificates-from-a-windows-certificate-store.md)。

<span id="_______-File______"></span><span id="_______-file______"></span><span id="_______-FILE______"></span>**-File**   
包含证书的文件的路径和名称。 如果找到了证书文件，则该工具会将其添加到目标设备中。 此证书可能是通过 [**MakeCert**](makecert.md) 工具创建的，也可能是通过增强的存储证书管理工具的 [**/export 交换机**](-export-switch.md) 导入的。

有关详细信息，请参阅 [从文件导入证书](importing-certificates-from-a-file.md)。

<span id="_______-New______"></span><span id="_______-new______"></span><span id="_______-NEW______"></span>**-New**   
包含用于创建自签名证书的规范的文件的路径和名称。 如果找到该文件，并且规范有效，则该工具会创建证书、对其进行数字签名，并将该证书添加到目标设备中。

有关详细信息，请参阅为 [**USB 存储设备创建证书**](creating-certificates-for-usb-storage-devices.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

将证书添加到目标设备时，以下准则适用：

-   PCp 证书用于在主机和目标设备之间执行管理身份验证。 如果目标设备没有 PCp 证书，则必须首先使用 PCp 证书预配目标设备。 对于 PCp 证书类型，必须使用值1指定 **-Index** 开关。

    **重要提示**  最好只使用 PCp 证书预配目标设备，该证书的私钥存储在计算机上的证书存储中。 如果在目标设备上设置了不正确的 PCp 证书，你将无法使用 [**/Initialize 开关**](-initialize-switch.md)清除包含 PCp 证书) 的证书存储 (。

     

-   如果在添加 HCh、ASCh 和 Sch-m 证书时未指定 **-Index** 开关，该工具会将证书存储在不使用的 ASC 存储区中的第一个索引中。

    **注意**  为了将这些证书类型添加到目标设备，正确的 PCp 证书必须驻留在主机中才能通过设备进行管理身份验证。

     

-   如果目标设备中的指定索引不为空，则 **/add** 交换机会将现有证书替换为指定的证书。

    **注意**  如果增强的存储证书管理工具替换指定索引处的 ASCh 证书，则该工具将删除 ASCh 证书链中的所有相关 Sch-m。
    如果该工具替换属于 ASCh 证书链一部分的指定索引处的 Sch-m 证书，则该工具将删除该 Sch-m 证书及其所有其父 Sch-m 证书。

     

-   只能指定 **-Store**、-**File** 或 **-New** 参数之一。

**注意**   增强的存储证书管理工具无法在目标设备中添加、删除或替换 asc 制造商 (ASCm) 证书。

 

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何从主机上的证书存储将证书添加到目标设备：

```
EhStorCertMgrCmd /Add -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:1 -Store:TestCert -Type:PCp -Validation:None
```

 

 





