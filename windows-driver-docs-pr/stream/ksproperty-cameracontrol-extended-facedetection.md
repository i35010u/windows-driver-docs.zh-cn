---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FACEDETECTION
description: KSPROPERTY\_CAMERACONTROL\_扩展\_FACEDETECTION 是用于打开和关闭人脸检测的属性 ID。
ms.assetid: F503939D-D6EF-47BD-855B-4404E1AAA15C
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEDETECTION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEDETECTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2d25c6cd9ac4798ed38b14c49d146286b6cc577e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843235"
---
# <a name="ksproperty_cameracontrol_extended_facedetection"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FACEDETECTION

KSPROPERTY\_CAMERACONTROL\_扩展\_FACEDETECTION 是用于打开和关闭人脸检测的属性 ID。

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

以下标志可以放置在 KSCAMERA\_EXTENDEDPROP\_标头中。用于控制驱动程序中的人脸检测的标志字段。 默认情况下，驱动程序的\_FACEDETECTION 应为 OFF。

```cpp
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF             0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW         0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_VIDEO           0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_PHOTO           0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK           0x0000000000000008
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE           0x0000000000000010
```

如果驱动程序支持此控件，则它必须支持 FACEDETECTION\_OFF 和 FACEDETECTION\_PREVIEW、FACEDETECTION\_视频或 FACEDETECTION\_照片。 该驱动程序应该进一步执行市场上的人脸分析，并在启用面部检测时直接将占太多的人脸送到3A。

如果驱动程序不支持人脸检测，驱动程序不应实现此控制。

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
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF</p></td>
<td><p>这是必需的功能。 指定时，驱动程序将禁用人脸检测。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW</p></td>
<td><p>这是一个可选功能。 指定时，将在驱动程序中启用人脸检测，驱动程序必须提供人脸信息和关联的时间戳（如果支持）作为通过预览 pin 的元数据。 此标志与 OFF 标志互相排斥，可与其他标志一起使用。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_VIDEO</p></td>
<td><p>此功能是可选的。 指定时，驱动程序中会启用人脸检测，支持此类功能的驱动程序必须提供人脸信息以及支持的时间戳（如果支持，则为通过视频 pin 的元数据）。 此标志与 OFF 标志互相排斥，可与其他标志一起使用。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_PHOTO</p></td>
<td><p>此功能是可选的。 指定时，驱动程序中会启用人脸检测，支持此类功能的驱动程序必须提供人脸信息以及支持的时间戳（如果支持，则为通过照片 pin 的元数据）。 此标志与 OFF 标志互相排斥，可与其他标志一起使用。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK</p></td>
<td><p>此功能是可选的。 仅当指定了预览、视频、和/或照片标记时，才能指定此标志。 如果指定此功能，则支持此类功能的驱动程序还必须通过相应的 pin 将闪烁信息作为元数据提供。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE</p></td>
<td><p>此功能是可选的。 仅当指定了预览、视频、和/或照片标记时，才能指定此标志。 如果指定此功能，则支持此类功能的驱动程序还必须通过相应的 pin 将笑脸信息作为元数据提供。</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> MFT0 应进一步将人脸信息附加为 MF\_捕获\_元数据\_FACEROIS、作为 MF 的时间戳\_捕获\_的元数据\_FACEROITIMESTAMPS，并将信息闪烁和/或视为 MF\_捕获示例\_FACEROICHARACTERIZATIONS\_元数据。
> 预览、视频和照片功能是可选的。 但是，如果支持此控件，则至少必须支持预览、视频和照片功能中的一种。

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
<td><p>必须是 KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF）。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING）。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是前面定义的受支持的 KSCAMERA_EXTENDEDPROP_FACEDETECTION_ * 标志的按位 "或"。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可能是你在上面定义的 KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF/预览/视频/照片标志，或具有以下任意组合的比特率或 KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK 和/或 KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILEKSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW/视频/照片标志。</p></td>
</tr>
</tbody>
</table>

下表包含了 KSCAMERA\_\_EXTENDEDPROP 的说明和要求 KSPROPERTY\_CAMERACONTROL\_扩展\_FACEDETECTION 属性。 此结构在 Ksmedia 中定义。

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
<td><p>“模式”</p></td>
<td><p>用. 必须为0。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/步骤</p></td>
<td><p>最小/最大/步骤包含照相机驱动程序可以检测或搜索的面部数量的最小/最大/增量，其中最小值必须为 &gt;= 1，步骤必须为1。 对于 GET 操作，驱动程序必须返回这些。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>如果在<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>的 "标志" 字段中指定了<strong>FACEDETECTION_PREVIEW</strong>、 <strong>FACEDETECTION_VIDEO</strong>或<strong>FACEDETECTION_PHOTO</strong> ，<strong>则必须同时</strong>指定驱动程序应搜索的面部面。</p>
<p>如果为 SET 操作指定了 FACEDETECTION_OFF，则将忽略 VideoProc 字段。</p>
<p>对于 GET 操作，驱动程序必须返回驱动程序当前正在搜索的最大面部数。 如果面部检测处于关闭状态，则应返回0。</p></td>
</tr>
<tr class="even">
<td><p>保留</p></td>
<td><p>这是未使用的。 驱动程序必须忽略此情况。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

当人脸检测启用时，可直接通过驱动程序使用人脸区域（ROIs）来帮助进行3A 处理。 如果通过 KSPROPERTY\_CAMERACONTROL 配置了任何用户指定的 ROIs\_\_投资回报\_ISPCONTROL，则指定 ROIs 的用户将优先于检测到的人脸 ROIs。 如果清除了用户指定的 ROIs，则检测到的人脸 ROIs 会生效。

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
