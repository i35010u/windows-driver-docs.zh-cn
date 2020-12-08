---
title: WavePci 设备的实现问题
description: WavePci 设备的实现问题
keywords:
- WDM 音频驱动程序 WDK，WavePci
- 音频驱动程序 WDK，WavePci
- WavePci 设计指南 WDK 音频
- 分散/收集 DMA WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f579ede788ba70f903f6edab81b0779e86a53b58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784765"
---
# <a name="implementation-issues-for-wavepci-devices"></a>WavePci 设备的实现问题


## <span id="implementation_issues_for_wavepci_devices"></span><span id="IMPLEMENTATION_ISSUES_FOR_WAVEPCI_DEVICES"></span>


本部分介绍了音频硬件供应商可用于提高其 WavePci 设备的性能和可靠性的硬件和软件设计准则。 所有这些指导原则适用于与 Microsoft Windows XP 和更高版本结合使用的音频设备和驱动程序，但许多应用程序还适用于 windows 98 第二版。

如 [波形过滤器](wave-filters.md)中所述，端口类系统驱动程序 Portcls.sys 为波形渲染和捕获设备提供了两个不同的端口驱动程序：

-   WaveCyclic 的硬件和软件要求较低，但其性能受在缓冲区之间复制数据的软件开销限制。

-   WavePci 是 WaveCyclic 的面向性能的替代方案，但需要更复杂的硬件和驱动程序软件。

尽管名称 WavePci 表示插入 PCI 总线的音频设备，但实际上，WavePci 设备的主要要求是它包含一个能够访问系统内存中任何位置的数据的散播/聚集 DMA 控制器：

-   典型的 WavePci 设备驻留在 PCI 总线上，但理论上至少可以为驻留在 PCI (以外的系统总线上的设备编写 WavePci 微型端口，例如 AGP) 。

-   驻留在 PCI 总线上但缺少散播/聚集 DMA 的波形设备可由 WaveCyclic 驱动程序表示，而不能由 WavePci 驱动程序表示。

从历史上看，一些供应商在实现功能齐全的 WavePci 设备方面存在困难。 主要有两个问题领域：

1.  降低性能的硬件设计缺陷。

2.  驱动程序实现错误会影响性能或可靠性。

此体验已细分为以下主题，这些主题解决了 WavePci 设备的关键硬件和软件设计问题：

[WavePci 设备的硬件要求](hardware-requirements-for-wavepci-devices.md)

[WavePci 微型端口驱动程序的性能问题](performance-issues-for-a-wavepci-miniport-driver.md)

[WavePci 微型端口驱动程序的可靠性问题](reliability-issues-for-a-wavepci-miniport-driver.md)

 

 




