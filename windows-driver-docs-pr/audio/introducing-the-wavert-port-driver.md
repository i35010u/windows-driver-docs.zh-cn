---
title: WaveRT 端口驱动程序简介
description: WaveRT 端口驱动程序简介
ms.assetid: 48b2b59e-385e-4814-ac20-c4b1a08f32dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe865d6635e690ce4bb348e5d9fe36b09ea7a388
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359866"
---
# <a name="introducing-the-wavert-port-driver"></a>WaveRT 端口驱动程序简介


在 Windows Vista 和更高版本操作系统中，为批实时 (WaveRT) 端口驱动程序，实现了改进了的性能但使用简单的循环缓冲区来呈现图形以及捕获音频流提供支持。

改进了的 WaveRT 端口驱动程序的性能具有以下特征：

-   批捕获过程的低延迟和批呈现

-   故障复原能力的音频流

WaveCyclic 和 WavePci 端口驱动程序的 Microsoft Windows 早期版本中，如 WaveRT 端口驱动程序提供的一般功能[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)(KS) 筛选器。 WaveRT 端口驱动程序提供支持的音频设备可以执行以下操作：

-   它们可以连接到系统总线，例如 PCI Express 总线。

-   他们可以播放或记录批数据 (音频数据描述[ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)或[ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)结构)。

-   他们可以使用可在 Windows Vista 中，若要减少的音频流的延迟的改进计划支持。

如果要确保音频设备才能利用中的改进的音频中提供 Windows，您的音频设备必须能够播放或流式处理期间捕获的驱动程序软件很少或没有干预的音频数据。 正确设计的音频设备，使用 WaveRT 端口驱动程序需要从输入音频流的时间的驱动程序软件的很少或毫无帮助*运行*状态，直到退出该状态。

WaveRT 端口驱动程序的主要的客户端是在共享模式下运行的音频引擎。 有关 Windows Vista 音频引擎的详细信息，请参阅[探究 Windows Vista 音频引擎](exploring-the-windows-vista-audio-engine.md)主题。

 

 




