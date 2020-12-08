---
title: WIA \_ IPA \_ 压缩
description: WIA \_ IPA \_ COMPRESSION 属性包含使用的当前压缩类型。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPA_COMPRESSION 图像设备
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
ms.openlocfilehash: abb57658d02b0fd304db843f79eef83b08fa5351
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840971"
---
# <a name="wia_ipa_compression"></a>WIA \_ IPA \_ 压缩


WIA \_ IPA \_ COMPRESSION 属性包含使用的当前压缩类型。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_compression_si"></span><span id="DDK_WIA_IPA_COMPRESSION_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读取/写入 (映像) ;只读 (映像存储) 

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ IPA \_ COMPRESSION 属性以确定映像压缩类型，或者应用程序将此属性设置为配置压缩设置。

下表介绍了 WIA IPA 压缩的有效常量 \_ \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
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
<td><p>组3压缩</p></td>
</tr>
<tr class="even">
<td><p>WIA_COMPRESSION_G4</p></td>
<td><p>组4压缩</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_JBIG<em></p></td>
<td><p>为 11544 (ITU-T) 压缩</p></td>
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
<td><p>无压缩</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_PNG *</p></td>
<td><p>W3C PNG 压缩</p></td>
</tr>
</tbody>
</table>

 

用星号标记 () 的值 \* 仅适用于 Windows Vista 和更高版本的操作系统。

**注意**   当文件格式为 WiaImgFmt \_ XPS 或 WiaImgFmt \_ PDFA 时，WIA \_ 压缩 \_ NONE 表示 "未定义"; 如果有任何以这两种文档格式存储的图像) ，则设备不能选择内部压缩 (。

 

所有 WIA 2.0 微型驱动程序都必须将此属性的初始值设置为其默认值，即 WIA \_ COMPRESSION \_ NONE。

WIA \_ IPA COMPRESSION 属性的访问权限 \_ 对于所有图像获取都是可读/写的，但存储的图像项是只读的。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





