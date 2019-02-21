---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE
description: 场景模式属性选择一种定义的驱动程序模式，它表示预设控件的集合。
ms.assetid: 32C350FF-AA54-4F28-8AD2-341A31648B60
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5af16830e4ebdf1c98da667000d2dffc70c98675
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523095"
---
# <a name="kspropertycameracontrolextendedscenemode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE

场景模式属性选择一种定义的驱动程序模式，它表示预设控件的集合。 驱动程序确定分配给场景模式下的预设，并选择场景时启用这些控件设置。

## <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。 **KSCAMERA\_EXTENDEDPROP\_值**是必需的但**值**成员将被忽略。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_值)。 **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

**功能**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含一个或多个以下的按位 OR 组合驱动程序支持的场景模式。

| 场景模式                                       | 描述                                                           |
|--------------------------------------------------|-----------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_AUTO          | 自动气味模式。 控件是在其自动设置。            |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_MACRO         | 宏场景模式 （驱动程序定义）。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_纵向      | 纵向场景模式 （驱动程序定义）。                                 |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_运动         | 运动场景模式 （驱动程序定义）。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_雪          | 白雪降落场景模式 （驱动程序定义）。                                     |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_夜间         | 夜间场景模式 （驱动程序定义）。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_BEACH         | 海滩场景模式 （驱动程序定义）。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_停用        | 停用场景模式 （驱动程序定义）。                                   |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_CANDLELIGHT   | Candlelight 场景模式 （驱动程序定义）。                              |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_横向     | 横向场景模式 （驱动程序定义）。                                |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_NIGHTPORTRAIT | 晚上纵向场景模式 （驱动程序定义）。                           |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_背光       | 背光场景模式 （驱动程序定义）。                                  |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_手动        | 手动更改控件并设置任何预定义的场景模式。 |

**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含场景模式当前设置为照相机。 用于相机的默认场景模式始终是 KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_自动。

此属性控制是异步的不取消。

## <a name="remarks"></a>备注

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY\_类型\_GET 请求，该驱动程序设置的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)到以下。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0XFFFFFFFF)。</td>
</tr>
<tr class="odd">
<td>尺寸</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |（场景模式支持值）。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前场景模式值设置 （只有一个值）。</td>
</tr>
</tbody>
</table>

如果没有场景之前设置模式，然后**标志**设置为 KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_自动 （默认值）。

### <a name="setting-the-property"></a>将属性设置

设置该属性是，KSPROPERTY\_类型\_集请求**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)将包含要启用的场景模式。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>从开始提供 Windows 8.1。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
