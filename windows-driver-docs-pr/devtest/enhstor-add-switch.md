---
title: /Add 开关
description: 增强型存储证书管理工具的 /Add 开关添加到指定的 USB 设备上的身份验证接收器证书 (ASC) 存储的证书。
ms.assetid: cca064ae-f525-45e4-9778-5fb23efbce88
keywords:
- / 添加开关驱动程序开发工具
topic_type:
- apiref
api_name:
- /Add
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67168f719cd5ed3b9c295b1b8c956143f65df45c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565451"
---
# <a name="add-switch"></a>/Add 开关


**/Add**增强存储证书管理工具的开关将证书添加到指定 IEEE 1667 合规 USB 存储设备上的身份验证接收器证书 (ASC) 存储。

**请注意**本主题中指定的 IEEE 1667 合规 USB 存储设备被称为*目标设备*。

 

```
    EhStorCertMgrCmd 
    /Add
     -Volume:
    VolumeName  -Type:CertificateType  -Validation:{None|Basic|Extended} [-Index:IndexValue] [[-Store:Certificate]|[-File:PathToFile]|
[-New:PathToIniFile]]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume______"></span><span id="_______-volume______"></span><span id="_______-VOLUME______"></span> **-Volume**   
目标设备的卷名称。 此参数的格式的详细信息，请参阅[增强存储证书管理工具的概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**请注意**若要生成的当前连接到计算机的 IEEE 1667 合规 USB 存储设备的卷名称列表，请键入**EhStorCertMgrCmd /List**在命令提示符，然后再按**Enter**.

 

<span id="_______-Type______"></span><span id="_______-type______"></span><span id="_______-TYPE______"></span> **-Type**   
要添加到的证书类型 ASC 将存储在目标设备。 下表定义了有效的证书类型。

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
<td align="left"><p>身份验证接收器证书 (ASC) 主机证书用于进行身份验证到主机的证书身份验证接收器。</p></td>
<td align="left"><p>任何大于 1 的索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>HCh</strong></p></td>
<td align="left"><p>用于进行身份验证的证书身份验证接收器到主机的主机证书 (HCh)。</p></td>
<td align="left"><p>任何大于 1 的索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>PCp</strong></p></td>
<td align="left"><p>要预配和管理证书身份验证接收器管理命令中使用的预配证书 (PCp) 序列。</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SCh</strong></p></td>
<td align="left"><p>用于定义主机的受信任的证书签名者证书 (SCh)。 此受信任的证书是 ASCh 证书和零个或多个 SCh 证书的链。</p></td>
<td align="left"><p>任何大于 1 的索引。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-Validation______"></span><span id="_______-validation______"></span><span id="_______-VALIDATION______"></span> **-Validation**   
证书验证过程中执行的目标设备中的可寻址命令目标 (ACT) 的类型。 下表定义了正确的验证类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">验证值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>无</strong></p></td>
<td align="left"><p>不验证该证书。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>基本</strong></p></td>
<td align="left"><p>IEEE 1667 标准中定义，通过基本验证策略验证证书。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>扩展</strong></p></td>
<td align="left"><p>扩展验证策略通过验证证书的 IEEE 1667 标准中定义。</p></td>
</tr>
</tbody>
</table>

 

**请注意**如果-验证： 未指定参数，该工具使用的验证值**None**。

 

<span id="_______-Index______"></span><span id="_______-index______"></span><span id="_______-INDEX______"></span> **-Index**   
将在其中保存该证书的 ASC 存储区中的索引。 如果指定的索引包含的证书，该证书将被替换。 索引值必须大于零。

<span id="_______-Store______"></span><span id="_______-store______"></span><span id="_______-STORE______"></span> **-Store**   
在主机上的证书存储中的证书的名称。 如果在证书存储区中找到的证书，该工具会将其添加到目标设备。

有关详细信息，请参阅[Windows 证书存储中导入证书](importing-certificates-from-a-windows-certificate-store.md)。

<span id="_______-File______"></span><span id="_______-file______"></span><span id="_______-FILE______"></span> **-File**   
路径和包含的证书文件的名称。 如果找到证书文件，则该工具会将其添加到目标设备。 此证书可以通过创建[ **MakeCert** ](makecert.md)工具或通过导入[ **/Export 开关**](-export-switch.md)的增强存储证书管理工具。

有关详细信息，请参阅[从文件导入证书](importing-certificates-from-a-file.md)。

<span id="_______-New______"></span><span id="_______-new______"></span><span id="_______-NEW______"></span> **-New**   
路径和文件包含用于创建自签名的证书的规范的名称。 如果找到该文件的规范是有效，该工具创建证书进行数字签名，并将证书添加到目标设备。

有关详细信息，请参阅[ **USB 存储设备的创建证书**](creating-certificates-for-usb-storage-devices.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

将证书添加到目标设备时，应考虑下列准则：

-   PCp 证书用于执行管理主机和目标设备之间的身份验证。 如果目标设备没有 PCp 证书，必须先设置 PCp 证书与目标设备。 对于 PCp 证书类型， **-索引**交换机必须指定一个值。

    **重要**预配目标设备使用 PCp 证书只有在您的计算机上的证书存储中存储其私钥是最佳选择。 如果在目标设备上设置了错误的 PCp 证书，则将无法通过清除 （其中包括 PCp 证书） 的证书存储区[ **/Initialize 交换机**](-initialize-switch.md)。

     

-   如果 **-索引**添加 HCh，ASCh，且 SCh 证书，该工具将该证书存储中未使用的 ASC 存储区中的第一个索引时不指定开关。

    **请注意**为了添加这些证书类型到目标设备，正确的 PCp 证书必须驻留在主机以与设备一起传递管理身份验证。

     

-   如果指定的索引不在目标设备中，为空 **/add**开关使用指定的证书替换现有的证书。

    **请注意**增强存储证书管理工具将替代中指定索引处的 ASCh 证书，如果该工具会将所有相关的 SCh 删除 ASCh 证书链。
    如果，工具将替代是 ASCh 证书链的一部分的指定索引处的 SCh 证书，该工具会在证书链中删除 SCh 证书以及其父 SCh 证书。

     

-   只有一个 **-应用商店**、-**文件**或 **-新**必须指定参数。

**请注意**的增强存储证书管理工具不能添加、 删除或替换从目标设备中的 ASC 存储区的 ASC 制造商 (ASCm) 证书。

 

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何将证书添加到的目标设备在主机上的证书存储中：

```
EhStorCertMgrCmd /Add -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:1 -Store:TestCert -Type:PCp -Validation:None
```

 

 





