---
title: WIA \_ IP \_ 显示 \_ 预览 \_ 控件
description: WIA \_ ip \_ 显示 \_ 预览 \_ 控制属性指示项是否需要向用户显示预览控件。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_SHOW_PREVIEW_CONTROL 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SHOW_PREVIEW_CONTROL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d120e10ad37c0c8696cb1c227abff32c9c993ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803855"
---
# <a name="wia_ips_show_preview_control"></a>WIA \_ IP \_ 显示 \_ 预览 \_ 控件


WIA \_ ip \_ 显示 \_ 预览 \_ 控制属性指示项是否需要向用户显示预览控件。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了在 WIA \_ ip \_ 显示 \_ 预览控件时有效的常量 \_ 。

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
<td><p>WIA_DONT_SHOW_PREVIEW_CONTROL</p></td>
<td><p>不向用户显示预览控件，因为此设备无法执行预览。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SHOW_PREVIEW_CONTROL</p></td>
<td><p>向用户显示预览控件，因为此设备可以执行预览。</p></td>
</tr>
</tbody>
</table>

 

你可以使用 "WIA \_ ip \_ 显示 \_ 预览 \_ 控件" 属性来帮助控制无法预览的设备。 例如，某些送纸器驱动设备无法重新加载预览扫描纸张。

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
<td><p>在 Windows Vista 和更高版本的操作系统中可用。 对于 Windows XP，请改用 WIA_DPS_SHOW_PREVIEW_CONTROL 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ 显示 \_ 预览 \_ 控件**](wia-dps-show-preview-control.md)

 

 






