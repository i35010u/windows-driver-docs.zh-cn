---
title: 引脚工厂
description: 引脚工厂
ms.assetid: 1399b8e1-bd73-4052-afa5-3e992be8789b
keywords:
- 音频筛选器 WDK 音频、 固定工厂
- pin 工厂 WDK 音频
- pin WDK 音频，工厂
- 筛选 WDK 音频、 固定工厂
- 多个 pin 工厂 WDK 音频
- 数据格式以 WDK 音频、 固定工厂
- 格式 WDK 音频、 固定工厂
- 多个 pin 实例 WDK 音频
- 标识 pin 工厂
- KSPIN_DESCRIPTOR 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67b533a94616091cce8abf4bddf390125e21099b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355304"
---
# <a name="pin-factories"></a>引脚工厂


## <span id="pin_factories"></span><span id="PIN_FACTORIES"></span>


音频筛选器的 pin 工厂描述所有筛选器可以实例化球瓶。 正如前面提到，音频微型端口驱动程序将 pin 信息存储在数组[ **PCPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcpin_descriptor)结构。 每个结构指定 pin 工厂中，并由其数组中的索引标识的 pin 工厂。 此索引通常称为*固定 ID*。

PCPIN\_描述符结构包含自动化表和一个[ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)结构。

KSPIN\_描述符结构包含有关球瓶 pin 工厂中的以下信息：

-   相对于筛选器的数据流方向

-   通信流的筛选器的相对方向 （在所有当前的 Windows 版本中，KS 筛选器使用 Irp 进行通信。）

-   Pin 类别

-   友好名称

-   实例功能

-   数据格式的功能

该结构的**类别**并**名称**成员指定 pin 工厂的 pin 类别和友好名称。 对于每个筛选器中的 pin 工厂，微型端口驱动程序指定的组合**类别**并**名称**，它们结合起来的 Guid 唯一地标识 pin 工厂。 如果两个或多个 pin 工厂共用同一个**类别**的值，每个 pin 工厂具有**名称**使它有别于其他值。 如果只有单个插针工厂具有特定**类别**值，值已足以确定 pin 工厂，并**名称**值可以设置该 pin 工厂为**NULL**. 有关编码的示例，请参阅[公开筛选器拓扑](exposing-filter-topology.md)。 有关 pin 类别的信息，请参阅[Pin Category 属性](pin-category-property.md)。

Pin 工厂数组的形式指定它支持的数据格式的范围扩展[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构：

-   支持一定范围的批或 DirectSound 数据的 pin 工厂格式为它的输入或输出流指定的数组[ **KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)结构。

-   Pin 工厂支持的范围的 MIDI 或 DirectMusic 数据的格式为它的输入或输出流指定的数组[ **KSDATARANGE\_音乐**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_music)结构。

KSDATARANGE\_音频和 KSDATARANGE\_音乐进行了扩展的 KSDATARANGE 版本。 有关这两种类型的数据范围的示例，请参阅[音频数据格式和数据范围](audio-data-formats-and-data-ranges.md)。

连接到另一个筛选器，图形生成器源 pin 的上一个筛选器的接收器 pin 之前 (例如， [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)) 可以搜索兼容格式的数据范围。 图生成器通常会调用筛选器的[交集数据处理程序](data-intersection-handlers.md)，它允许在筛选器可以选择兼容的格式。

筛选器可以有多个 pin 工厂，而 pin 工厂可以支持多个 pin 实例。

-   无筛选器上的多个 pin 工厂可用于区分不同类型的流经筛选器的数据的单独的数据路径。 例如，一个 pin 工厂可能支持 PCM 数据流量，另一个 pin 工厂可能支持 ac-3 流。

-   有单个筛选器可支持呈现，同时捕获流。 呈现和捕获路径有单独的筛选器工厂。

-   经常接收器 pin 工厂上有多个 pin 实例意味着混合，在这种情况下的筛选器包含 SUM 节点 ([**KSNODETYPE\_SUM**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum))。

类似于筛选器，插针是内核对象，由内核句柄。 通过调用创建 pin 实例的句柄[ **KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatepin)。 为内核对象，可以为目标的 IRP 指定 pin。 IOCTL 请求发送到 pin 时，该驱动程序的客户端指定 pin 句柄。

在生成时[音频筛选器图形](audio-filter-graphs.md)，SysAudio 链接一个筛选器到另一个连接他们的 pin。 从一个筛选器的源 pin 可以连接到另一个筛选器的接收器插针。 数据和来自源的 Irp 将固定到通过此连接的接收器 pin 的流。 若要使该连接，图形生成器 (通常 SysAudio) 创建源 pin 首先通过调用[ **KsCreatePin** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatepin) ，然后通过调用创建接收器 pin **KsCreatePin**再次。 在第二个调用中，但是，客户端指定新的接收器 pin 所要连接到已在第一次调用中创建的源插针。

 

 




