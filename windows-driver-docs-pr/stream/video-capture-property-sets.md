---
title: 视频捕获属性集
description: 视频捕获属性集
ms.assetid: 23f61735-ae04-4143-8bd5-b713a2ab0e90
keywords:
- 视频捕获 WDK AVStream，属性设置
- 捕获视频 WDK AVStream，属性设置
- 属性集 WDK 视频捕获
- 硬件属性集 WDK 视频捕获
- 流属性设置 WDK 视频捕获
- 范围 WDK 视频捕获
- 默认视频捕获属性设置 WDK AVStream
- 捕获 WDK 视频捕获的属性集
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: e3f0fecbe54d01fbb80b6aa6a60e632ee47e4cbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519500"
---
# <a name="video-capture-property-sets"></a>视频捕获属性集


视频捕获属性集组相关的设备和流的属性。 只要有可能，微型驱动程序应实现中定义的标准属性集*ksmedia.h*标头文件，如[KSPROPSETID\_Pin](kspropsetid-pin.md)和[PROPSETID\_分配器\_控制](propsetid-allocator-control.md)。 微型驱动程序应避免定义新的属性集，如果标准属性组的一组提供相同的功能。

用户模式应用程序通常调用 COM 接口来控制属性设置。 COM 接口，然后发送和接收流并适配器属性设置为通过 Win32 微型驱动程序**DeviceIoControl** API。 每个属性集的参考页介绍了用户模式应用程序调用来控制流式处理的设置该属性的内核的 COM 接口。

具体取决于哪个内核流式处理接口微型驱动程序使用 （AVStream 或 Stream 类），微型驱动程序指定视频捕获属性设置，它支持以不同的方式。 例如，如果微型驱动程序使用 AVStream 接口，然后它指定其属性在递归层次结构中封装[ **KSPROPERTY\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)结构。 如果微型驱动程序使用 Stream 类接口，则它指定在其属性[ **HW\_流\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_header)结构。 Microsoft 定义多个驱动程序开发人员可用于指定其微型驱动程序支持，而不考虑流式处理的接口及其微型驱动程序使用的内核的属性的宏。

有关如何支持属性和属性集，如果你的微型驱动程序使用 AVStream 接口的详细信息，请参阅[AVStream 以筛选器为中心的模拟捕获驱动程序 (Avssamp)](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/avssamp)和[AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/avshws)示例在 GitHub 上的 Windows 驱动程序示例存储库中的微型驱动程序。

有关如何支持属性和属性集，如果你的微型驱动程序使用 Stream 类接口的详细信息，请参阅[支持属性设置](supporting-property-sets.md)。

### <a name="hardware-and-stream-property-sets"></a>硬件和 Stream 属性集

属性集归类为属于硬件或特定的流。 硬件属性集应用于所有设备，并且会影响所有流。 例如， [PROPSETID\_VIDCAP\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)，用于定位照相机，会影响所有输出流，因此归类为硬件属性集。 请注意，某些属性设置，如[PROPSETID\_VIDCAP\_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)，它可以控制在单个输出流的压缩行为实现为包括硬件属性集特定的流的索引。 需要此方法，因为未连接 pin 时，流属性集是不可用。 硬件属性集将始终可用。

下表列出了通过视频捕获微型驱动程序使用的主属性集。 它还指示属性是否设置会影响视频捕获硬件或单个视频捕获的流。 该列表还指明微型驱动程序所需实现的属性集。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性集</th>
<th>硬件属性集</th>
<th>视频捕获属性集</th>
<th>必需</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="propsetid-allocator-control.md" data-raw-source="[PROPSETID_ALLOCATOR_CONTROL](propsetid-allocator-control.md)">PROPSETID_ALLOCATOR_CONTROL</a></p></td>
<td></td>
<td><p>Y</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-tuner.md" data-raw-source="[PROPSETID_TUNER](propsetid-tuner.md)">PROPSETID_TUNER</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><a href="propsetid-vidcap-cameracontrol.md" data-raw-source="[PROPSETID_VIDCAP_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)">PROPSETID_VIDCAP_CAMERACONTROL</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-vidcap-crossbar.md" data-raw-source="[PROPSETID_VIDCAP_CROSSBAR](propsetid-vidcap-crossbar.md)">PROPSETID_VIDCAP_CROSSBAR</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><a href="propsetid-vidcap-droppedframes.md" data-raw-source="[PROPSETID_VIDCAP_DROPPEDFRAMES](propsetid-vidcap-droppedframes.md)">PROPSETID_VIDCAP_DROPPEDFRAMES</a></p></td>
<td></td>
<td><p>Y</p></td>
<td><p>Y</p></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-vidcap-tvaudio.md" data-raw-source="[PROPSETID_VIDCAP_TVAUDIO](propsetid-vidcap-tvaudio.md)">PROPSETID_VIDCAP_TVAUDIO</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><a href="propsetid-vidcap-videocompression.md" data-raw-source="[PROPSETID_VIDCAP_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)">PROPSETID_VIDCAP_VIDEOCOMPRESSION</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-vidcap-videocontrol.md" data-raw-source="[PROPSETID_VIDCAP_VIDEOCONTROL](propsetid-vidcap-videocontrol.md)">PROPSETID_VIDCAP_VIDEOCONTROL</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><a href="propsetid-vidcap-videodecoder.md" data-raw-source="[PROPSETID_VIDCAP_VIDEODECODER](propsetid-vidcap-videodecoder.md)">PROPSETID_VIDCAP_VIDEODECODER</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-vidcap-videoprocamp.md" data-raw-source="[PROPSETID_VIDCAP_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)">PROPSETID_VIDCAP_VIDEOPROCAMP</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

 

至少，微型驱动程序必须报告期间捕获上表中所述的丢帧数。 支持的所有其他属性集是可选的具体取决于设备的功能。 强烈建议相机、 产品/服务仅一组有限的捕获的帧速率，实现[PROPSETID\_VIDCAP\_VIDEOCONTROL](propsetid-vidcap-videocontrol.md)允许视频会议应用程序进行优化系统带宽的使用。

### <a name="property-set-default-values-and-ranges"></a>属性设置默认值和范围

默认值和范围，可以支持属性。 用户界面元素，如滑块和滚动条，使用此信息，如下图中所示。

![显示用户界面元素，如滑块和滚动条，如何使用默认值和范围属性对话框的屏幕截图](images/vcuiprop.gif)

中提供的默认值和范围信息[ **KSPROPERTY\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_values)结构，它是属性定义的一部分。 此结构包含一个指向包含一个或多个静态表[ **KSPROPERTY\_MEMBERSLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_memberslist)结构实例。 在 KSPROPERTY\_MEMBERSLIST 结构微型驱动程序可以指定默认值或一系列值。 可以通过最小值、 最大和单步执行值指定的值范围。 设置**MembersFlags**的成员[ **KSPROPERTY\_MEMBERSHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_membersheader) KSPROPERTY 结构\_成员\_范围值，指示 KSPROPERTY\_MEMBERSLIST 结构是一系列值。 KSPROPERTY\_MEMBERSLIST 结构还用于指定该属性的默认值。 这是通过设置**MembersFlags** KSPROPERTY 成员\_MEMBERSHEADER 到 KSPROPERTY\_成员\_值值。

 

 




