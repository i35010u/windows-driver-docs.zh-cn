---
title: 数据交集
description: 数据交集
ms.assetid: a1588ce0-a091-4bfd-98a9-4d78e2fc847f
keywords:
- 数据交集处理程序 WDK 音频，有关数据交集
- 数据交集 WDK 音频
- 交集 WDK 音频
- 数据范围交集 WDK 音频
- 接收器 pin WDK 音频
- 源 pin WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4857f3cbb07d73ce8764517dd7cb7b961206c510
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359096"
---
# <a name="data-intersection"></a>数据交集


## <span id="data_intersection"></span><span id="DATA_INTERSECTION"></span>


音频筛选器关系图中的音频流可以从流源 pin 的一个筛选器到另一个筛选器的接收器插针只有两个 pin 的流支持一种通用格式。 同样，客户端可以将音频流发送到接收器 pin 对筛选器或音频流接收来自源 pin 对筛选器，仅当客户端和 pin 支持常见的流格式。 音频筛选器使用一种称为数据交集 （的缩写的数据范围交集） 技术来识别常见到两个 pin 或客户端和 pin 码的流格式。

例如，在 Windows Server 2003、 Windows XP、 Windows 2000 和 Windows Me / 98， [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)使用数据交集方法来通过连接筛选器的 pin 对支持的构造音频筛选器关系图兼容的音频数据格式。

一个[pin 工厂](pin-factories.md)指定一组的每个 pin 支持的数据范围，其中每个数据区域是类型的结构数组作为格式[ **KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio). 数据范围指定常规格式的类型，可以是[ **KSDATAFORMAT\_WAVEFORMATEX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)或[ **KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_dsound). 此外，数据范围指定一个范围的值为每个以下参数：

-   每个样本位

-   采样频率

-   通道数

KSDATARANGE\_音频结构指定位每个示例和示例频率范围中的最小值和最大值，但仅的最大通道数范围。 通道的最小数目是隐式之一。

查找两个数据区域-从每个 pin-相互交叉的包含协商两个 pin 的常用数据格式的作业。 对数据范围相交如果：

-   它们支持相同的常规波形格式 (KSDATAFORMAT\_WAVEFORMATEX 或 KSDATAFORMAT\_DSOUND)。

-   其位每个样本范围重叠。

-   及其采样频率范围重叠。

如前文所述，KSDATAFORMAT\_音频结构意味着在该通道受 pin 的最小数目始终是一个硬件型号。 根据此模型中，任何两个 pin 的通道数范围应始终重叠，因为这两个 pin 支持至少一个通道。 很明显，具有多个通道的最少的硬件适配器不符合此模型中，但适配器驱动程序可以包括一个专有数据交集处理程序来处理此类型的问题 (请参阅中的示例[专有Data-Intersection 处理程序](proprietary-data-intersection-handlers.md))。

在查找一对重叠的数据区域的两个 pin，处理程序的常用数据格式从选择的交集的区域，如下所示：

-   从在其中的两位每个样本范围重叠的区域选择的每个样本位数。

-   在这两个示例频率范围重叠的区域中选择采样频率。

-   在这两个频道号范围重叠的区域中选择的通道数。

例如，协商音频端口驱动程序的接收器 pin 和另一个筛选器的源插针的通用格式时 (通常情况下， [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver))，SysAudio 首先获取源插针的数据范围数组。 然后将发送 SysAudio [ **KSPROPERTY\_PIN\_DATAINTERSECTION** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)对接收器 pin 的请求，并包含与此请求的源插针的数据范围数组。 内核流式处理层截获的请求，并以迭代方式为在源插针的数据范围数组中，直到该处理程序中查找成功开头的第一个元素，每个连续元素一次地调用端口驱动程序的数据交叉处理程序数据交集。

SysAudio 对端口驱动程序的数据交叉处理程序每次调用，该处理程序首先从微型端口驱动程序获取接收器插针的数据范围数组。 它然后循环访问数组，从第一个元素，直到它成功地找到接收器 pin 数据范围和当前的源 pin 数据区域之间的交集。 该处理程序将选择位于交集，并输出到调用方此格式的通用格式。

在迭代中每个步骤，端口驱动程序调用微型端口驱动程序的专有数据交集处理程序包含两个数据区域-一个用于每个两个 pin。 如果在执行任一步骤专有的处理程序拒绝处理两个数据区域之间的交集数据检查，端口驱动程序的数据交叉处理程序执行检查。

总而言之，搜索源 pin 数据范围和接收器 pin 数据范围之间的交集是一个迭代过程：

-   在外部循环中，内核流式处理层循环访问源插针的数据范围数组，从第一个数组元素中的连续元素。

-   在内部循环中，端口驱动程序循环访问接收器插针的数据范围数组，从第一个数组元素中的连续元素。

查找第一个数据交集后停止搜索。 此过程往往比较适合每个插针的数据范围数组的开头的元素。 在指定的 pin 的数据范围数组时，适配器驱动程序应订购数组元素上来将该数组的开头的首选格式的数据范围。

 

 




