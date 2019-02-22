---
title: WIA\_DPS\_显示\_预览\_控件
description: WIA\_DPS\_显示\_预览\_控件属性指示某个项是否需要向用户显示预览控件。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 45bd6030-34b1-466b-b594-e7ee0d2902f9
keywords:
- WIA_DPS_SHOW_PREVIEW_CONTROL 成像设备
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
ms.openlocfilehash: 2efaac3e83ff8d8a8a5b05100282260c8299a778
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544849"
---
# <a name="wiadpsshowpreviewcontrol"></a>WIA\_DPS\_显示\_预览\_控件


WIA\_DPS\_显示\_预览\_控件属性指示某个项是否需要向用户显示预览控件。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dps_show_preview_control_si"></span><span id="DDK_WIA_DPS_SHOW_PREVIEW_CONTROL_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了有效使用 WIA 的常量\_DPS\_显示\_预览\_控件。

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

 

WIA\_DPS\_显示\_预览\_控件属性可帮助控制无法预览的设备。 例如，某些送纸器驱动的设备不能重新加载预览扫描的纸张。

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
<td><p>使用 Microsoft Windows XP 可用。 适用于 Windows Vista 和更高版本，使用 WIA_IPS_SHOW_PREVIEW_CONTROL 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_IPS\_显示\_预览\_控件**](wia-ips-show-preview-control.md)

 

 






