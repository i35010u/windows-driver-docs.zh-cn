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
ms.openlocfilehash: 467ba6f8a73665367a22a1658b8e6c5aa9b43f37
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184335"
---
# <a name="video-capture-property-sets"></a>视频捕获属性集

视频捕获属性用于设置设备和流的与组相关的属性。 微型驱动程序应尽可能实现 *ksmedia* 头文件中定义的标准属性集，如 [KSPROPSETID \_ Pin](kspropsetid-pin.md) 和 [PROPSETID \_ 分配器 \_ 控件](propsetid-allocator-control.md)。 如果某个标准属性集提供相同的功能，则微型驱动程序应避免定义新的属性集。

用户模式应用程序通常调用 COM 接口来控制属性设置。 然后，COM 接口通过 Win32 **DeviceIoControl** API 向微型驱动程序发送流和适配器属性集。 每个属性集的参考页描述了用户模式应用程序调用以控制该集的内核流式处理属性的 COM 接口。

根据微型驱动程序使用 (AVStream 或 Stream 类) 的内核流式处理接口，微型驱动程序指定其支持方式不同的视频捕获属性集。 例如，如果微型驱动程序使用 AVStream 接口，则它在封装在 [**KSPROPERTY \_ 集**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set) 结构中的递归层次结构中指定其属性。 如果微型驱动程序使用 Stream 类接口，则它会在 [**HW \_ 流 \_ 标题**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header) 结构中指定其属性。 Microsoft 定义了多个宏，驱动程序开发人员可以使用这些宏指定其微型驱动程序支持的属性，而不考虑其微型驱动程序使用的内核流式处理接口。

若要详细了解微型驱动程序使用 AVStream 接口时，如何支持属性和属性集，请参阅 GitHub 上 Windows 驱动程序示例存储库中的 [AVStream 筛选器中心模拟捕获)  (驱动 ](/samples/microsoft/windows-driver-samples/avstream-filter-centric-simulated-capture-sample-driver-avssamp/) 程序 [ (AVStream) ](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/) 示例 AVSHwS。

有关在微型驱动程序使用 Stream 类接口的情况下如何支持属性和属性集的详细信息，请参阅 [支持属性集](supporting-property-sets.md)。

## <a name="hardware-and-stream-property-sets"></a>硬件和流属性集

属性集归类为属于硬件或特定流。 硬件属性集适用于所有设备，并影响所有流。 例如， [PROPSETID \_ VIDCAP \_ CAMERACONTROL](propsetid-vidcap-cameracontrol.md)，用于照相机定位，影响所有输出流，因而归类为硬件属性集。 请注意，某些属性集（如 [PROPSETID \_ VIDCAP \_ VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)）用于控制单个输出流的压缩行为，作为包含特定流的索引的硬件属性集实现。 此方法是必需的，因为当未连接 pin 时，流属性集不可用。 硬件属性集始终可用。

下表列出了视频捕获微型驱动程序使用的主属性集。 它还指示属性集是影响视频捕获硬件，还是影响单个视频捕获流。 此列表还指示实现属性集是否需要微型驱动程序。

| 属性集 | 硬件属性集 | 视频捕获属性集 | 必须 |
| --- | --- | --- | --- |
| [PROPSETID_ALLOCATOR_CONTROL](propsetid-allocator-control.md) |  | Y |  |
| [PROPSETID_TUNER](propsetid-tuner.md) | Y |  |  |
| [PROPSETID_VIDCAP_CAMERACONTROL](propsetid-vidcap-cameracontrol.md) | Y |  |  |
| [PROPSETID_VIDCAP_CROSSBAR](propsetid-vidcap-crossbar.md) | Y |  |  |
| [PROPSETID_VIDCAP_DROPPEDFRAMES](propsetid-vidcap-droppedframes.md) |  | Y | Y |
| [PROPSETID_VIDCAP_TVAUDIO](propsetid-vidcap-tvaudio.md) | Y |  |  |
| [PROPSETID_VIDCAP_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md) | Y |  |  |
| [PROPSETID_VIDCAP_VIDEOCONTROL](propsetid-vidcap-videocontrol.md) | Y |  |  |
| [PROPSETID_VIDCAP_VIDEODECODER](propsetid-vidcap-videodecoder.md) | Y |  |  |
| [PROPSETID_VIDCAP_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md) | Y |  |  |

至少，微型驱动程序必须报告在捕获期间丢弃的帧数，如上表中所述。 所有其他属性集的支持都是可选的，具体取决于设备的功能。 强烈建议仅提供有限的捕获帧速率集的照相机，实现 [PROPSETID \_ VIDCAP \_ VIDEOCONTROL](propsetid-vidcap-videocontrol.md) ，以允许视频会议应用程序充分利用系统带宽。

## <a name="property-set-default-values-and-ranges"></a>属性集默认值和范围

属性可以支持默认值和范围。 用户界面元素（如滑块和滚动条）使用此信息，如下图所示。

![显示用户界面元素（如滑块和滚动条）如何使用默认值和范围的 "属性" 对话框的屏幕截图](images/vcuiprop.gif)

默认值和范围信息在作为属性定义的一部分的 [**KSPROPERTY \_ 值**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_values) 结构中提供。 此结构包括一个指针，该指针指向包含一个或多个 [**KSPROPERTY \_ MEMBERSLIST**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_memberslist) 结构实例的静态表。 在 KSPROPERTY \_ MEMBERSLIST 结构中，微型驱动程序可以指定默认值或一系列值。 可以通过最小值、最大值和步进值指定值的范围。 将[**KSPROPERTY \_ MEMBERSHEADER**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_membersheader)结构的**MEMBERSFLAGS**成员设置为 KSPROPERTY \_ 成员 \_ 范围值，以指示 KSPROPERTY \_ MEMBERSLIST 结构是一个值范围。 KSPROPERTY \_ MEMBERSLIST 结构还用于指定属性的默认值。 这是通过将 KSPROPERTY MEMBERSHEADER 的 **MembersFlags** 成员设置 \_ 为 KSPROPERTY \_ 成员 \_ 值值来完成的。