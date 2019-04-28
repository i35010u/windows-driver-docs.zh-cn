---
title: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_设置
description: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_KSPROPERTY 中定义的设置属性 ID\_CAMERACONTROL\_PERFRAMESETTING\_属性用于设置每个帧驱动程序中的设置。
ms.assetid: 2EFBEA64-8340-4367-A56B-2C46167F0DE5
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_SET 流式处理媒体设备
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
ms.openlocfilehash: 18fe6849e44076e1cb4ae2208ca7968099f3daa4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338364"
---
# <a name="kspropertycameracontrolperframesettingset"></a>KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_设置

**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_设置**中定义的属性 ID [ **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property)用于驱动程序中设置每个帧设置。

## <a name="usage-summary"></a>使用情况摘要

若要设置帧设置每**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_设置**属性控制发送到的驱动程序以及每个帧设置负载。

此属性可以读取或写入。 虽然**获取**调用可以用于返回每个帧设置驱动程序, 设置的最后一个**获取**调用不会公开给应用程序客户端，并在初始化时才发出时间每个帧设置控件由 MF 管道，则驱动程序必须返回构造**状态\_缓冲区\_OVERFLOW**缓冲区大小为 0。

在 GET 调用中，一个零长度缓冲区是先发送到该驱动程序来找出要保存此驱动程序存在的基于帧的整个设置的所需的数据缓冲区大小。 此调用的响应，则驱动程序必须返回**状态\_缓冲区\_OVERFLOW**具有所需的每个帧设置缓冲区大小必须为 0，如果从未设置没有每个帧的设置，或在最小大小[ **KSCAMERA\_PERFRAMESETTING\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_header)否则为。

每个帧设置有效负载必须开头**KSCAMERA\_PERFRAMESETTING\_标头**后, 跟一个或多个帧设置。 帧设置的数量 FrameCount 中指定。 每个帧的设置必须开头[ **KSCAMERA\_PERFRAMESETTING\_帧\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_frame_header)后, 跟零个或多个项设置。 ItemCount 中指定项设置的数量。 对于每个项，如果任何必须启动与设置[ **KSCAMERA\_PERFRAMESETTING\_项\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_item_header)。

设置的每个项，如果存在，则值负载**KSCAMERA\_PERFRAMESETTING\_项\_标头**后面必须跟[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)。 如果存在，自定义项，则**KSCAMERA\_PERFRAMESETTING\_项\_标头**后面必须跟[ **KSCAMERA\_PERFRAMESETTING\_自定义\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_custom_item)后, 跟与中指定的 GUID Id 关联的自定义数据**KSCAMERA\_PERFRAMESETTING\_自定义\_项**.

如果 FrameCount 为 0，驱动程序必须拒绝每个帧设置有效负载。 如果 ItemCount 为 0，则指定没有框架的设置。 该驱动程序必须应用于关联的帧的全局设置。 例如，FrameCount 1 和 ItemCount = = 0 表示使用全局设置的单个帧变量照片序列。

下图说明了数据结构布局中的每个帧设置负载配置。 在下面的示例中，四个帧的每个帧设置配置了帧 0 包含三个项、 两个不带有效负载和一个具有值的有效负载;第 1 包含两个项目，一个不带有效负载，使用值有效负载; 另一个帧帧 2 包含 0 项，这意味着帧 2; 的全局设置帧 3 包含四个项，另一个使用值负载，每个自定义项和自定义数据负载，使用两个，另一个不带有效负载。

![结构 perframesetting\-标头](images/oem-perframesettings-header-payload-datastructure.png)

1.  **每个帧设置标头中的大小**表示要填充的总负载大小**KSCAMERA\_PERFRAMESETTING\_标头。大小**

2.  **每个帧设置框架中的大小**表示要填充的大小**KSCAMERA\_PERFRAMESETTING\_帧\_标头。大小**帧。

3.  **项大小**表示要填充的大小**KSCAMERA\_PERFRAMESETTING\_项\_标头。大小**的项。

4.  **自定义项大小**表示要填充的大小**KSCAMERA\_PERFRAMESETTING\_自定义\_项。大小**自定义项。

**每个帧设置公开时间**

如果手动暴露时间中指定每个帧设置**KSCAMERA\_EXTENDEDPROP\_值。Value.ll**将包含中的所需的暴露时间**设置**调用和当前的暴露时间中使用**获取**调用。

**每个帧设置补偿**

如果每个帧设置中未指定手动设置补偿**KSCAMERA\_EXTENDEDPROP\_值。Value.l**将包含中的所需的曝光补偿**设置**调用和在中使用的当前曝光补偿**获取**调用。

**每个帧设置焦点**

如果手动/每帧设置中指定每个帧设置**KSCAMERA\_EXTENDEDPROP\_值。Value.ul**将包含中的所需的可重用功能区位置**设置**调用和当前可重用功能区中使用定位**获取**调用。

**每个帧设置 ISO**

如果该驱动程序不支持**KSCAMERA\_EXTENDEDPROP\_ISO\_手动**，则不包含值有效负载。 否则，每个帧设置项标头必须后跟**KSCAMERA\_EXTENDEDPROP\_值**。 在中**设置**调用，请**KSCAMERA\_EXTENDEDPROP\_值。Value.ul**如果包含所需的 ISO 速度**KSCAMERA\_EXTENDEDPROP\_ISO\_手动**支持并且在指定**KSCAMERA\_PERFRAMESETTING\_项\_标头。标志**。

下面演示了如何项标头和值负载应如下所示的每个帧设置 ISO 功能何时**KSCAMERA\_EXTNDEDPROP\_ISO\_自动**， **KSCAMERA\_EXTENDEDPROP\_ISO\_手动**(最小值 = 30，最大 = 210，步骤 = 20)，如下所示：

