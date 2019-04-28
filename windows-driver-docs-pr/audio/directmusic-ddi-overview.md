---
title: DirectMusic DDI 概述
description: DirectMusic DDI 概述
ms.assetid: 95870103-197c-4b7c-b6ee-cac176b62dfc
keywords:
- 有关 DirectMusic DDI DirectMusic WDK 音频
- 用户模式下 synths WDK 音频
- 内核模式 synths WDK 音频
- 用户模式接口 WDK 音频
- Dmu 端口驱动程序 WDK 音频
- 内核模式接口 WDK 音频
- 自定义 synths WDK 音频
- Dmu 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a58619bd7d4e2f7789888a519c48241854aa0275
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333792"
---
# <a name="directmusic-ddi-overview"></a>DirectMusic DDI 概述


## <span id="directmusic_ddi_overview"></span><span id="DIRECTMUSIC_DDI_OVERVIEW"></span>


实现用户模式下 synths 通常所需的设计原则适用于内核模式 synths 也。 出于此原因，本指南开头的用户模式下实现和特定的内核模式下的主题进行讨论。

通常情况下，最佳的设计策略是，即先编写软件实现的 DirectMusic*设备驱动程序接口 (DDI)* 在用户模式下运行。 即使最终产品在使用硬件组件的内核模式下实现此方法的优点。 用户模式版本完成后，该软件被可转换为内核模式和硬件，一次一项功能与已建立的连接。 有关详细信息，请参阅[的用户模式下与内核模式](user-mode-versus-kernel-mode.md)。

DirectMusic 使用控件用户模式下合成器的以下用户模式接口，并与内核流式处理驱动程序进行通信：

[IDirectMusicSynth](https://msdn.microsoft.com/library/windows/hardware/ff536519)

这是用户模式接口，用于实现自定义软件 synths。

[IDirectMusicSynthSink](https://msdn.microsoft.com/library/windows/hardware/ff536520)

这是在 Microsoft DirectX 6.1 和 DirectX 7 中实现自定义批接收器的用户模式接口。 DirectX 8 及更高版本，DirectMusic 始终使用其专用批接收器具有用户模式下合成器，并没有公共接口支持为用户模式下批接收器。

[IKsControl](https://msdn.microsoft.com/library/windows/hardware/ff559766)

DirectMusic 使用此接口从 DirectX 6.1 及更高版本的用户模式下访问内核流式处理驱动程序的属性。

内核模式术语由于端口微型端口驱动程序模型从用户模式会稍有不同 (请参阅[端口类简介](introduction-to-port-class.md))，该委托到泛型内核流式处理任务[Dmu 端口驱动程序](dmus-port-driver.md)并将特定于硬件的函数分配给 Dmu 微型端口驱动程序。 端口和微型端口驱动程序共享合成的职责。 内核模式批接收器是驻留在内核中的端口驱动程序的一部分。 与 DirectX 6.1 和 DirectX 7 中的用户模式下批接收器，内核模式批接收器不是可替换的。 大部分生成自定义内核模式驱动程序所需是工作的以书面形式微型端口驱动程序。 在大多数情况下，微型端口驱动程序是硬件的驱动程序编写器需要实现将支持，或为 DirectMusic 实现自定义软件合成器的唯一组件。

自定义 Dmu 微型端口驱动程序使用以下内核模式接口：

[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)

[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)

[ISynthSinkDMus](https://msdn.microsoft.com/library/windows/hardware/ff537011)

[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)

[IMasterClock](https://msdn.microsoft.com/library/windows/hardware/ff536696)

[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)

Dmu 微型端口驱动程序实现**IMiniportDMus**， **ISynthSinkDMus**，并**IMXF**接口。 Dmu 端口驱动程序实现**IAllocatorMXF**， **IMasterClock**，并**IPortDMus**接口并将其公开到微型端口驱动程序。

 

 




