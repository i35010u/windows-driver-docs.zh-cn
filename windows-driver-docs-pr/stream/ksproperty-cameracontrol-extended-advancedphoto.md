---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_ADVANCEDPHOTO
description: KSPROPERTY\_CAMERACONTROL\_扩展的\_ADVANCEDPHOTO 用于控制驱动程序上的相片 HDR、flash no flash 和超高亮度合成。 这是仅适用于照片 pin 的 pin 级别控制。
ms.assetid: 88C14C9E-8675-42BF-A606-64232ABD4FD1
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ADVANCEDPHOTO 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ADVANCEDPHOTO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5c33639634aa3be42a932e01fd0b7911e2bc0944
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843245"
---
# <a name="ksproperty_cameracontrol_extended_advancedphoto"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_ADVANCEDPHOTO


KSPROPERTY\_CAMERACONTROL\_扩展的\_ADVANCEDPHOTO 用于控制驱动程序上的相片 HDR、flash no flash 和超高亮度合成。 这是仅适用于照片 pin 的 pin 级别控制。

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
<td><p>大头针</p></td>
<td><p>同步</p></td>
</tr>
</tbody>
</table>

 

下面是可以放置在 KSCAMERA\_EXTENDEDPROP\_标头中的标志。用于控制照片 HDR、闪光无闪光和超高光源合成的标志字段。 默认值应为 KSCAMERA\_EXTENDEDPROP\_ADVANCEDPHOTO\_OFF。

```cpp
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_OFF             0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_AUTO            0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_HDR             0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_FNF             0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ULTRALOWLIGHT   0x0000000000000008
```

如果驱动程序支持此控件，则它必须支持 KSCAMERA\_EXTENDEDPROP\_ADVANCEDPHOTO\_OFF。

如果驱动程序不支持任何高级照片捕获，驱动程序不应实现此控制。

当照片 pin KSSTATE\_运行状态时，此控件的设置调用不起作用。 如果照片 pin 处于运行状态并且返回状态\_无效\_设备\_状态，则驱动程序应拒绝收到的设置呼叫。 在 GET 调用中，驱动程序应返回 "标志" 字段中的当前设置。

下表介绍了标志功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>旗帜</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_OFF</p></td>
<td><p>这是必需的功能。 如果指定此项，则不应在该驱动程序中执行高级照片。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_AUTO</p></td>
<td><p>此功能是可选的。 如果单独指定，则支持此类功能的驱动程序将根据场景分析来确定是否应执行 photo HDR、Flash no Flash 或超高光源合成。 此标志与 OFF 标志互相排斥，可与其他标志一起使用。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_HDR</p></td>
<td><p>此功能是可选的。 如果单独指定，则支持此类功能的驱动程序将执行照片 HDR。 此标志与 AUTO 以外的其他标志互相排斥。 当指定为 "自动" 时，驱动程序将根据场景分析来确定是否应执行照片 HDR。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_FNF</p></td>
<td><p>此功能是可选的。 如果单独指定，则支持此类功能的驱动程序将不会执行闪存。 此标志与 AUTO 以外的其他标志互相排斥。 当指定为 "自动" 时，驱动程序将根据场景分析来确定是否应执行闪存。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ULTRALOWLIGHT</p></td>
<td><p>此功能是可选的。 如果单独指定，则支持此类功能的驱动程序将执行超高的轻型合成。 此标志与 AUTO 以外的其他标志互相排斥。 当指定为 "自动" 时，驱动程序将根据场景分析来确定是否应执行超低压负载。</p></td>
</tr>
</tbody>
</table>

 

下表包含使用控件时[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。

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
<td><p>版本</p></td>
<td><p>这必须为1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>必须是与照片 Pin 关联的 Pin ID。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE）。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是前面定义的受支持的 KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ * 标志的按位 "或"。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的 KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ * 标志之一。</p></td>
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
