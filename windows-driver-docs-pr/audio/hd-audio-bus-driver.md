---
title: HD 音频总线驱动程序
description: HD 音频总线驱动程序
keywords:
- HD 音频，通用音频体系结构
- 高清晰音频 (HD 音频) ，通用音频体系结构
- UAA WDK
- 通用音频体系结构 WDK
- 总线驱动程序 WDK 音频
- HD 音频，总线驱动程序
- 高清晰音频 (HD 音频) ，总线驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c01f04b087446b3fdea338ba7c217d3c04de70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786509"
---
# <a name="hd-audio-bus-driver"></a>HD 音频总线驱动程序


HD 音频总线驱动程序是唯一直接访问 HD 音频总线接口控制器的硬件寄存器的软件组件。 总线驱动程序公开了 HD 音频 DDI，其中的子（控制音频和调制解调器编解码器的函数驱动程序的实例）可用于对 HD 音频控制器硬件进行编程。 此外，总线驱动程序还管理 HD 音频链接硬件资源，其中包括 DMA 引擎和总线带宽。 函数驱动程序通过 HD audio DDI 分配和释放这些资源。

HD 音频总线驱动程序：

-   在总线上查询编解码器，并创建子编解码器来管理编解码器。

-   处理 (Isr) 的中断服务例程，以获取未经请求的响应，并将未经请求的响应传播到其子代。

-   将命令从其子编解码器传递到编解码器，并从编解码器检索响应。

-   设置在循环缓冲区之间传输数据的 DMA 引擎。

-   管理 HD 音频链接上的总线带宽资源。

-   提供对墙壁时钟寄存器和链接位置寄存器的访问。

-   提供同步的流组的启动和停止。

HD 音频总线驱动程序未提供：

-   用于对未在 Intel 高质音频规范中定义的 DSP 或其他寄存器进行编程的接口。

-   优先带宽管理。

在设备枚举过程中，HD 音频总线驱动程序检测附加到 HD audio 控制器的 HD 音频链接的编解码器。 对于每个编解码器，总线驱动程序会加载一个函数驱动程序 (如果它在编解码器内找到的每个函数组都可用) 。 有关函数组的信息，请参阅 [INTEL HD 音频](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html) 网站上的 Intel 高质音频规范。

 

 




