---
title: WaveRT 端口驱动程序简介
description: WaveRT 端口驱动程序简介
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66626a10c04f28201e6192d79daeaf1c81927a44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784711"
---
# <a name="introducing-the-wavert-port-driver"></a>WaveRT 端口驱动程序简介


在 Windows Vista 和更高版本的操作系统中，提供对实时 (WaveRT) 端口驱动程序的支持，以提高性能，但使用简单的循环缓冲区呈现和捕获音频流。

WaveRT 端口驱动程序的性能改进包括以下特性：

-   波形捕获和声波呈现期间的低延迟

-   故障复原音频流

与早期版本的 Microsoft Windows 中的 WaveCyclic 和 WavePci 端口驱动程序类似，WaveRT 端口驱动程序为 [内核流式处理](../stream/kernel-streaming.md) (KS) 筛选器提供通用功能。 WaveRT 端口驱动程序支持音频设备，可以执行以下操作：

-   它们可以连接到系统总线，例如 PCI Express 总线。

-   它们可以通过 [**WAVEFORMATEX**](/windows/win32/api/mmreg/ns-mmreg-waveformatex) 或 [**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible) 结构) 描述的音频数据来播放或录制波形数据 (。

-   他们可以使用 Windows Vista 中提供的改进计划支持来降低音频流的延迟时间。

如果希望音频设备利用 Windows 中提供的音频改进功能，则在流式传输过程中，音频设备必须能够在无需干预的情况下播放或捕获音频数据。 使用 WaveRT 端口驱动程序的设计正确的音频设备需要从音频流进入 *运行* 状态到从该状态退出之前，几乎或不需要驱动程序软件的帮助。

WaveRT 端口驱动程序的主客户端是在共享模式下运行的音频引擎。 有关 Windows Vista 音频引擎的详细信息，请参阅 [探索 Windows Vista 音频引擎](exploring-the-windows-vista-audio-engine.md) 主题。

 

