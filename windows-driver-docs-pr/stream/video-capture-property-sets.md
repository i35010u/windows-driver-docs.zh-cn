---
title: 视频捕获属性集
description: 视频捕获属性集
ms.assetid: 23f61735-ae04-4143-8bd5-b713a2ab0e90
keywords:
- 视频捕获 WDK AVStream，属性集
- 捕获视频 WDK AVStream，属性集
- 属性集 WDK 视频捕获
- 硬件属性设置 WDK 视频捕获
- 流属性设置 WDK 视频捕获
- 范围 WDK 视频捕获
- 默认视频捕获属性设置 WDK AVStream
- 捕获属性集 WDK 视频捕获
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae901aebc8986487c0550ff4d608e6153e01c640
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844932"
---
# <a name="video-capture-property-sets"></a>视频捕获属性集


视频捕获属性用于设置设备和流的与组相关的属性。 微型驱动程序应尽可能实现*ksmedia*头文件中定义的标准属性集，如[KSPROPSETID\_固定](kspropsetid-pin.md)和[PROPSETID\_分配器\_控制](propsetid-allocator-control.md)。 如果某个标准属性集提供相同的功能，则微型驱动程序应避免定义新的属性集。

用户模式应用程序通常调用 COM 接口来控制属性设置。 然后，COM 接口通过 Win32 **DeviceIoControl** API 向微型驱动程序发送流和适配器属性集。 每个属性集的参考页描述了用户模式应用程序调用以控制该集的内核流式处理属性的 COM 接口。

根据微型驱动程序使用的内核流式处理接口（AVStream 或 Stream 类），微型驱动程序指定其支持方式不同的视频捕获属性集。 例如，如果微型驱动程序使用 AVStream 接口，则它将在[**KSPROPERTY\_集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)结构中封装的递归层次结构中指定其属性。 如果微型驱动程序使用 Stream 类接口，则它会在[**HW\_Stream\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)结构中指定其属性。 Microsoft 定义了多个宏，驱动程序开发人员可以使用这些宏指定其微型驱动程序支持的属性，而不考虑其微型驱动程序使用的内核流式处理接口。

若要详细了解如何支持微型驱动程序使用 AVStream 接口的属性和属性集，请参阅[AVStream 筛选器中心模拟捕获驱动程序（Avssamp）](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/avssamp)和[AVStream 模拟硬件示例驱动程序（AVSHwS）](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/avshws)GitHub 上的 Windows 驱动程序示例存储库中的示例微型驱动程序。

有关在微型驱动程序使用 Stream 类接口的情况下如何支持属性和属性集的详细信息，请参阅[支持属性集](supporting-property-sets.md)。

### <a name="hardware-and-stream-property-sets"></a>硬件和流属性集

属性集归类为属于硬件或特定流。 硬件属性集适用于所有设备，并影响所有流。 例如， [PROPSETID\_VIDCAP\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)用于照相机定位，它会影响所有输出流，因而归类为硬件属性集。 请注意，某些属性集（如[PROPSETID\_VIDCAP\_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)控制单个输出流的压缩行为）是作为包含特定流的索引的硬件属性集实现的。 此方法是必需的，因为当未连接 pin 时，流属性集不可用。 硬件属性集始终可用。

下表列出了视频捕获微型驱动程序使用的主属性集。 它还指示属性集是影响视频捕获硬件，还是影响单个视频捕获流。 此列表还指示实现属性集是否需要微型驱动程序。

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

 

至少，微型驱动程序必须报告在捕获期间丢弃的帧数，如上表中所述。 所有其他属性集的支持都是可选的，具体取决于设备的功能。 强烈建议仅提供有限的捕获帧速率集的照相机，实现[PROPSETID\_VIDCAP\_VIDEOCONTROL](propsetid-vidcap-videocontrol.md) ，以允许视频会议应用程序充分利用系统带宽。

### <a name="property-set-default-values-and-ranges"></a>属性集默认值和范围

属性可以支持默认值和范围。 用户界面元素（如滑块和滚动条）使用此信息，如下图所示。

![显示用户界面元素（如滑块和滚动条）如何使用默认值和范围的 "属性" 对话框的屏幕截图](images/vcuiprop.gif)

默认值和范围信息在作为属性定义一部分的[**KSPROPERTY\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_values)结构中提供。 此结构包括一个指针，指向包含一个或多个[**KSPROPERTY\_MEMBERSLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_memberslist)结构实例的静态表。 在 KSPROPERTY\_MEMBERSLIST 结构中，微型驱动程序可以指定默认值或一系列值。 可以通过最小值、最大值和步进值指定值的范围。 将[**KSPROPERTY\_MEMBERSHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_membersheader)结构的**MembersFlags**成员设置为 KSPROPERTY\_成员\_范围值，以指示 KSPROPERTY\_MEMBERSLIST 结构是一系列值。 KSPROPERTY\_MEMBERSLIST 结构还用于指定属性的默认值。 为此，可将 KSPROPERTY\_MEMBERSHEADER 的**MembersFlags**成员设置为 KSPROPERTY\_成员\_值值。

 

 




