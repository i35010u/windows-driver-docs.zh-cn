---
title: DirectMusic DDI 概述
description: DirectMusic DDI 概述
ms.assetid: 95870103-197c-4b7c-b6ee-cac176b62dfc
keywords:
- DirectMusic WDK 音频，关于 DirectMusic DDI
- 用户模式 synths WDK 音频
- 内核模式 synths WDK 音频
- 用户模式接口 WDK 音频
- Dmu 端口驱动程序 WDK 音频
- 内核模式接口 WDK 音频
- 自定义 synths WDK 音频
- Dmu 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f0e69c0db64e1281c607992de9464eec1808ab3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833546"
---
# <a name="directmusic-ddi-overview"></a>DirectMusic DDI 概述


## <span id="directmusic_ddi_overview"></span><span id="DIRECTMUSIC_DDI_OVERVIEW"></span>


实现用户模式 synths 所需的设计原则也适用于内核模式 synths。 出于此原因，本指南首先介绍用户模式实现，并逐步介绍特定的内核模式主题。

通常，最佳设计策略是首先编写在用户模式下运行的 DirectMusic*设备驱动程序接口（DDI）* 的软件实现。 即使最终产品是使用硬件组件的内核模式实现，此方法也非常有用。 在用户模式版本完成后，可以将软件转换为内核模式，以及与硬件建立的连接，一次一项功能。 有关详细信息，请参阅[用户模式与内核模式](user-mode-versus-kernel-mode.md)。

DirectMusic 使用以下用户模式接口控制用户模式合成程序，并与内核流式处理驱动程序通信：

[IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)

这是用于实现自定义软件 synths 的用户模式接口。

[IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)

这是在 Microsoft DirectX 6.1 和 DirectX 7 中实现自定义波形接收器的用户模式接口。 在 DirectX 8 及更高版本中，DirectMusic 始终将其专用波形接收器与用户模式合成一起使用，并且用户模式波形接收器不支持公共接口。

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)

DirectMusic 使用此接口从 DirectX 6.1 和更高版本中的用户模式访问内核流式处理驱动程序的属性。

内核模式术语与用户模式略有不同，因为端口-微型驱动程序模型（请参阅[端口类简介](introduction-to-port-class.md)），该模型将一般内核流式处理任务委托给[dmu 端口驱动程序](dmus-port-driver.md)并分配特定于硬件的用于 Dmu 微型端口驱动程序的函数。 端口和微型端口驱动程序分担合成的责任。 内核模式波形接收器是内核驻留端口驱动程序的一部分。 不同于 DirectX 6.1 和 DirectX 7 中的用户模式波形接收器，无法更换内核模式波形接收器。 构建自定义内核模式驱动程序所需的大部分工作都是写入微型端口驱动程序。 在大多数情况下，微型端口驱动程序是驱动程序编写器唯一需要实现以支持一段硬件或实现 DirectMusic 的自定义软件合成的唯一组件。

自定义 Dmu 微型端口驱动程序使用以下内核模式接口：

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

Dmu 微型端口驱动程序实现**IMiniportDMus**、 **ISynthSinkDMus**和**IMXF**接口。 Dmu 端口驱动程序实现了**IAllocatorMXF**、 **IMasterClock**和**IPortDMus**接口，并将它们公开给微型端口驱动程序。

 

 




