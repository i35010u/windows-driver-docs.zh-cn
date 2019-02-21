---
title: WIA\_IPA\_平面数据
description: WIA\_IPA\_平面属性包含图像数据打包选项。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: df4013db-8f9e-428a-83dd-c344f7998034
keywords:
- WIA_IPA_PLANAR 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_PLANAR
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e3708de0cb31754ea19340cbc5a05cbf1a83f27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520221"
---
# <a name="wiaipaplanar"></a>WIA\_IPA\_平面数据


WIA\_IPA\_平面属性包含图像数据打包选项。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_planar_si"></span><span id="DDK_WIA_IPA_PLANAR_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表或 WIA\_PROP\_NONE

访问权限：读/写或只读的

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPA\_平面数据以确定映像打包选项或设置当前图像打包选项。

下表描述了有效使用 WIA 的常量\_IPA\_平面数据。

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
<td><p>WIA_PACKED_PIXEL</p></td>
<td><p>图像数据的格式打包像素。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PLANAR</p></td>
<td><p>图像数据的平面格式。</p></td>
</tr>
</tbody>
</table>

 

如果设备可以设置为单个值，则可以实现 WIA\_IPA\_平面属性作为 WIA\_PROP\_NONE 和只读的。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中已过时。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





