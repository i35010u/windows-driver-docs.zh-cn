---
title: 视频捕获微型驱动程序属性集
description: 视频捕获微型驱动程序属性集
ms.assetid: adbf62c4-1c66-46e9-ae8e-867a88bb107c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c18f715de86868aed3a84e6592103b8c4e6e75d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184365"
---
# <a name="video-capture-minidriver-property-sets"></a>视频捕获微型驱动程序属性集


## <span id="ddk_video_capture_minidriver_property_sets_ks"></span><span id="DDK_VIDEO_CAPTURE_MINIDRIVER_PROPERTY_SETS_KS"></span>


本部分介绍视频捕获特定的属性集，这些属性集可用于在 Microsoft Windows XP、Windows 2000 和 Windows 98/Me 及更高版本的操作系统中使用 WDM 内核流式处理服务的视频捕获微型驱动程序。

每个属性的引用页面都包含一个具有以下列标题的表。


| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

这些标题具有以下含义：

-   **Get**

    目标 KS 对象是否支持 KSPROPERTY \_ 类型 \_ GET 属性请求？

-   **设置**

    目标 KS 对象是否支持 KSPROPERTY \_ 类型 \_ 集属性请求？

-   **Target**

    目标是向其发送属性请求的 KS 对象。 视频捕获属性的目标是筛选器或 pin。  (属性请求按其内核句柄指定目标对象。 ) 

-   **属性描述符类型**

    属性说明符指定属性和要对该属性执行的操作。 描述符始终以 [**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) 结构开始，但某些类型的描述符包含附加信息。 例如， [**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty) 结构是以 KSPROPERTY 结构开头但还包含节点标识符的属性描述符。

-   **属性值类型**

    属性具有值，并且此值的类型取决于属性。 例如，一个只能处于两种状态的属性（打开或关闭）通常具有 BOOL 值。 可以假设从0x0 到0xFFFFFFFF 的整数值的属性可能具有 ULONG 值。 更复杂的属性可能具有作为数组或结构的值。

以上属性说明符和属性值是 [KS 属性、事件和方法](./ks-properties--events--and-methods.md) 讨论的实例规范和操作数据缓冲区的属性特定版本。

属性请求使用下列标志之一来指定要对属性执行的操作：

-   KSPROPERTY \_ 类型 \_ BASICSUPPORT

-   KSPROPERTY \_ 类型 \_ GET

-   KSPROPERTY \_ 类型 \_ 集

所有筛选器和 pin 对象均支持对其属性的基本支持操作。 它们是否支持 *get* 和 *Set* 操作取决于属性。 表示筛选器或固定对象的固有功能的属性可能只需要 get 操作。 尽管获取操作也可能对读取当前设置很有用，但表示可配置的设置的属性可能只需要 *设置* 操作。 若要详细了解如何使用视频捕获属性的 get、set 和 basic 支持操作，请参阅 [KS properties](./ks-properties.md)。

每个属性说明都包含一个表，用于指示视频捕获微型驱动程序是否必须支持读取或写入属性。 视频捕获微型驱动程序应返回对 \_ \_ 微型驱动程序不支持的属性的 get 或 set 请求所需的状态。

以下列表描述了视频捕获微型驱动程序使用的内核流式处理属性集：

[PROPSETID \_ 分配器 \_ 控件](propsetid-allocator-control.md)

[PROPSETID \_ EXT \_ 设备](propsetid-ext-device.md)

[PROPSETID \_ 扩展 \_ 传输](propsetid-ext-transport.md)

[PROPSETID 时间 \_ 码 \_ 读取器](propsetid-timecode-reader.md)

[PROPSETID \_ 调谐器](propsetid-tuner.md)

[PROPSETID \_ VIDCAP \_ CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSPROPERTYSETID \_ ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID \_ VIDCAP \_ 横线](propsetid-vidcap-crossbar.md)

[PROPSETID \_ VIDCAP \_ DROPPEDFRAMES](propsetid-vidcap-droppedframes.md)

[PROPSETID \_ VIDCAP \_ TVAUDIO](propsetid-vidcap-tvaudio.md)

[PROPSETID \_ VIDCAP \_ VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)

[PROPSETID \_ VIDCAP \_ VIDEOCONTROL](propsetid-vidcap-videocontrol.md)

[PROPSETID \_ VIDCAP \_ VIDEODECODER](propsetid-vidcap-videodecoder.md)

[PROPSETID \_ VIDCAP \_ VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

以下属性集可与 [USB 视频类驱动程序](./usb-video-class-driver.md)一起使用：

[PROPSETID \_ VIDCAP \_ CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSPROPERTYSETID \_ ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID \_ VIDCAP \_ VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

[PROPSETID \_ VIDCAP \_ 选择器](propsetid-vidcap-selector.md)

 

