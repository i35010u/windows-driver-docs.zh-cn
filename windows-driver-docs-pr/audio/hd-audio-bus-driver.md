---
title: HD 音频总线驱动程序
description: HD 音频总线驱动程序
ms.assetid: a08f4304-467b-45cf-8026-87f41b408692
keywords:
- HD 音频，通用音频体系结构
- 高清晰音频（HD 音频），通用音频体系结构
- UAA WDK
- 通用音频体系结构 WDK
- 总线驱动程序 WDK 音频
- HD 音频，总线驱动程序
- 高清晰音频（HD 音频），总线驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6885db4038e3dedc0e7f53cccbe914b4ef6820ad
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925584"
---
# <a name="hd-audio-bus-driver"></a>HD 音频总线驱动程序


HD 音频总线驱动程序是唯一直接访问 HD 音频总线接口控制器的硬件寄存器的软件组件。 总线驱动程序公开了 HD 音频 DDI，其中的子（控制音频和调制解调器编解码器的函数驱动程序的实例）可用于对 HD 音频控制器硬件进行编程。 此外，总线驱动程序还管理 HD 音频链接硬件资源，其中包括 DMA 引擎和总线带宽。 函数驱动程序通过 HD audio DDI 分配和释放这些资源。

HD 音频总线驱动程序：

-   在总线上查询编解码器，并创建子编解码器来管理编解码器。

-   处理非请求响应的中断服务例程（Isr），并将未经请求的响应传播到其子代。

-   将命令从其子编解码器传递到编解码器，并从编解码器检索响应。

-   设置在循环缓冲区之间传输数据的 DMA 引擎。

-   管理 HD 音频链接上的总线带宽资源。

-   提供对墙壁时钟寄存器和链接位置寄存器的访问。

-   提供同步的流组的启动和停止。

HD 音频总线驱动程序未提供：

-   用于对未在 Intel 高质音频规范中定义的 DSP 或其他寄存器进行编程的接口。

-   优先带宽管理。

在设备枚举过程中，HD 音频总线驱动程序检测附加到 HD audio 控制器的 HD 音频链接的编解码器。 对于每个编解码器，总线驱动程序会为它在编解码器内找到的每个函数组加载一个函数驱动程序（如果可用）。 有关函数组的信息，请参阅[INTEL HD 音频](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html)网站上的 Intel 高质音频规范。

 

 




