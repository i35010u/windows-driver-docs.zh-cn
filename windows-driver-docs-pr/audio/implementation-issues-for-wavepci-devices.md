---
title: WavePci 设备的实现问题
description: WavePci 设备的实现问题
ms.assetid: c286d745-6e76-4540-98e6-a46ce1dd0f5d
keywords:
- WDM 音频驱动程序 WDK WavePci
- 音频驱动程序 WDK WavePci
- WavePci 设计指导原则 WDK 音频
- 散播-聚集 DMA WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50f5418f7657e8d178d2cd862723255895971f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333482"
---
# <a name="implementation-issues-for-wavepci-devices"></a>WavePci 设备的实现问题


## <span id="implementation_issues_for_wavepci_devices"></span><span id="IMPLEMENTATION_ISSUES_FOR_WAVEPCI_DEVICES"></span>


本部分提供有关音频硬件供应商可用于提高性能和可靠性的其 WavePci 设备的硬件和软件设计的准则。 所有这些准则适用于音频设备和驱动程序用于处理 Microsoft Windows XP 和更高版本，但许多也适用于早期版本的 Windows 回到 Windows 98 Second Edition。

如中所述[批筛选器](wave-filters.md)，端口类系统驱动程序 Portcls.sys，为批呈现和捕获设备提供两个不同的端口驱动程序：

-   WaveCyclic 要求较低的硬件和软件，但其性能受到的缓冲区之间复制数据的软件系统开销。

-   WavePci WaveCyclic，注重性能的替代方法，但需要更复杂的硬件和驱动程序软件。

尽管从名称 WavePci 音频设备插入到 PCI 总线，事实上，WavePci 设备的主要要求是它包含可以访问任意位置在系统内存中的数据的分散/聚拢 DMA 控制器：

-   典型的 WavePci 设备 does 驻留在 PCI 总线上，但是，从理论上讲，至少，WavePci 微型端口驱动程序无法编写驻留的设备 PCI (例如，AGP) 以外的系统总线上。

-   驻留在 PCI 总线上，但缺少散播-聚集的波形设备由 WaveCyclic 驱动程序，但不能通过 WavePci 驱动程序可以表示 DMA。

从历史上看，某些供应商必须实现完全正常运行 WavePci 设备中的难度。 两个主要问题方面包括：

1.  导致性能下降的硬件设计缺陷。

2.  驱动程序实现错误会影响性能或可靠性。

这种体验的提炼到解决的关键硬件和软件设计问题的 WavePci 设备的以下主题：

[WavePci 设备的硬件要求](hardware-requirements-for-wavepci-devices.md)

[WavePci 微型端口驱动程序的性能问题](performance-issues-for-a-wavepci-miniport-driver.md)

[WavePci 微型端口驱动程序的可靠性问题](reliability-issues-for-a-wavepci-miniport-driver.md)

 

 




