---
title: 引脚工厂
description: 引脚工厂
ms.assetid: 1399b8e1-bd73-4052-afa5-3e992be8789b
keywords:
- 音频筛选 WDK 音频，固定工厂
- 固定工厂的 WDK 音频
- 固定 WDK 音频、工厂
- 筛选 WDK 音频，固定工厂
- 多个 pin 工厂 WDK 音频
- 数据格式化 WDK 音频，固定工厂
- 格式化 WDK 音频，固定工厂
- 多个 pin 实例 WDK 音频
- 标识 pin 工厂
- KSPIN_DESCRIPTOR 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20feaed3e6607852cb2fcf8ab09fb97c374c13cd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830234"
---
# <a name="pin-factories"></a>引脚工厂


## <span id="pin_factories"></span><span id="PIN_FACTORIES"></span>


音频筛选器的 pin 工厂描述了筛选器可以实例化的所有 pin。 如前文所述，音频微型端口驱动程序将 pin 信息存储在 PCPIN 的数组中[ **\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)结构。 每个结构都指定了一个 pin 工厂，而 pin 工厂由其在数组中的索引标识。 此索引通常称为*PIN ID*。

PCPIN\_描述符结构包含一个自动化表和一个[**KSPIN\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构。

KSPIN\_描述符结构包含有关 pin 工厂中的 pin 的下列信息：

-   筛选器-数据流的相对方向

-   与筛选器相关的通信流方向（在所有当前的 Windows 版本中，KS 筛选器使用 Irp 进行通信）。

-   固定类别

-   友好名称

-   实例功能

-   数据格式功能

结构的**类别**和**名称**成员指定 pin 工厂的 pin 类别和友好名称。 对于筛选器中的每个 pin 工厂，微型端口驱动程序指定共同标识 pin 工厂的**类别**和**名称**guid 的组合。 如果两个或多个 pin 工厂共享同一**类别**值，则每个 pin 工厂都有一个**名称**值，用于将其与其他值区分开来。 如果只有单个 pin 工厂具有特定**类别**值，则该值足以标识 pin 工厂，并且该 pin 工厂的**名称**值可以设置为**NULL**。 有关编码示例，请参阅[公开筛选器拓扑](exposing-filter-topology.md)。 有关 pin 类别的信息，请参阅[固定类别属性](pin-category-property.md)。

Pin 工厂将其支持的数据格式范围指定为扩展[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构的数组：

-   支持其输入或输出流的一系列 wave 或 DirectSound 数据格式的 pin 工厂指定了[**KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)结构的数组。

-   支持其输入或输出流的一系列 MIDI 或 DirectMusic 数据格式的 pin 工厂指定了[**KSDATARANGE\_音乐**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)结构的数组。

KSDATARANGE\_音频和 KSDATARANGE\_音乐是 KSDATARANGE 的扩展版本。 有关这两种类型的数据范围的示例，请参阅[音频数据格式和数据范围](audio-data-formats-and-data-ranges.md)。

在将一个筛选器上的接收器 pin 连接到其他筛选器上的源 pin 之前，图形生成器（例如， [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)）可以在数据区域中搜索兼容的格式。 Graph 生成器通常调用筛选器的[数据交集处理程序，该处理程序](data-intersection-handlers.md)允许筛选器本身选择兼容的格式。

筛选器可以有多个 pin 工厂，并且 pin 工厂可以支持多个 pin 实例。

-   在筛选器上具有多个 pin 工厂对于区分流经筛选器的不同类型的数据，这很有用。 例如，一个 pin 工厂可能支持 PCM 数据流，另一个 pin 工厂可能支持 AC 3 流。

-   单个筛选器可以同时支持呈现和捕获流。 呈现和捕获路径包含不同的筛选器工厂集。

-   接收器-pin 工厂上的多个 pin 实例经常隐含混合，在这种情况下，筛选器包含一个 SUM 节点（[**KSNODETYPE\_sum**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)）。

与筛选器一样，pin 是内核对象，由内核句柄标识。 通过调用[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)创建 pin 实例的句柄。 作为内核对象，可以将 pin 指定为 IRP 的目标。 驱动程序的客户端在向 pin 发送 IOCTL 请求时指定 pin 句柄。

生成[音频筛选器关系图](audio-filter-graphs.md)时，SysAudio 通过连接其 pin 来链接一个筛选器。 一个筛选器中的源 pin 可以连接到其他筛选器的接收器 pin。 源 pin 中的数据和 Irp 通过此连接流入接收器 pin。 若要建立连接，图形生成器（通常为 SysAudio）先通过调用[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)创建源 pin，然后再次调用**KsCreatePin**来创建接收器 pin。 但是，在第二次调用中，客户端指定将新的接收器 pin 连接到在第一次调用中创建的源 pin。

 

 




