---
title: WaveRT 端口驱动程序简介
description: WaveRT 端口驱动程序简介
ms.assetid: 48b2b59e-385e-4814-ac20-c4b1a08f32dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 624a4c0524fde1a19e701bf6ff9c4c54fad1b15f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333420"
---
# <a name="introducing-the-wavert-port-driver"></a>WaveRT 端口驱动程序简介


在 Windows Vista 和更高版本操作系统中，为批实时 (WaveRT) 端口驱动程序，实现了改进了的性能但使用简单的循环缓冲区来呈现图形以及捕获音频流提供支持。

改进了的 WaveRT 端口驱动程序的性能具有以下特征：

-   批捕获过程的低延迟和批呈现

-   故障复原能力的音频流

WaveCyclic 和 WavePci 端口驱动程序的 Microsoft Windows 早期版本中，如 WaveRT 端口驱动程序提供的一般功能[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff560842)(KS) 筛选器。 WaveRT 端口驱动程序提供支持的音频设备可以执行以下操作：

-   它们可以连接到系统总线，例如 PCI Express 总线。

-   他们可以播放或记录批数据 (音频数据描述[ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)或[ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)结构)。

-   他们可以使用可在 Windows Vista 中，若要减少的音频流的延迟的改进计划支持。

如果要确保音频设备才能利用中的改进的音频中提供 Windows，您的音频设备必须能够播放或流式处理期间捕获的驱动程序软件很少或没有干预的音频数据。 正确设计的音频设备，使用 WaveRT 端口驱动程序需要从输入音频流的时间的驱动程序软件的很少或毫无帮助*运行*状态，直到退出该状态。

WaveRT 端口驱动程序的主要的客户端是在共享模式下运行的音频引擎。 有关 Windows Vista 音频引擎的详细信息，请参阅[探究 Windows Vista 音频引擎](exploring-the-windows-vista-audio-engine.md)主题。

 

 




