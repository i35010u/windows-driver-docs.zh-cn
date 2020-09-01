---
title: 数据交集
description: 数据交集
ms.assetid: a1588ce0-a091-4bfd-98a9-4d78e2fc847f
keywords:
- 数据交集处理程序 WDK 音频，关于数据交集
- 数据交集 WDK 音频
- 与 WDK 音频交叉
- 数据范围交集 WDK 音频
- 接收器引脚 WDK 音频
- 源引脚 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0978a318336443a1f79ba4579e2cbbc3d3df8fd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208169"
---
# <a name="data-intersection"></a>数据交集


## <span id="data_intersection"></span><span id="DATA_INTERSECTION"></span>


在音频筛选器图中，只有当两个 pin 支持公共格式的流时，音频流才能从一个筛选器的源插针流向另一个筛选器的接收器 pin。 同样，客户端可以将音频流发送到筛选器上的接收器插针，或仅当客户端和 pin 支持公共流格式时才从筛选器的源插针接收音频流。 音频筛选器使用一种称为数据交集的技术 (短于数据范围交集) 来识别两个插针或客户端和 pin 共用的流格式。

例如，在 Windows Server 2003、Windows XP、Windows 2000 和 Windows Me/98 中， [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver) 通过连接支持兼容音频数据格式的一对筛选器 pin 来使用数据交叉技术来构造音频筛选器关系图。

[Pin 工厂](pin-factories.md)将每个 pin 支持的一组格式指定为数据范围的数组，其中每个数据区域都是[**KSDATARANGE \_ AUDIO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)类型的结构。 数据范围指定常规格式类型，可为 [**KSDATAFORMAT \_ WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex) 或 [**KSDATAFORMAT \_ DSOUND**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)。 此外，数据范围还为以下每个参数指定了一系列值：

-   每个样本的位数

-   采样频率

-   通道数量

KSDATARANGE \_ 音频结构同时为每样本位和采样频率范围指定最小值和最大值，但最大值为通道数范围。 最小通道数是隐式的。

为两个插针协商通用数据格式的工作包括查找两个数据范围-一个来自每个 pin--彼此相交。 如果是以下情况，则一对数据范围会交集：

-   它们支持相同的常规波形格式 (KSDATAFORMAT \_ WAVEFORMATEX 或 KSDATAFORMAT \_ DSOUND) 。

-   它们每个样本的位数重叠。

-   它们的采样频率范围重叠。

如前所述，KSDATAFORMAT \_ 音频结构表示一个硬件型号，其中 pin 支持的最小通道数始终为1。 根据此模型，任意两个 pin 的通道数范围应始终重叠，因为这两个 pin 至少支持一个通道。 显然，最小数量为1个通道的硬件适配器不符合此模型，但适配器驱动程序可以包含专用的数据交集处理程序来处理此类问题 (参阅 [专用数据交集处理程序](proprietary-data-intersection-handlers.md)) 中的示例。

为两个插针查找一对相交的数据范围时，处理程序将从交集区域中选择一个通用数据格式，如下所示：

-   每个样本的位数是从两个每个样本单元重叠的区域中选择的。

-   从两个采样频率范围重叠的区域中选择了采样频率。

-   从两个通道范围重叠的区域中选择通道数。

例如，在为音频端口驱动程序的接收器 pin 和其他筛选器的源 pin 协商通用格式时 (通常情况下， [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)) 首先获取源 pin 的数据范围数组。 然后，SysAudio 将 [**KSPROPERTY \_ pin \_ DATAINTERSECTION**](../stream/ksproperty-pin-dataintersection.md) 请求发送到接收器 pin，并在此请求中包含源 PIN 的数据范围数组。 内核流式处理层会截获请求，并以迭代方式为源插针的数据范围数组中的每个连续元素（从第一个元素开始）调用端口驱动程序的数据交集处理程序，直到处理程序成功查找数据交集。

对于 SysAudio 为端口驱动程序的数据交集处理程序发出的每个调用，处理程序首先从微型端口驱动程序获取接收器 pin 的数据范围数组。 然后，它将从第一个元素开始循环访问数组，直到它成功找到接收器数据范围和当前源-pin 数据范围之间的交集。 处理程序选择位于交集内的通用格式，并将此格式输出到调用方。

在迭代的每个步骤中，端口驱动程序都调用微型端口驱动程序的专用数据交集处理程序和两个数据范围-每个数据区域对应两个数据区域。 如果在任何步骤中，专用处理程序拒绝处理两个数据区域之间的数据交集检查，则端口驱动程序的数据交集处理程序将改为执行检查。

总而言之，搜索源 pin 数据范围和接收器 pin 数据范围之间的交集是一个迭代过程：

-   在外部循环中，内核流式处理层从第一个数组元素开始，遍历源插针的数据范围数组中的连续元素。

-   在内部循环中，端口驱动程序从第一个数组元素开始，遍历接收器插针的数据范围数组中的后续元素。

查找第一个数据交集时停止搜索。 此过程倾向于使元素接近于每个插针的数据范围数组的开头。 当指定 pin 的数据范围数组时，适配器驱动程序应通过将首选格式的数据范围置于数组的开头来对数组元素进行排序。

 

