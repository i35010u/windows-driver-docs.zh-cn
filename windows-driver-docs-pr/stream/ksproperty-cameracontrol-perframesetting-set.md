---
title: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_集
description: KSPROPERTY 中定义的 KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_设置属性 ID\_CAMERACONTROL\_PERFRAMESETTING\_属性用于设置驱动程序中的每帧设置。
ms.assetid: 2EFBEA64-8340-4367-A56B-2C46167F0DE5
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_SET 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_SET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f291028350a415bf16d41c2fa0b0710b13964db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843340"
---
# <a name="ksproperty_cameracontrol_perframesetting_set"></a>KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_集

KSPROPERTY 中定义的**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_集**属性 ID [ **\_CAMERACONTROL\_PERFRAMESETTING\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property)用于设置中的每帧设置驱动器.

## <a name="usage-summary"></a>使用情况摘要

若要设置每帧设置，请将**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_设置**属性控制发送到驱动程序以及每帧设置负载。

此属性可读写。 尽管可以使用**get**调用来返回驱动程序上设置的最后一个每帧设置，但**get**调用不会公开给应用客户端，而只会在由 MF 管道构造每帧设置控制时在初始化时发出，其中，驱动程序必须返回**状态\_缓冲区\_溢出**，缓冲区大小为0。

在 GET 调用中，将先向驱动程序发送零长度缓冲区，以找出所需的数据缓冲区大小来保存驱动程序具有的整个每帧设置。 对于此调用，驱动程序必须返回**状态\_缓冲区\_溢出**，其中包含所需的每帧设置缓冲区大小（如果以前未设置每帧设置或至少 KSCAMERA 大小，则必须为0） [ **\_否则，PERFRAMESETTING\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_header)。

每帧设置负载必须以**KSCAMERA\_PERFRAMESETTING\_标头**开始，后跟一个或多个框架设置。 在 FrameCount 中指定帧设置的数目。 每个帧的设置必须以[**KSCAMERA\_PERFRAMESETTING\_帧\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_frame_header)开头，后跟零个或多个项设置。 在 ItemCount 中指定项设置的数目。 每个项目的设置（如果有）必须以[**KSCAMERA\_PERFRAMESETTING\_item\_页眉**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_item_header)开头。

对于每个项的设置，如果存在值有效负载，则**KSCAMERA\_PERFRAMESETTING\_item\_标头**必须后跟[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)。 如果自定义项存在，则**KSCAMERA\_PERFRAMESETTING\_item\_标头**必须后跟[**KSCAMERA\_PERFRAMESETTING\_自定义\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_custom_item)，后跟 GUID Id 关联的自定义数据在**KSCAMERA\_PERFRAMESETTING 中指定\_自定义\_项**。

如果 FrameCount 为0，则驱动程序必须拒绝每帧设置负载。 如果 ItemCount 为0，则不指定帧设置。 驱动程序必须将全局设置应用于关联的帧。 例如，FrameCount = 1，ItemCount = 0 表示具有全局设置的单个帧可变照片序列。

下图演示了每帧设置负载配置的数据结构布局。 在下面的示例中，四个帧的每帧设置都配置了帧0，其中包含三个项，两个没有负载，另一个具有值负载;第1帧包含两项，其中一个没有负载，另一个具有值负载;第2帧包含0项，这意味着第2帧的全局设置;第3帧包含四项，其中一个具有值负载，两个项具有自定义项和自定义数据负载，而一个没有负载。

![perframesetting\-标头的结构](images/oem-perframesettings-header-payload-datastructure.png)

1.  **"按帧设置的大小" 标头**表示要在**KSCAMERA\_PERFRAMESETTING\_标头中填充的总负载大小。大小**

2.  **"按帧设置的大小" 框**表示要在**KSCAMERA\_PERFRAMESETTING\_帧\_标头中填充的大小。** 帧的大小。

3.  **项大小**表示要在**KSCAMERA\_PERFRAMESETTING\_项\_标题中填充的大小。** 项的大小。

4.  **自定义项大小**表示要在**KSCAMERA\_PERFRAMESETTING\_自定义\_项中填充的大小。** 自定义项的大小。

**每帧设置的曝光时间**

如果按帧设置指定了手动曝光时间，则**KSCAMERA\_EXTENDEDPROP\_值。值。** 将包含在**集**调用中所需的公开时间和在**GET**调用中使用的当前曝光时间。

**每帧设置补偿**

如果在 "每帧设置" 中指定手动设置补偿，则**KSCAMERA\_EXTENDEDPROP\_值。值. l**将包含在**集合**调用中所需的曝光补偿，以及在**GET**调用中使用的当前曝光补偿。

**每帧设置焦点**

如果每帧设置中指定了 "每帧手动设置"，则**KSCAMERA\_EXTENDEDPROP\_"值。值 ul**将包含在**集合**调用中所需的镜头位置，以及在**GET**调用中使用的当前镜头位置。

**每帧设置 ISO**

如果驱动程序不支持**KSCAMERA\_EXTENDEDPROP\_ISO\_"手动**"，则不会包括值负载。 否则，每帧设置的项标头必须后跟一个**KSCAMERA\_EXTENDEDPROP\_值**。 在**SET**调用中， **KSCAMERA\_EXTENDEDPROP\_值。** 如果支持 **\_EXTENDEDPROP\_ISO\_** \_，则值 ul 包含所需的 iso 速度**KSCAMERA PERFRAMESETTING\_项\_标头。标志**。

下面演示了在每帧设置 ISO 功能**KSCAMERA\_EXTNDEDPROP\_iso\_AUTO**， **KSCAMERA\_EXTENDEDPROP\_ISO\_手动时项标头和值负载的外观**（最小 = 30，最大 = 210，步骤 = 20），如下所示：

