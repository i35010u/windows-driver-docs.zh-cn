---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE
description: 扩展\_FLASHMODE\_的 KSPROPERTY\_CAMERACONTROL 扩展为支持助手 flash。
ms.assetid: 413B3A02-498A-4C5A-8940-9A0D10D6CE81
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE 流媒体设备
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
ms.openlocfilehash: bb87cdccb34b4ea3267c154993754f82a6a1fd1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843229"
---
# <a name="ksproperty_cameracontrol_extended_flashmode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE

扩展 **\_FLASHMODE\_的 KSPROPERTY\_CAMERACONTROL**扩展为支持助手 flash。

## <a name="usage-summary-table"></a>使用情况摘要表


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

功能标志的定义如下。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_ON               0x0000000000000080
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_AUTO             0x0000000000000100
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_OFF              0x0000000000000000
```

**KSCAMERA\_EXTENDEDPROP\_闪存\_助手\_**

此标志指示 "AF 助手" 指示灯处于开启状态。

**KSCAMERA\_EXTENDEDPROP\_闪存\_助手\_自动**

此标志类似于标志 **\_的助手**。 照相机驱动程序不会始终打开 AF 助手灯，而是根据当前的照明条件来确定是否应打开 AF 助手灯。

**KSCAMERA\_EXTENDEDPROP\_闪存\_助手\_关闭**

此标志指示 AF 助手 light 处于关闭状态。

使用**KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE**属性时， [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明与 Windows 8.1 DDI 相同。

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
