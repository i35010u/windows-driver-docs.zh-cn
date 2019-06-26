---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_缩放
description: KSPROPERTY\_CAMERACONTROL\_扩展\_缩放用于控制数字的缩放。
ms.assetid: 93CFCBFC-69B3-4241-913F-94615599BE8E
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: a6a7542eea0b46d974f6d7afe89ebb3fba9c44a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356650"
---
# <a name="kspropertycameracontrolextendedzoom"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_缩放

**KSPROPERTY\_CAMERACONTROL\_扩展\_缩放**用于控制数字的缩放。 在中定义[ **KSPROPERTY\_CAMERACONTROL\_扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举，用于获取和设置的缩放比率和获取缩放范围是从驱动程序。 在 Windows 10 中，此控件已扩展到还支持平滑缩放。

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

以下标志可以置于**KSCAMERA\_EXTENDEDPROP\_标头。标志**控制平滑缩放与直接缩放到字段。 在定义了默认驱动程序。

```cpp
#define KSCAMERA_EXTENDEDPROP_ZOOM_DEFAULT  0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_ZOOM_DIRECT   0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_ZOOM_SMOOTH   0x0000000000000002
```

如果该驱动程序支持此控件，它必须支持**KSCAMERA\_EXTENDEDPROP\_缩放\_默认**。

如果该驱动程序不支持数字缩放，该驱动程序不应实现此控件。

下表介绍标志功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_DEFAULT</strong></p></td>
<td><p>这是必需的功能。 如果指定，该驱动程序将决定是否应该应用直接缩放或平滑缩放和缩放到 VideoProc.Value.ul 中相应地指定目标缩放系数。 此标志是互斥的直接和平滑流标记与。</p></td>
</tr>
<tr class="even">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_DIRECT</strong></p></td>
<td><p>这是必需的功能。 如果指定，该驱动程序将缩放到 VideoProc.Value.ul 中尽可能快地指定目标缩放系数。 此标志是互相排斥使用自动和平滑的标志。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_SMOOTH</strong></p></td>
<td><p>此功能是可选的。 如果指定，该驱动程序将缩放到 VideoProc.Value.ul 中逐渐平滑的方式指定目标缩放系数。 达到指定的缩放因子帧所需的数量由驱动程序。 此标志是互相排斥使用自动和直接的标志。</p></td>
</tr>
</tbody>
</table>

每个**获取**调用时，该驱动程序必须报告的当前缩放范围允许根据当前配置或安装程序。

下表包含的说明和要求[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段时使用**KSPROPERTY\_CAMERACONTROL\_扩展\_缩放**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>这必须是 1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xFFFFFFFF)</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)"><strong>KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING</strong></a>)，</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这表示最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是上面定义的受支持的标志的按位 OR。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是上面定义的受支持的任何的标志一个。</p></td>
</tr>
</tbody>
</table>

下表包含的说明和要求**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**结构的字段**KSPROPERTY\_CAMERACONTROL\_扩展\_缩放**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>模式</p></td>
<td><p>这是未使用，必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>最小值/最大/步骤</p></td>
<td><p>最小值/最大/步骤包含最小值/最大/增量的缩放比率 Q16 格式照相机驱动程序支持。 该驱动程序必须返回以下值作为<strong>获取</strong>操作。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>有关<strong>设置</strong>操作，VideoProc.Value.ul 必须指定最小值/最大/Step 参数所描述的范围内的缩放比率。 有关<strong>获取</strong>操作，则驱动程序必须返回当前的缩放比率。</p></td>
</tr>
<tr class="even">
<td><p>保留</p></td>
<td><p>这是未使用。 这必须忽略由驱动程序。</p></td>
</tr>
</tbody>
</table>

此属性控制是同步的不取消。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
