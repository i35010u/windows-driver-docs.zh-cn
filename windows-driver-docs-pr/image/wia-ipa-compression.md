---
title: WIA\_IPA\_压缩
description: WIA\_IPA\_压缩属性包含当前使用的压缩类型。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 6853dc51-bde0-4548-92f6-678b55cf6275
keywords:
- WIA_IPA_COMPRESSION 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_COMPRESSION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fbca734cb6848f23608573f3be77e326b9212d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369563"
---
# <a name="wiaipacompression"></a>WIA\_IPA\_压缩


WIA\_IPA\_压缩属性包含当前使用的压缩类型。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_compression_si"></span><span id="DDK_WIA_IPA_COMPRESSION_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写 （图像收购）;只读的 （映像存储）

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPA\_压缩属性来确定映像压缩类型或应用程序设置此属性可配置的压缩设置。

下表描述了有效使用 WIA 的常量\_IPA\_压缩。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_COMPRESSION_BI_RLE4</p></td>
<td><p>RLE 4 压缩</p></td>
</tr>
<tr class="even">
<td><p>WIA_COMPRESSION_BI_RLE8</p></td>
<td><p>RLE 8 压缩</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_G3</p></td>
<td><p>组 3 压缩</p></td>
</tr>
<tr class="even">
<td><p>WIA_COMPRESSION_G4</p></td>
<td><p>组 4 压缩</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_JBIG<em></p></td>
<td><p>是 11544 (ITU-T T.82) 压缩</p></td>
</tr>
<tr class="even">
<td><p>WIA_COMPRESSION_JPEG</p></td>
<td><p>JPEG 压缩</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_JPEG2K</em></p></td>
<td><p>JPEG 2000 压缩</p></td>
</tr>
<tr class="even">
<td><p>WIA_COMPRESSION_NONE</p></td>
<td><p>不进行压缩</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_PNG*</p></td>
<td><p>W3C PNG 压缩</p></td>
</tr>
</tbody>
</table>

 

标有星号值 (\*) 适用于 Windows Vista 和更高版本仅操作系统。

**请注意**  文件格式时 WiaImgFmt\_XPS 或 WiaImgFmt\_PDFA、 WIA\_压缩\_无表示"未定义"; 在设备不能选择内部压缩 （如果有）对于存储在以下两种文档格式的映像。

 

所有 WIA 2.0 微型驱动程序必须将此属性的初始值都设置为其默认值，即 WIA\_压缩\_NONE。

WIA 的访问权限\_IPA\_压缩属性是读/写所有图像但只读存储的图像项的收购。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





