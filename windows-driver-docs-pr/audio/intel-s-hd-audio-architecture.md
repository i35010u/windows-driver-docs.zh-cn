---
title: Intel 的 HD 音频体系结构
description: Intel 的 HD 音频体系结构
ms.assetid: 86cba795-847c-4f54-93f8-e34ae73dc708
keywords:
- HD Audio，体系结构
- 高清晰度音频 (HD Audio) 体系结构
- 体系结构 WDK 音频
- Intel 高清晰度音频规范
- UAA WDK
- 通用音频体系结构 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 226cc5b72c3a348aa1d8c3f422e920a0737abbbc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333427"
---
# <a name="intels-hd-audio-architecture"></a>Intel 的 HD 音频体系结构


Intel 高定义音频规范 (请参阅[Intel HD 音频](https://go.microsoft.com/fwlink/p/?linkid=42508)网站) 描述的后继 Intel AC'97 编解码器和控制器规范作为开发的音频硬件体系结构。 操作系统的 UAA 驱动程序组件可以提供服务的音频解决方案，用于公开的 HD Audio 寄存器集并连接到系统的内部总线，而无需从硬件供应商的特定于解决方案的驱动程序。

HD Audio 体系结构为数字音频控制器提供一个统一的编程接口。 通常情况下，今天的音频编解码器符合 AC'97 行业标准，并且数字控制器连接到一个或多个 AC'97 编解码器通过另一种行业标准，AC 链接。 尽管这些标准有助于确保该编解码器以及一致地实现链接，但没有标准目前存在的数字音频控制器中定义的接口。 供应商往往具有非常类似的解决方案，其系统集成 AC'97 数字音频控制器，但每个 AC'97 解决方案很可能是足够的差异需要单独的驱动程序。 HD Audio 体系结构旨在通过指定在所有的实现是统一的基寄存器集消除特定于解决方案的驱动程序的要求。

HD Audio 体系结构符合总线控制器：

-   提供控制器硬件版本信息。

-   提供了硬件配置信息，包括串行数据扩展 (SDO) 行和 DMA 引擎数。

-   管理 HD 音频链接上的可用总线带宽量。

-   接受未经请求的响应和来自编解码器的唤醒事件。

-   队列编解码器命令和在单独的环形缓冲区中的编解码器响应。

-   提供了一系列输入、 输出和双向 DMA 引擎执行散播-聚集传输并通过主机处理器可以流媒体编解码器和而无需干预的内存中的循环缓冲区之间的数据。

下图显示了 UAA 驱动程序体系结构的关系图的高清晰度音频设备在 Windows Vista 中。 在图中，Microsoft 提供了标记 UAA HD 音频类驱动程序和高清晰度音频总线驱动程序软件组件。 标记为调制解调器驱动程序的组件提供的独立硬件供应商。

![对 intel 说明 uaa 驱动程序体系结构的关系图 hd 音频设备](images/hdaudio.png)

UAA HD 音频类驱动程序提供了驱动程序 （在上图中未显示） 上的操作系统音频堆栈的流式处理接口。

HD Audio 总线驱动程序直接访问硬件寄存器 HD Audio 控制器中的，并提供 DDI 的 UAA HD Audio 类驱动程序或调制解调器驱动程序使用来管理的 DMA 引擎，并将命令发送到编解码器。 HD Audio 总线驱动程序代表 HD 音频链接上的音频设备处理所有中断、 插通知和电源管理事件。

HD Audio 控制器提供的 DMA 引擎和用于命令和传输数据到编解码器 HD 音频链接上的命令缓冲区。 在上图中标记为编解码器的框可以编解码器的音频或调制解调器，并且它们可以连接到外围通过外部插孔的可移动设备或固定的内部外围设备，如移动 PC 扬声器。

 

 




