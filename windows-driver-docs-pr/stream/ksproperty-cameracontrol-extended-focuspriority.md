---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSPRIORITY
description: '\_ \_ \_ KSPROPERTY CAMERACONTROL 扩展属性枚举中定义的 KSPROPERTY CAMERACONTROL 扩展 FOCUSPRIORITY 属性 ID \_ \_ \_ 用于配置焦点优先级。'
ms.assetid: 7E3558A1-0D0D-4470-B9C9-61EA359E92C5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSPRIORITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSPRIORITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d0b60555bb4d2760510dd210e234e35fbe067fd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187377"
---
# <a name="ksproperty_cameracontrol_extended_focuspriority"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSPRIORITY


[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举中定义的**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSPRIORITY**属性 ID 用于配置焦点优先级。 设置焦点优先级后，焦点将优先于拍摄的图片，以确保所拍摄的图片始终处于焦点。 否则，无论图片是否处于焦点上，都将立即执行图片。 处理失败焦点以及是否需要超时的行为是驱动程序的内部和最高的。

## <a name="usage-summary-table"></a>使用情况摘要表


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>作用域</th>
<th>控制</th>
<th>类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>筛选器</p></td>
<td><p>同步</p></td>
</tr>
</tbody>
</table>

 

若要配置焦点优先级，必须使用 **KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSPRIORITY** 属性 ID。 设置焦点优先级后，焦点将优先于拍摄的图片，以确保所拍摄的图片始终处于焦点。 如果未设置焦点优先级，则无论图片是否处于焦点上，都将立即执行图片。 处理失败焦点的行为失败，超时由 OEM 确定，并且是驱动程序内部的。

对于 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)，将以下标志定义为值。 在 get 调用中，照相机驱动程序使用其中一个标志返回其当前焦点优先级配置。 在集调用中，照相机驱动程序使用其中一个标志设置新的焦点优先级配置。

```cpp
#define KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_OFF     0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_ON      0x0000000000000001
```

**注意**   这是一个同步控件，没有为此控件定义任何功能。

 

下表包含使用焦点优先级控件时 **KSCAMERA \_ EXTENDEDPROP \_ 标头** 结构字段的说明和要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>这必须为1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须 KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) ，</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这指示错误结果，</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是0，</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的 KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_Xxx 标志之一。</p></td>
</tr>
</tbody>
</table>

 

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