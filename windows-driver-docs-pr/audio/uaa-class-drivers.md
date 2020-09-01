---
title: UAA 类驱动程序
description: UAA 类驱动程序
ms.assetid: 57f8f6fe-53a9-4ef1-b4f6-715232e88fdf
keywords:
- HD 音频，通用音频体系结构
- 高清晰音频 (HD 音频) ，通用音频体系结构
- UAA WDK
- 通用音频体系结构 WDK
- 类驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dbd00078e3f8da5dfd41d962fce5d27a20017e3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209917"
---
# <a name="uaa-class-drivers"></a>UAA 类驱动程序


在 Windows Vista 中，Microsoft 为音频设备提供 UAA 类驱动程序，用于连接到内部总线 (PCI) 或 (IEEE 1394 或 USB) 的外部总线。 若要为特定总线的 UAA 类驱动程序提供支持，设备必须符合该总线的 UAA 硬件规范。 对于内部总线上的设备，UAA 硬件要求文档指定以下各项：

-   HD 音频控制器的注册集，其中包含在 [高清音频体系结构的 UAA 扩展](uaa-extensions-to-the-hd-audio-architecture.md)中讨论的少量更改。

-   )  (发布 HD 音频编解码器的要求。

有关 UAA 设备在外部总线上的要求或有关 UAA 类驱动程序的信息，请参阅 [通用音频体系结构](/previous-versions/windows/hardware/design/dn640534(v=vs.85)) 白皮书。

本讨论的其余部分仅涉及控制音频设备的 UAA 类驱动程序版本，该设备连接到内部总线，实现 HD 音频硬件注册，并控制与 UAA 兼容的 HD 音频编解码器。 此类驱动程序是 HD 音频总线驱动程序的子驱动程序，它使用总线驱动程序的基线 HD 音频 DDI 来编程符合 UAA 标准的硬件。

HD 音频编解码器的 UAA 类驱动程序：

-   为系统提供音频编解码器或编解码器的设备接口。

-   收集有关 HD 音频链接上存在的编解码器中的数字到音频转换器、音频到数字转换器和插孔存在检测 pin 的信息。

-   在启动时用第三方命令初始化音频编解码器或编解码器。

-   获取和设置音频编解码器中的音频属性。

-   提供了一个流式处理接口， (将流的循环缓冲区映射到用户模式，设置编解码器和 DMA 引擎，并处理属性（如链接位置) ）。

-   处理音频编解码器中的电源管理。

此类驱动程序不提供：

-   一种动态编程编解码器中的音频效果节点的方式。

-   将函数跨两个或更多编解码器组合起来形成一个聚合音频或调制解调器设备。

-   除非在 UAA 硬件要求文档中明确定义了常规用途 i/o，否则无法处理小组件上的 (GPIO) 针。

-   用于编程编解码器或提供软件效果的第三方代码的插件模型。

 

