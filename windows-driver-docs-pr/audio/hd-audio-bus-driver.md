---
title: 高清晰度音频总线驱动程序
description: 高清晰度音频总线驱动程序
ms.assetid: a08f4304-467b-45cf-8026-87f41b408692
keywords:
- 高清晰度音频，通用音频体系结构
- 高清晰度音频 （HD 音频） 通用音频体系结构
- UAA WDK
- 通用音频体系结构 WDK
- 总线驱动程序 WDK 音频
- HD Audio，总线驱动程序
- 高清晰度音频 (HD Audio) 总线驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a15802a495212ec51a559917614093d565ca1c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555893"
---
# <a name="hd-audio-bus-driver"></a>高清晰度音频总线驱动程序


HD Audio 总线驱动程序是唯一的软件组件来直接访问硬件的 HD Audio 总线界面控制器注册。 总线驱动程序公开 HD 音频 DDI 的子级-实例的功能的驱动程序，用于控制音频和调制解调器的编解码器-可以使用 HD Audio 控制器硬件进行编程。 此外，总线驱动程序管理的 HD 音频链接硬件资源，其中包括的 DMA 引擎和总线带宽。 功能的驱动程序分配和释放这些资源通过 HD 音频 DDI。

HD Audio 总线驱动程序：

-   查询在总线上的编解码器，并创建管理编解码器的子级。

-   处理中断服务例程 (Isr) 的未经请求的响应并传播到其子未经请求的响应。

-   将其子级中的命令传递给编解码器，并从编解码器检索响应。

-   设置传输到或从循环缓冲区数据的 DMA 引擎。

-   管理 HD 音频链接上的总线带宽资源。

-   提供对墙时钟寄存器和链接位置寄存器的访问。

-   提供了已同步的启动和停止的流的组。

HD Audio 总线驱动程序不提供：

-   用于编程 DSP 或 Intel 高定义音频规范中未定义的其他寄存器的接口。

-   按优先顺序排列的带宽管理。

在设备枚举期间 HD Audio 总线驱动程序检测到连接到高清晰度音频控制器的 HD 音频链路的编解码器。 对于每个编解码器，总线驱动程序将为它找到编解码器中的每个函数组加载一个功能驱动程序 （如果可用）。 有关函数组的信息，请参阅 Intel 高定义音频规范[Intel HD Audio](https://go.microsoft.com/fwlink/p/?linkid=42508)网站。

 

 