```cpp
KSCAMERA_EXTNDEDPROP_ISO_AUTO, 
KSCAMERA_EXTENDEDPROP_ISO_MANUAL (min = 30, max = 210, step =20)
```

1.  如果 ISO 速度 70

    ```cpp
    KSCAMERA_PERFRAMESETTING_ITEM_HEADER.Flags = KSCAMERA_EXTENDEDPROP_ISO_MANUAL
    KSCAMERA_EXTENDEDPROP_VALUE.Value.ul = 70
    ```

2.  如果 ISO 速度为 50

    ```cpp
    KSCAMERA_PERFRAMESETTING_ITEM_HEADER.Flags = KSCAMERA_EXTENDEDPROP_ISO_MANUAL
    KSCAMERA_EXTENDEDPROP_VALUE.Value.ul = 50
    ```

下表总结了可用的控件和每个帧设置的值。 实际可用性由驱动程序的实际功能，可以使用获取[ **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能**](ksproperty-cameracontrol-perframesetting-capability.md).

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
<td><p>暴露时间</p></td>
<td><p>自动或以 100 纳秒的时间。</p></td>
</tr>
<tr class="even">
<td><p>Flash</p></td>
<td><p>打开/关闭，自动，打开/关闭，以百分比表示的闪存 power 避免红眼。</p></td>
</tr>
<tr class="odd">
<td><p>曝光补偿</p></td>
<td><p>自动或补偿的步长值。</p></td>
</tr>
<tr class="even">
<td><p>ISO 感光度</p></td>
<td><p>自动或手动使用 ISO 的整数值。</p></td>
</tr>
<tr class="odd">
<td><p>Focus</p></td>
<td><p>自动或逻辑可重用功能区位置。 此值不具有特定的单元。</p></td>
</tr>
<tr class="even">
<td><p>自定义属性</p></td>
<td><p>OEM 定义此自定义的 GUID 和属性数据。</p></td>
</tr>
<tr class="odd">
<td><p>确认图像</p></td>
<td><p>打开/关闭</p></td>
</tr>
</tbody>
</table>

要将自定义属性数据传递到每个帧设置，该应用程序执行以下任务：

1.  IFrameSettingsControls 来获得 IMFGetServices 接口与每个帧设置关联上调用 QueryInterface。

2.  从 IMFGetServices 接口上的每个帧设置创建自定义 IMFAttributes 接口调用 GetService。

3.  调用 SetUINT32 SetBlob，自定义属性 GUID 与每个帧设置关联 IMFAttributes 上设置自定义属性数据等。

该框架将查找自定义的 IMFAttributes 构造自定义项有效负载，如果有在组装驱动程序上设置的每个帧设置有效负载。

**LoopCount**字段中**KSCAMERA\_PERFRAMESETTING\_标头**指定应为每个帧设置的重复次数应用于未来的帧为捕获照片序列中。 **LoopCount**被硬编码为 1，由管道 (例如，每帧设置将仅应用一次而无需进一步地使用重复)。 **FrameCount**字段中**KSCAMERA\_PERFRAMESETTING\_标头**指定的数，每个帧设置应应用于在每个帧的帧设置重复此操作。

**ItemCount**字段中**KSCAMERA\_PERFRAMESETTING\_帧\_标头**指定应该应用到的项设置的数量相应帧。 如果**ItemCount**为 0，则应相应帧应用全局设置。

下表列出了可能的配置以及相应的照片序列类型。

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
<td><p>L(L=1)</p></td>
<td><p>N(N&gt;0)</p></td>
<td><p>S(S&gt;=0)</p></td>
<td><p>有限变量照片序列</p></td>
</tr>
<tr class="even">
<td><p>L(L=1)</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>使用全局设置的一个帧有限变量照片序列</p></td>
</tr>
<tr class="odd">
<td><p>L(L=1)</p></td>
<td><p>0</p></td>
<td><p>S</p></td>
<td><p>无效的配置</p></td>
</tr>
</tbody>
</table>

简化了变量照片序列执行有限的捕获，而只有一个重复执行。 具有每个帧设置的照片序列将始终标记为变量照片序列和每个帧设置有效负载始终是必需。

如果循环计数为 L (L = 1)，帧计数为 N (N &gt; 0)，它是有限的变量照片序列。 将每个帧设置重复 L 与应用于每次重复时的下一步 N 将来帧的 N 帧设置 = 1 次。

如果循环计数为 L (L = 1)、 帧计数为 1，和项的计数为 0，它是具有全局设置的一个帧有限变量照片序列。

进一步简化变量照片序列以对未请求任何过往帧。 管道 (例如，RequestedHistoryFrames) 为 0 的照片计数，之后将进行硬编码请求。 该驱动程序提供仅将来帧变量照片序列中。 下图说明了预期的要传送的变量照片序列中的驱动程序的帧数。 中指定过去的照片计数**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE。RequestedHistoryFrames**由[ **KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE** ](ksproperty-cameracontrol-extended-photomode2.md)扩展属性控件进行硬编码为 0 的管道。

```cpp
N : Frame Count
L : Loop Count
P : Past Photos Requested
T : Total number of frame delivered by driver
L = 1
P = 0
T = (N * L) + P
```

对于有限变量照片序列，该驱动程序必须将标记**KSSTREAM\_标头。OptionsFlags**使用的最后一个帧**KSSTREAM\_标头\_OPTIONSF\_ENDOFPHOTOSEQUENCE**标志。 这可以确保，驱动程序会自动停止的预期将来的帧后返回到 MF 管道传送帧已传递。 这样可以有效地停止照片序列并通知完成后的照片序列应用客户端。 驱动程序完成捕获有限变量照片序列中的最后一帧时，将发生这种情况。

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
