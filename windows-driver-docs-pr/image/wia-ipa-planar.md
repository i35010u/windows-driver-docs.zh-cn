---
title: WIA \_ IPA \_ 平面
description: WIA \_ IPA \_ 平面属性包含图像数据打包选项。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPA_PLANAR 图像设备
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
ms.openlocfilehash: 7f9ef9a3ecb4ccc4755e57366a6a387081b94fa2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817255"
---
# <a name="wia_ipa_planar"></a>WIA \_ IPA \_ 平面


WIA \_ IPA \_ 平面属性包含图像数据打包选项。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_planar_si"></span><span id="DDK_WIA_IPA_PLANAR_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表或 wia " \_ \_ 无"

访问权限：读/写或只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ IPA \_ 平面来确定图像打包选项，或设置当前图像打包选项。

下表介绍了 WIA IPA 平面的有效常量 \_ \_ 。

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
<td><p>图像数据采用打包像素格式。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PLANAR</p></td>
<td><p>图像数据采用平面格式。</p></td>
</tr>
</tbody>
</table>

 

如果设备只能设置为单个值，则可以实现 wia \_ IPA \_ 平面属性为 wia 属性 \_ \_ NONE 和只读。

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
<td><p>在 Windows Vista 和更高版本的操作系统中已过时。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