```cpp
KSCAMERA_EXTNDEDPROP_ISO_AUTO, 
KSCAMERA_EXTENDEDPROP_ISO_MANUAL (min = 30, max = 210, step =20)
```

1.  如果 ISO 速度为70

    ```cpp
    KSCAMERA_PERFRAMESETTING_ITEM_HEADER.Flags = KSCAMERA_EXTENDEDPROP_ISO_MANUAL
    KSCAMERA_EXTENDEDPROP_VALUE.Value.ul = 70
    ```

2.  如果 ISO 速度为50

    ```cpp
    KSCAMERA_PERFRAMESETTING_ITEM_HEADER.Flags = KSCAMERA_EXTENDEDPROP_ISO_MANUAL
    KSCAMERA_EXTENDEDPROP_VALUE.Value.ul = 50
    ```

下表汇总了每帧设置的可用控件和值。 实际的可用性取决于驱动程序的实际功能，可使用[**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能**](ksproperty-cameracontrol-perframesetting-capability.md)获得。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>可用值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>曝光时间</p></td>
<td><p>100毫微秒内的自动或时间。</p></td>
</tr>
<tr class="even">
<td><p>Flash</p></td>
<td><p>开启/关闭，自动，红眼降低/关闭，闪烁电量百分比。</p></td>
</tr>
<tr class="odd">
<td><p>曝光补偿</p></td>
<td><p>自动或补偿步骤值。</p></td>
</tr>
<tr class="even">
<td><p>ISO 感光度</p></td>
<td><p>用整数 ISO 值自动或手动。</p></td>
</tr>
<tr class="odd">
<td><p>对焦</p></td>
<td><p>自动或逻辑镜头位置。 此值没有特定的单位。</p></td>
</tr>
<tr class="even">
<td><p>自定义属性</p></td>
<td><p>OEM 使用自定义 GUID 和属性数据定义此。</p></td>
</tr>
<tr class="odd">
<td><p>确认图像</p></td>
<td><p>打开/关闭</p></td>
</tr>
</tbody>
</table>

若要将自定义属性数据传入每帧设置，应用会执行以下操作：

1.  调用 IFrameSettingsControls 上的 QueryInterface 以获取与每帧设置关联的 IMFGetServices 接口。

2.  从 IMFGetServices 接口调用 GetService，以在每帧设置上创建自定义 IMFAttributes 接口。

3.  对自定义属性 GUID 调用 SetUINT32、SetBlob 等，以设置与每帧设置关联的 IMFAttributes 上的自定义属性数据。

当组装要在驱动程序上设置的每帧设置负载时，框架将查找自定义 IMFAttributes 以构造自定义项负载。

**KSCAMERA\_PERFRAMESETTING\_标头**中的**LoopCount**字段指定了每帧设置应应用于要在照片序列中捕获的未来帧的重复次数。 管道将**LoopCount**硬编码为1（例如，每帧设置仅应用一次，无需进一步重复）。 **KSCAMERA\_PERFRAMESETTING\_标头**中的**FrameCount**字段指定每个帧设置应应用于每个重复的帧的帧设置的数目。

**KSCAMERA\_PERFRAMESETTING\_FRAME\_标头**中的**ItemCount**字段指定应用于相应帧的项设置的数目。 如果**ItemCount**为0，则全局设置应应用于相应的帧。

下表列出了可能的配置和相应的照片序列类型。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>LoopCount</th>
<th>FrameCount</th>
<th>ItemCount</th>
<th>在任务栏的搜索框中键入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>L （L = 1）</p></td>
<td><p>N （N&gt;0）</p></td>
<td><p>S （&gt;= 0）</p></td>
<td><p>有限可变照片序列</p></td>
</tr>
<tr class="even">
<td><p>L （L = 1）</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>具有全局设置的一帧有限变量照片序列</p></td>
</tr>
<tr class="odd">
<td><p>L （L = 1）</p></td>
<td><p>0</p></td>
<td><p>S</p></td>
<td><p>配置无效</p></td>
</tr>
</tbody>
</table>

可变照片序列已简化，只需要一个重复操作即可执行有限捕获。 每帧设置的照片序列将始终标记为可变照片序列，且始终需要每帧设置负载。

如果循环计数为 L （L = 1），并且帧计数为 N （N &gt; 0），则它是一个有限的可变照片序列。 每帧设置将重复 L = 1 次，并在每次重复后，将 N 帧设置应用于接下来的第 N 个未来帧。

如果循环计数为 L （L = 1），则帧计数为1，项计数为0，它是具有全局设置的一种帧有限变量照片序列。

可变照片序列会进一步简化，以不请求任何过去的帧。 管道会将请求的过去照片计数（例如，RequestedHistoryFrames）硬编码为0。 驱动程序仅在可变照片序列中提供未来的帧。 下图说明了驱动程序在可变照片序列中传递的预期帧数。 过去的照片计数是在**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE 中指定的。RequestedHistoryFrames** By [**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE**](ksproperty-cameracontrol-extended-photomode2.md)扩展属性控件，该控件由管道硬编码为0。

```cpp
N : Frame Count
L : Loop Count
P : Past Photos Requested
T : Total number of frame delivered by driver
L = 1
P = 0
T = (N * L) + P
```

对于有限可变照片序列，驱动程序必须将 KSSTREAM 标记为 " **\_"。** **KSSTREAM\_标题\_OPTIONSF\_ENDOFPHOTOSEQUENCE**标志的最后一帧的 OptionsFlags。 这样做可确保在交付预期的未来帧量后，驱动程序会自动停止将帧传递回 MF 管道。 这会有效地停止照片序列并通知应用客户端照片序列完成。 当驱动程序完成捕获有限可变照片序列中的最后帧时，会发生这种情况。

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
