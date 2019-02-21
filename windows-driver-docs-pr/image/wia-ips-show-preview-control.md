---
title: WIA\_IPS\_显示\_预览\_控件
description: WIA\_IPS\_显示\_预览\_控件属性指示某个项是否需要向用户显示预览控件。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 50559dc2-8e5b-4dbc-9c39-8c51e0f825dc
keywords:
- WIA_IPS_SHOW_PREVIEW_CONTROL 成像设备
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
ms.openlocfilehash: 65bf1c747517b843b0d316d3742a8f68446d606d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545456"
---
# <a name="wiaipsshowpreviewcontrol"></a>WIA\_IPS\_显示\_预览\_控件


WIA\_IPS\_显示\_预览\_控件属性指示某个项是否需要向用户显示预览控件。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了有效使用 WIA 的常量\_IPS\_显示\_预览\_控件。

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
<td><p>不再向用户显示预览控件，因为此设备无法执行预览。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SHOW_PREVIEW_CONTROL</p></td>
<td><p>显示给用户，预览控件，因为此设备可以执行预览。</p></td>
</tr>
</tbody>
</table>

 

可以使用 WIA\_IPS\_显示\_预览\_控件属性，以帮助控制设备，无法预览。 例如，某些送纸器驱动的设备不能重新加载预览扫描的纸张。

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
<td><p>在 Windows Vista 和更高版本操作系统中可用。 对于 Windows XP 中，而是使用 WIA_DPS_SHOW_PREVIEW_CONTROL 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_DPS\_显示\_预览\_控件**](wia-dps-show-preview-control.md)

 

 






