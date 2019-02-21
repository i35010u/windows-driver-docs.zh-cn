---
title: WIA\_IP\_预览
description: WIA\_IP\_预览属性指示设备的预览模式。
ms.assetid: 06caadc7-2a65-4c54-8d63-4aa1c17186de
keywords:
- WIA_IPS_PREVIEW 成像设备
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
ms.openlocfilehash: ebde67ca6fa81701d2c0b7d5b72643fddecd9144
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525883"
---
# <a name="wiaipspreview"></a>WIA\_IP\_预览


WIA\_IP\_预览属性指示设备的预览模式。

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序设置 WIA\_IP\_预览版将设备置于预览模式。

下表描述了有效使用 WIA 的常量\_IP\_预览。

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
<td><p>应用程序将执行最后一个扫描。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PREVIEW_SCAN</p></td>
<td><p>应用程序将执行预览扫描。</p></td>
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
<td><p>在 Windows Vista 和更高版本操作系统中可用。 对于 Windows XP 中，而是使用 WIA_DPS_PREVIEW 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_DPS\_预览**](wia-dps-preview.md)

 

 






