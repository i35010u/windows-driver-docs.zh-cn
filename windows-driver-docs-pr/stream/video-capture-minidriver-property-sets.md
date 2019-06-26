---
title: 视频捕获微型驱动程序属性集
description: 视频捕获微型驱动程序属性集
ms.assetid: adbf62c4-1c66-46e9-ae8e-867a88bb107c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f82ee31d07d3d901c8c33dcd0081343212527b8c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385388"
---
# <a name="video-capture-minidriver-property-sets"></a>视频捕获微型驱动程序属性集


## <span id="ddk_video_capture_minidriver_property_sets_ks"></span><span id="DDK_VIDEO_CAPTURE_MINIDRIVER_PROPERTY_SETS_KS"></span>


本部分描述了可用于使用 Microsoft Windows XP、 Windows 2000 和 Windows 98 中的 WDM 内核流式处理服务的视频捕获微型驱动程序的视频捕获特定的属性集 / 我和更高版本的操作系统。

每个属性的参考页包含具有以下列标题的表。


| Get | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

这些标题具有以下含义：

-   **Get**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_属性的 GET 请求？

-   **Set**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_集属性请求？

-   **Target**

    目标是 KS 对象请求发送到哪个属性。 视频捕获属性的目标是筛选器或 pin。 （属性请求指定的目标对象由其内核句柄。）

-   **属性描述符类型**

    属性描述符指定的属性和要在该属性上执行的操作。 描述符始终开头[ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)结构，但某些类型的描述符包含其他信息。 例如， [ **KSNODEPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)结构是开头 KSPROPERTY 结构，但还包括节点标识符的属性描述符。

-   **属性值类型**

    属性的值，而此值的类型取决于属性。 例如，可以是一个只有两种状态-打开或关闭-中的属性通常具有一个 BOOL 值。 可以假定为 0xFFFFFFFF 0x0 从整数值的属性可能具有 ULONG 值。 更复杂的属性可能是数组或结构的值。

属性描述符和更高版本的属性值是实例规范的属性特定于版本和操作数据缓冲[KS 属性、 事件和方法](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)讨论。

属性请求使用下列标志之一来指定要在属性上执行的操作：

-   KSPROPERTY\_类型\_BASICSUPPORT

-   KSPROPERTY\_TYPE\_GET

-   KSPROPERTY\_TYPE\_SET

所有筛选器和 pin 对象支持属性对其的 basic 支持操作。 是否支持*获取*并*设置*操作取决于属性。 该属性表示的筛选器或 pin 对象的固有功能是可能需要仅一个 get 操作。 表示可配置的设置的属性可能只需要*设置*操作，尽管可能适用于读取的当前设置的 get 操作。 有关使用具有视频捕获属性的 get、 集和 basic 支持操作的详细信息，请参阅[KS 属性](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)。

每个属性描述包含一个数据表，说明视频捕获微型驱动程序是否必须支持读取或写入属性。 视频捕获微型驱动程序应返回状态\_不\_要获取或设置为不受微型驱动程序的属性的请求的响应中受支持。

以下列表描述了内核流式处理视频捕获微型驱动程序使用的属性集：

[PROPSETID\_分配器\_控件](propsetid-allocator-control.md)

[PROPSETID\_EXT\_DEVICE](propsetid-ext-device.md)

[PROPSETID\_EXT\_TRANSPORT](propsetid-ext-transport.md)

[PROPSETID\_TIMECODE\_READER](propsetid-timecode-reader.md)

[PROPSETID\_调谐器](propsetid-tuner.md)

[PROPSETID\_VIDCAP\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSPROPERTYSETID\_ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID\_VIDCAP\_CROSSBAR](propsetid-vidcap-crossbar.md)

[PROPSETID\_VIDCAP\_DROPPEDFRAMES](propsetid-vidcap-droppedframes.md)

[PROPSETID\_VIDCAP\_TVAUDIO](propsetid-vidcap-tvaudio.md)

[PROPSETID\_VIDCAP\_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)

[PROPSETID\_VIDCAP\_VIDEOCONTROL](propsetid-vidcap-videocontrol.md)

[PROPSETID\_VIDCAP\_VIDEODECODER](propsetid-vidcap-videodecoder.md)

[PROPSETID\_VIDCAP\_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

下面的属性设置可用于[USB 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver):

[PROPSETID\_VIDCAP\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSPROPERTYSETID\_ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID\_VIDCAP\_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

[PROPSETID\_VIDCAP\_SELECTOR](propsetid-vidcap-selector.md)

 

 





