---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 缩放
description: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 缩放用于控制数字缩放。
ms.assetid: 93CFCBFC-69B3-4241-913F-94615599BE8E
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM 流媒体设备
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
ms.openlocfilehash: 39bdd8e3ea6dba0fcc83537c03c590bbc9e4e4fe
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107266"
---
# <a name="ksproperty_cameracontrol_extended_zoom"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 缩放

**KSPROPERTY \_CAMERACONTROL \_ 扩展 \_ 缩放** 用于控制数字缩放。 它在 [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property) 枚举中定义，用于获取和设置缩放比率，并从驱动程序获取缩放范围。 在 Windows 10 中，此控件扩展为还支持平滑缩放。

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

以下标志可以放置在 **KSCAMERA \_ EXTENDEDPROP \_ 标头中。** 用于控制平滑缩放和直接缩放的标志字段。 默认值由驱动程序定义。

```cpp
#define KSCAMERA_EXTENDEDPROP_ZOOM_DEFAULT  0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_ZOOM_DIRECT   0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_ZOOM_SMOOTH   0x0000000000000002
```

如果驱动程序支持此控件，则它必须支持 **KSCAMERA \_ EXTENDEDPROP \_ ZOOM \_ 默认值**。

如果驱动程序不支持数字缩放，驱动程序不应实现此控制。

下表介绍了标志功能。

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
<td><p>这是必需的功能。 指定时，驱动程序将决定是否应应用直接缩放或平滑缩放，并相应地缩放到 VideoProc 中指定的目标缩放系数。 此标志与直接和平滑标志互斥。</p></td>
</tr>
<tr class="even">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_DIRECT</strong></p></td>
<td><p>这是必需的功能。 如果指定此值，驱动程序将尽可能快地缩放到 VideoProc 中指定的目标缩放系数。 此标志与自动和平滑标志互斥。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_SMOOTH</strong></p></td>
<td><p>此功能是可选的。 指定时，驱动程序将缩放到 VideoProc 中指定的目标缩放系数。 达到指定缩放系数所用的帧数取决于驱动程序。 此标志与自动和直接标志互斥。</p></td>
</tr>
</tbody>
</table>

对于每个 **GET** 调用，驱动程序必须根据当前配置或设置来报告允许的当前缩放范围。

下表包含使用**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 缩放**属性时[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。

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
<td><p>这必须 <strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xffffffff) ，</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)"><strong>KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING</strong></a>) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这指示上次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是上面定义的支持标志的按位 "或"。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的任何一个支持的标志。</p></td>
</tr>
</tbody>
</table>

下表包含**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 缩放**属性的**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**结构字段的说明和要求。

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
<td><p>“模式”</p></td>
<td><p>这是未使用的，必须为0。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/步骤</p></td>
<td><p>最小/最大/步骤包含 Q16 格式的相机驱动程序所支持的缩放比率的最小/最大/增量。 驱动程序必须为 <strong>GET</strong> 操作返回这些值。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>对于 <strong>SET</strong> 操作，VideoProc 必须指定最小/最大值/步骤参数描述的范围内的缩放比例。 对于 <strong>GET</strong> 操作，驱动程序必须返回当前的缩放比例。</p></td>
</tr>
<tr class="even">
<td><p>保留</p></td>
<td><p>这是未使用的。 驱动程序必须忽略此情况。</p></td>
</tr>
</tbody>
</table>

此属性控件是同步的，不可取消。

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