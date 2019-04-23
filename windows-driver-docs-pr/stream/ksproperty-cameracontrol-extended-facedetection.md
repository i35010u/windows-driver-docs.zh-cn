---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FACEDETECTION
description: KSPROPERTY\_CAMERACONTROL\_扩展\_FACEDETECTION 是用于打开和关闭人脸检测的属性 ID。
ms.assetid: F503939D-D6EF-47BD-855B-4404E1AAA15C
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEDETECTION 流式处理媒体设备
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
ms.openlocfilehash: 12ec1ae5972e0290528bbea782e8cadc8f1699fe
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902835"
---
# <a name="kspropertycameracontrolextendedfacedetection"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FACEDETECTION

KSPROPERTY\_CAMERACONTROL\_扩展\_FACEDETECTION 是用于打开和关闭人脸检测的属性 ID。

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

以下标志可放置在 KSCAMERA\_EXTENDEDPROP\_标头。标记字段以控制驱动程序中的人脸检测。 默认情况下，该驱动程序应具有 FACEDETECTION\_OFF。

```cpp
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF             0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW         0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_VIDEO           0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_PHOTO           0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK           0x0000000000000008
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE           0x0000000000000010
```

如果该驱动程序支持此控件，它必须支持 FACEDETECTION\_OFF 和任一 FACEDETECTION\_预览、 FACEDETECTION\_视频或 FACEDETECTION\_照片。 驱动程序应进一步执行主要人脸分析和源主要人脸到 3A 直接启用人脸检测。

如果该驱动程序不支持人脸检测，该驱动程序不应实现此控件。

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
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF</p></td>
<td><p>这是必需的功能。 指定时，人脸检测被禁用驱动程序中。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW</p></td>
<td><p>这是可选功能。 指定时，驱动程序中启用了人脸检测和驱动程序必须提供的人脸信息，以及相关如果支持，作为通过预览针元数据的时间戳。 此标志与 OFF 标志互斥，可以用于其他标志。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_VIDEO</p></td>
<td><p>此功能是可选的。 指定时，驱动程序中启用了人脸检测和驱动程序支持此类功能必须提供的人脸信息，以及相关如果支持，作为通过视频 pin 元数据的时间戳。 此标志与 OFF 标志互斥，可以用于其他标志。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_PHOTO</p></td>
<td><p>此功能是可选的。 指定时，驱动程序中启用了人脸检测和驱动程序支持此类功能必须提供的人脸信息，以及相关如果支持，作为通过照片 pin 元数据的时间戳。 此标志与 OFF 标志互斥，可以用于其他标志。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK</p></td>
<td><p>此功能是可选的。 指定预览版中，视频中，和/或照片标志时，可以仅指定此标志。 指定时，驱动程序支持此类功能必须作为元数据通过对应的插针此外提供闪烁一次信息。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE</p></td>
<td><p>此功能是可选的。 指定预览版中，视频中，和/或照片标志时，可以仅指定此标志。 指定时，驱动程序支持此类功能必须此外提供笑脸信息作为元数据通过相应的 pin。</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> MFT0 应进一步将附加的人脸信息作为 MF\_捕获\_元数据\_FACEROIS，时间戳，MF\_捕获\_元数据\_FACEROITIMESTAMPS，和闪烁和/或微笑信息作为 MF\_捕获\_元数据\_FACEROICHARACTERIZATIONS 示例。
> 预览、 视频和照片是可选的功能。 但是，在至少一个预览、 视频和照片功能必须支持此控件支持。

下表包含的说明和要求[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段时使用的控件。

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
<td><p>这必须是 1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>必须是 KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING)。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是支持 KSCAMERA_EXTENDEDPROP_FACEDETECTION_ * 标志上面定义的按位 OR。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以与任何组合的是，上面定义的 KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF/预览/视频/照片标志或位 OR 的 KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK 位 OR 和/或 KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILEKSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW/视频/照片的标志。</p></td>
</tr>
</tbody>
</table>

下表包含的说明和要求 KSCAMERA\_EXTENDEDPROP\_KSPROPERTY VIDEOPROCSETTING 结构字段\_CAMERACONTROL\_扩展\_FACEDETECTION 属性。 此结构在 Ksmedia.h 中定义。

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
<td><p>未使用。 必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>最小值/最大/步骤</p></td>
<td><p>最小值/最大/步骤包含最小值/最大/增量的照相机的驱动程序可检测到或中最小值必须是搜索的实际面部数&gt;= 1 和步骤都必须是 1。 驱动程序必须返回它们的 GET 操作。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>如果<strong>FACEDETECTION_PREVIEW</strong>， <strong>FACEDETECTION_VIDEO</strong>或<strong>FACEDETECTION_PHOTO</strong>中的标志字段指定<strong>KSCAMERA_EXTENDEDPROP_标头</strong>， <strong>VideoProc.Value.ul</strong>还必须指定驱动程序应搜索的人脸的最大数目。</p>
<p>如果指定 FACEDETECTION_OFF，则为设置操作，则忽略 VideoProc 字段。</p>
<p>对于 GET 操作，则驱动程序必须返回当前搜索驱动程序的人脸的最大数目。 如果人脸检测为 OFF，则返回 0。</p></td>
</tr>
<tr class="even">
<td><p>保留</p></td>
<td><p>这是未使用。 这必须忽略由驱动程序。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

人脸检测打开时，可以直接由驱动程序，以帮助 3A 处理，根据需要使用兴趣 (ROIs) 的人脸区域。 如果指定任何用户，ROIs 配置通过 KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_ISPCONTROL 在相同时，用户指定的投资回报率将优先于人脸检测到的投资回报率。 如果用户指定的投资回报率将被清除，人脸检测到的投资回报率将会生效。

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
