---
title: 视频捕获微型驱动程序属性集
description: 视频捕获微型驱动程序属性集
ms.assetid: adbf62c4-1c66-46e9-ae8e-867a88bb107c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a4ec95337d16e765de3a21982fc59b33cec735b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844971"
---
# <a name="video-capture-minidriver-property-sets"></a>视频捕获微型驱动程序属性集


## <span id="ddk_video_capture_minidriver_property_sets_ks"></span><span id="DDK_VIDEO_CAPTURE_MINIDRIVER_PROPERTY_SETS_KS"></span>


本部分介绍视频捕获特定的属性集，这些属性集可用于在 Microsoft Windows XP、Windows 2000 和 Windows 98/Me 及更高版本的操作系统中使用 WDM 内核流式处理服务的视频捕获微型驱动程序。

每个属性的引用页面都包含一个具有以下列标题的表。


| “获取” | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

这些标题具有以下含义：

-   **获取**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_获取属性请求？

-   **字符集**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_设置属性请求？

-   **靶**

    目标是向其发送属性请求的 KS 对象。 视频捕获属性的目标是筛选器或 pin。 （属性请求按其内核句柄指定目标对象。）

-   **属性描述符类型**

    属性说明符指定属性和要对该属性执行的操作。 描述符始终以[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)结构开始，但某些类型的描述符包含附加信息。 例如， [**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)结构是以 KSPROPERTY 结构开头但还包含节点标识符的属性描述符。

-   **属性值类型**

    属性具有值，并且此值的类型取决于属性。 例如，一个只能处于两种状态的属性（打开或关闭）通常具有 BOOL 值。 可以假设从0x0 到0xFFFFFFFF 的整数值的属性可能具有 ULONG 值。 更复杂的属性可能具有作为数组或结构的值。

以上属性说明符和属性值是[KS 属性、事件和方法](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)讨论的实例规范和操作数据缓冲区的属性特定版本。

属性请求使用下列标志之一来指定要对属性执行的操作：

-   KSPROPERTY\_类型\_BASICSUPPORT

-   KSPROPERTY\_类型\_GET

-   KSPROPERTY\_类型\_集

所有筛选器和 pin 对象均支持对其属性的基本支持操作。 它们是否支持*get*和*Set*操作取决于属性。 表示筛选器或固定对象的固有功能的属性可能只需要 get 操作。 尽管获取操作也可能对读取当前设置很有用，但表示可配置的设置的属性可能只需要*设置*操作。 若要详细了解如何使用视频捕获属性的 get、set 和 basic 支持操作，请参阅[KS properties](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)。

每个属性说明都包含一个表，用于指示视频捕获微型驱动程序是否必须支持读取或写入属性。 视频捕获微型驱动程序应返回\_不\_支持的状态，以响应对微型驱动程序不支持的属性的 get 或 set 请求。

以下列表描述了视频捕获微型驱动程序使用的内核流式处理属性集：

[PROPSETID\_分配器\_控制](propsetid-allocator-control.md)

[PROPSETID\_EXT\_设备](propsetid-ext-device.md)

[PROPSETID\_EXT\_传输](propsetid-ext-transport.md)

[PROPSETID\_时间码\_读者](propsetid-timecode-reader.md)

[PROPSETID\_调谐器](propsetid-tuner.md)

[PROPSETID\_VIDCAP\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSPROPERTYSETID\_ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID\_VIDCAP\_横线](propsetid-vidcap-crossbar.md)

[PROPSETID\_VIDCAP\_DROPPEDFRAMES](propsetid-vidcap-droppedframes.md)

[PROPSETID\_VIDCAP\_TVAUDIO](propsetid-vidcap-tvaudio.md)

[PROPSETID\_VIDCAP\_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)

[PROPSETID\_VIDCAP\_VIDEOCONTROL](propsetid-vidcap-videocontrol.md)

[PROPSETID\_VIDCAP\_VIDEODECODER](propsetid-vidcap-videodecoder.md)

[PROPSETID\_VIDCAP\_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

以下属性集可与[USB 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)一起使用：

[PROPSETID\_VIDCAP\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSPROPERTYSETID\_ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID\_VIDCAP\_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

[PROPSETID\_VIDCAP\_选择器](propsetid-vidcap-selector.md)

 

 





