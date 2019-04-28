---
title: UAA 类驱动程序
description: UAA 类驱动程序
ms.assetid: 57f8f6fe-53a9-4ef1-b4f6-715232e88fdf
keywords:
- 高清晰度音频，通用音频体系结构
- 高清晰度音频 （HD 音频） 通用音频体系结构
- UAA WDK
- 通用音频体系结构 WDK
- 类驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8adc304c411a93685685dcb2740a3d411b696017
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335434"
---
# <a name="uaa-class-drivers"></a>UAA 类驱动程序


在 Windows Vista 中，Microsoft 提供的音频设备的连接到的内部总线 (PCI) 或 （IEEE 1394 或 USB） 的外部总线 UAA 类驱动程序。 若要获得特定的总线的 UAA 类驱动程序的支持，设备必须符合该总线的 UAA 硬件规格。 对于内部总线上设备，请指定以下 UAA 硬件要求文档：

-   HD Audio 控制器的次要更改中所述使用注册组[HD 音频体系结构的 UAA 扩展](uaa-extensions-to-the-hd-audio-architecture.md)。

-   （要发布） 的高清晰度音频编解码器的要求。

有关外部总线上 UAA 设备的要求的信息或 UAA 类驱动程序的信息，请参阅标题为的白皮书*通用音频体系结构*处[音频技术](https://go.microsoft.com/fwlink/p/?linkid=8751)网站。

在本文的其余部分只是指控制音频设备，用于连接到内部 bus、 实现 HD Audio 硬件寄存器，以及控制 UAA 符合 HD Audio 编解码器的 UAA 类驱动程序的版本。 此类驱动程序是 HD Audio 总线驱动程序的子级，并使用总线驱动程序的基线 HD 音频 DDI UAA 符合硬件编程。

HD Audio 编解码器在 UAA 类驱动程序：

-   为系统提供设备接口的音频编解码器或编解码器。

-   收集有关数字音频转换器、 音频到数字转换器和 HD 音频链接存在的编解码器中的 jack 存在检测 pin 信息。

-   音频编解码器或编解码器与第三方命令在启动时初始化。

-   获取和设置中的音频编解码器的音频的属性。

-   提供的流式接口 （映射到用户模式下的流的循环缓冲区，设置编解码器和 DMA 引擎和处理属性，如链接位置）。

-   处理音频编解码器中的电源管理。

未提供此类驱动程序：

-   动态编程中编解码器的音频效果节点的一种方法。

-   跨两个或多个编解码器以形成一个聚合的音频或调制解调器设备组合函数。

-   处理的通用 I/O (GPIO) 会固定小组件上，除非将它们显式定义 UAA 硬件要求文档中。

-   第三方代码的编程编解码器或提供软件效果插件模型。

 

 




