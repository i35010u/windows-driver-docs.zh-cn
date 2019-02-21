---
title: 高清晰度音频 DDI 版本之间的差异
description: 高清晰度音频 DDI 版本之间的差异
ms.assetid: e24071d3-9021-40c0-907a-91ada8a1306b
keywords:
- HD Audio，DDI 版本差异
- 高清晰度音频 (HD Audio) DDI 版本差异
- HDAUDIO_BUS_INTERFACE 结构
- HDAUDIO_BUS_INTERFACE_BDL 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37b50727c187b3910c925917bc68107c1d2ad560
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523888"
---
# <a name="differences-between-the-hd-audio-ddi-versions"></a>高清晰度音频 DDI 版本之间的差异


HD 音频 DDI 现已推出，如下所示定义的三个稍有不同版本：

-   HD 音频 DDI 由定义的基线版本[ **HDAUDIO\_总线\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff536413)结构。 音频和调制解调器编解码器的大多数函数驱动程序要求此 DDI 版本提供的功能。 此版本时可通过提供与 Windows XP 和 Windows Vista 的 HD Audio 总线驱动程序。

-   由定义 HD 音频 DDI 的增强的版本[ **HDAUDIO\_总线\_接口\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)结构。 此版本的 DDI 提供能够灵活地支持 DMA 驱动事件通知所需的其他功能。 它是在 Windows Vista 和更高版本的 Windows 中可用。

-   HD 音频 DDI 所定义的修改的版本[ **HDAUDIO\_总线\_接口\_BDL** ](https://msdn.microsoft.com/library/windows/hardware/ff536416)结构。 此版本可容纳的要求相对较少的音频和调制解调器驱动程序必须具有对安装程序的额外控制缓冲 DMA 操作描述符列表 (BDLs)。 此版本的 DDI 是适用于 Windows XP 和更高版本的 Windows。 但是，使用任一 HDAUDIO\_总线\_接口或 HDAUDIO\_总线\_接口\_V2 DDI 版本相反。 .

在所有三个结构的名称和类型的前五个成员与匹配的五个成员[**界面**](https://msdn.microsoft.com/library/windows/hardware/ff547825)结构。 有关这些成员的值的信息，请参阅[获取 HDAUDIO\_总线\_界面 DDI 对象](obtaining-an-hdaudio-bus-interface-ddi-object.md)，[获取 HDAUDIO\_总线\_接口\_V2 DDI 对象](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)或[获取 HDAUDIO\_总线\_接口\_BDL DDI 对象](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)。

HD 音频 DDI 的三个版本中的例程执行以下任务：

-   传输到编解码器的命令和检索到这些命令的响应。

-   分配和设置传输中呈现的数据，并捕获流的 DMA 引擎。

-   一个或多个 DMA 引擎将流状态更改为正在运行、 暂停、 停止状态，或重置。

-   呈现器的链接带宽预留，并捕获流。

-   提供直接访问权限的墙时钟寄存器并链接位置寄存器。

-   通知客户端的未经请求的响应的编解码器。

-   注册内核事件，以便他们可以接收 DMA 进度通知。

HDAUDIO\_总线\_界面和 HDAUDIO\_总线\_接口\_DDI BDL 版本具有以下差异：

-   HDAUDIO\_总线\_接口结构定义两个例程[ **AllocateDmaBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536179)并[ **FreeDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536391)，都不存在于 HDAUDIO\_总线\_接口\_BDL。

-   HDAUDIO\_总线\_界面\_BDL 结构定义三个例程[ **SetupDmaEngineWithBdl**](https://msdn.microsoft.com/library/windows/hardware/ff537894)， [ **AllocateContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536178)，并[ **FreeContiguousDmaBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536390)，都不存在于 HDAUDIO\_总线\_接口。

当客户端调用**AllocateDmaBuffer**例程中的第一个 DDI 版本，HD Audio 总线驱动程序：

-   DMA 缓冲区和 DMA 引擎 BDL 用于分配。

-   初始化 BDL。

-   要使用的缓冲区和 BDL 的 DMA 引擎设置。

与此相反， **AllocateContiguousDmaBuffer**例程在第二个 DDI 版本为 DMA 缓冲区和 BDL，分配存储，但依赖于调用方初始化 BDL。 **SetupDmaEngineWithBdl**例程将设置为 DMA 引擎使用缓冲区和调用方初始化 BDL。

BDL 包含的 DMA 引擎散播-聚集队列中的物理内存块的列表。 通过调用**SetupDmaEngineWithBdl**若要设置 BDL，客户端可以指定的点的 DMA 引擎生成中断该数据流中。 客户端是通过在所选 BDL 条目中设置完成时中断 (IOC) 位。 借助此功能，客户端可以精确地控制音频流的处理过程中出现的 IOC 中断的时间。 音频调制解调器驱动程序还使用第二个 DDI 版本获取准确的系统时钟信息。

有关详细信息，请参阅*Intel 高定义音频规范*。

但是，几乎所有客户端将使用 HDAUDIO\_总线\_DDI 界面版本。 只有需要精确控制的中断时间的几个客户端将使用 HDAUDIO\_总线\_接口\_BDL 版本。

 

 




