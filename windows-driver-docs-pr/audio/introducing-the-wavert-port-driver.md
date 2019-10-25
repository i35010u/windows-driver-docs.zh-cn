---
title: WaveRT 端口驱动程序简介
description: WaveRT 端口驱动程序简介
ms.assetid: 48b2b59e-385e-4814-ac20-c4b1a08f32dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc75496a8214bf76fb258ddac31b334ccbd46050
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831151"
---
# <a name="introducing-the-wavert-port-driver"></a>WaveRT 端口驱动程序简介


在 Windows Vista 和更高版本的操作系统中，提供对实时（WaveRT）端口驱动程序的支持，以提高性能，但使用简单的循环缓冲区呈现和捕获音频流。

WaveRT 端口驱动程序的性能改进包括以下特性：

-   波形捕获和声波呈现期间的低延迟

-   故障复原音频流

与早期版本的 Microsoft Windows 中的 WaveCyclic 和 WavePci 端口驱动程序类似，WaveRT 端口驱动程序为[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)（KS）筛选器提供通用功能。 WaveRT 端口驱动程序支持音频设备，可以执行以下操作：

-   它们可以连接到系统总线，例如 PCI Express 总线。

-   它们可以播放或录制波形数据（由[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)或[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构描述的音频数据）。

-   他们可以使用 Windows Vista 中提供的改进计划支持来降低音频流的延迟时间。

如果希望音频设备利用 Windows 中提供的音频改进功能，则在流式传输过程中，音频设备必须能够在无需干预的情况下播放或捕获音频数据。 使用 WaveRT 端口驱动程序的设计正确的音频设备需要从音频流进入*运行*状态到从该状态退出之前，几乎或不需要驱动程序软件的帮助。

WaveRT 端口驱动程序的主客户端是在共享模式下运行的音频引擎。 有关 Windows Vista 音频引擎的详细信息，请参阅[探索 Windows Vista 音频引擎](exploring-the-windows-vista-audio-engine.md)主题。

 

 




