---
title: WIA \_ IPA \_ \_ \_ \_
description: WIA \_ IPA \_ \_ \_ 属性流兼容 \_ ID 属性指定类标识符 (CLSID) 表示一组设备属性值。
keywords:
- WIA_IPA_PROP_STREAM_COMPAT_ID 图像设备
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
ms.openlocfilehash: 49957ff32bd6d767ccd3d937fbcef533b87d0e8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817235"
---
# <a name="wia_ipa_prop_stream_compat_id"></a>WIA \_ IPA \_ \_ \_ \_


WIA \_ IPA \_ \_ \_ 属性流兼容 \_ ID 属性指定类标识符 (CLSID) 表示一组设备属性值。

## <span id="ddk_wia_ipa_prop_stream_compat_id_si"></span><span id="DDK_WIA_IPA_PROP_STREAM_COMPAT_ID_SI"></span>


属性类型： VT \_ CLSID

有效值： WIA 内容 \_ \_ 列表

访问权限：只读

<a name="remarks"></a>备注
-------

如果设备驱动程序实现了 WIA \_ IPA \_ \_ 属性流 \_ 兼容 \_ ID 属性，则应用程序将使用此属性来确定设备是否支持一组值。

下表描述了对 WIA \_ IPA 类型 \_ \_ 流 \_ 兼容 \_ ID 有效的常量。

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
<td><p>带有标头文件的 Microsoft Windows 位图</p></td>
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
<td><p>JPEG 压缩格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_PHOTOCD</p></td>
<td><p>Eastman Kodak 文件格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_PNG</p></td>
<td><p>W3C PNG 格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_MEMORYBMP</p></td>
<td><p>不带标头文件的 Windows 位图</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_TIFF</p></td>
<td><p>Tag 图像文件格式</p></td>
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
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





