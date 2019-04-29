---
title: WIA\_IPA\_PROP\_STREAM\_COMPAT\_ID
description: WIA\_IPA\_PROP\_流\_COMPAT\_ID 属性指定一个表示一组设备属性值的类标识符 (CLSID)。
ms.assetid: e0701a7a-45e8-4096-8f20-2ed7d3113181
keywords:
- WIA_IPA_PROP_STREAM_COMPAT_ID 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_PROP_STREAM_COMPAT_ID
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1563f77641271777dbfc296527f2049207e6871f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380349"
---
# <a name="wiaipapropstreamcompatid"></a>WIA\_IPA\_PROP\_STREAM\_COMPAT\_ID


WIA\_IPA\_PROP\_流\_COMPAT\_ID 属性指定一个表示一组设备属性值的类标识符 (CLSID)。

## <span id="ddk_wia_ipa_prop_stream_compat_id_si"></span><span id="DDK_WIA_IPA_PROP_STREAM_COMPAT_ID_SI"></span>


属性类型：VT\_CLSID

有效值：WIA\_PROP\_列表

访问权限：只读

<a name="remarks"></a>备注
-------

如果设备驱动程序实现 WIA\_IPA\_PROP\_流\_COMPAT\_ID 属性，应用程序使用此属性来确定设备是否支持一组值。

下表描述了有效使用 WIA 的常量\_IPA\_PROP\_流\_COMPAT\_id。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>格式</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WiaImgFmt_BMP</p></td>
<td><p>标头文件的 Microsoft Windows 位图</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_EMF</p></td>
<td><p>扩展的 Windows 图元文件</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_EXIF</p></td>
<td><p>可交换文件格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_FLASHPIX</p></td>
<td><p>FlashPix 格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_GIF</p></td>
<td><p>GIF 图像格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_ICO</p></td>
<td><p>Windows 图标文件格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_JPEG</p></td>
<td><p>JPEG 压缩的格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_PHOTOCD</p></td>
<td><p>· Kodak 文件格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_PNG</p></td>
<td><p>W3C PNG 格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_MEMORYBMP</p></td>
<td><p>Windows 位图不带标头文件</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_TIFF</p></td>
<td><p>标记图像文件格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_WMF</p></td>
<td><p>Windows 图元文件</p></td>
</tr>
</tbody>
</table>

 

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

 

 





