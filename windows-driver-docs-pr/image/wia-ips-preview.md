---
title: WIA \_ IP \_ 预览版
description: "\"WIA \\_ ip \\_ 预览\" 属性指示设备的预览模式。"
keywords:
- WIA_IPS_PREVIEW 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PREVIEW
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ef2aef19c2615cfead349229a01161dd613ee1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839089"
---
# <a name="wia_ips_preview"></a>WIA \_ IP \_ 预览版


"WIA \_ ip \_ 预览" 属性指示设备的预览模式。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序将 WIA \_ IPS \_ 预览版设置为将设备置于预览模式。

下表描述了对 WIA ip 预览版有效的常量 \_ \_ 。

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
<td><p>WIA_FINAL_SCAN</p></td>
<td><p>该应用程序将执行最终扫描。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PREVIEW_SCAN</p></td>
<td><p>该应用程序将执行预览扫描。</p></td>
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
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。 对于 Windows XP，请改用 WIA_DPS_PREVIEW 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ 预览版**](wia-dps-preview.md)

 

 






