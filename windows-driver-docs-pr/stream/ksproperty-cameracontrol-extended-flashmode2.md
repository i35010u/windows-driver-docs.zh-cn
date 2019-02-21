---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE
description: KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE 属性已扩展为支持助手立刻正式投入工作。
ms.assetid: 413B3A02-498A-4C5A-8940-9A0D10D6CE81
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: f8806bf3588b8564c604d97cd6ad22c4d9832c51
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534497"
---
# <a name="kspropertycameracontrolextendedflashmode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE

**KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE**属性已扩展为支持助手立刻正式投入工作。

## <a name="usage-summary-table"></a>使用率摘要表


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控件</th>
<th>在任务栏的搜索框中键入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>Filter</p></td>
<td><p>同步</p></td>
</tr>
</tbody>
</table>

功能标志定义，如下所示。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_ON               0x0000000000000080
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_AUTO             0x0000000000000100
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_OFF              0x0000000000000000
```

**KSCAMERA\_EXTENDEDPROP\_FLASH\_ASSISTANT\_ON**

此标志指示已打开 AF 助手 light。

**KSCAMERA\_EXTENDEDPROP\_FLASH\_ASSISTANT\_AUTO**

此标志是类似于**助手\_ON**标志。 而不是始终打开 AF 助手灯，照相机驱动程序将确定是否 AF 助手 light 应打开根据当前的光照条件。

**KSCAMERA\_EXTENDEDPROP\_FLASH\_ASSISTANT\_OFF**

此标志指示 AF 助手指示灯不亮。

有关说明[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段时使用**KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE**属性将与 Windows 8.1 DDI 相同。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
