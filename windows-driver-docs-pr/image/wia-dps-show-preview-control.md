---
title: WIA \_ DPS \_ 显示 \_ 预览 \_ 控件
description: WIA \_ DPS \_ 显示 \_ 预览 \_ 控制属性指示项是否需要向用户显示预览控件。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_DPS_SHOW_PREVIEW_CONTROL 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_SHOW_PREVIEW_CONTROL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bc02663c9afd4667a3113c2a61ab20b5cc144a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831717"
---
# <a name="wia_dps_show_preview_control"></a>WIA \_ DPS \_ 显示 \_ 预览 \_ 控件


WIA \_ DPS \_ 显示 \_ 预览 \_ 控制属性指示项是否需要向用户显示预览控件。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dps_show_preview_control_si"></span><span id="DDK_WIA_DPS_SHOW_PREVIEW_CONTROL_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

下表介绍了 WIA \_ DPS \_ 显示 \_ 预览控件中的有效常量 \_ 。

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

 

WIA \_ DPS \_ 显示 \_ 预览 \_ 控件属性可帮助控制无法预览的设备。 例如，某些送纸器驱动设备无法重新加载预览扫描纸张。

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
<td><p>适用于 Microsoft Windows XP。 于 windows Vista 和更高版本，请使用 WIA_IPS_SHOW_PREVIEW_CONTROL 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IP \_ 显示 \_ 预览 \_ 控件**](wia-ips-show-preview-control.md)

 

 






