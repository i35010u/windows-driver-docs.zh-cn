---
title: HD 音频 DDI 版本之间的差异
description: HD 音频 DDI 版本之间的差异
keywords:
- HD 音频，DDI 版本差异
- 高清晰音频 (HD 音频) ，DDI 版本差异
- HDAUDIO_BUS_INTERFACE 结构
- HDAUDIO_BUS_INTERFACE_BDL 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d5a257294b5193354199efdfc1bd8b67157f63e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784865"
---
# <a name="differences-between-the-hd-audio-ddi-versions"></a>HD 音频 DDI 版本之间的差异


HD 音频 DDI 提供三个略有不同的版本，如下所示：

-   HD 音频 DDI 的基线版本，由 [**HDAUDIO \_ 总线 \_ 接口**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface) 结构定义。 大多数音频和调制解调器编解码器函数驱动程序只需要此 DDI 版本所提供的功能。 此版本通过随 Windows XP 和 Windows Vista 一起提供的 HD 音频总线驱动程序提供。

-   [**HDAUDIO \_ 总线 \_ 接口 \_ V2**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)结构定义的 HD 音频 DDI 的增强版本。 此版本的 DDI 提供了支持具有灵活性的 DMA 驱动事件通知所需的附加功能。 它在 Windows Vista 和更高版本的 Windows 中可用。

-   [**HDAUDIO \_ 总线 \_ 接口 \_ BDL**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构定义的 HD 音频 DDI 的修改版本。 此版本满足相对较少的音频和调制解调器驱动程序的要求，这些驱动程序必须对 (BDLs) 进行 DMA 操作的缓冲描述符列表的设置进行更多的控制。 此版本的 DDI 适用于 Windows XP 和更高版本的 Windows。 不过，请改为使用 HDAUDIO \_ 总线 \_ 接口或 HDAUDIO \_ 总线 \_ 接口 \_ V2 DDI 版本。 .

在所有三个结构中，前五个成员的名称和类型与 [**接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface) 结构的五个成员的名称和类型匹配。 有关这些成员的值的信息，请参阅 [获取 HDAUDIO \_ BUS \_ 接口 ddi 对象](obtaining-an-hdaudio-bus-interface-ddi-object.md)、 [获取 HDAUDIO \_ 总线 \_ 接口 \_ V2 DDI](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md) 对象或 [获取 HDAUDIO \_ 总线 \_ 接口 \_ BDL ddi 对象](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)。

高清音频 DDI 三个版本中的例程执行以下任务：

-   将命令传输到编解码器，并检索对这些命令的响应。

-   分配并设置 DMA 引擎以在呈现和捕获流中传输数据。

-   将一个或多个 DMA 引擎的流状态更改为正在运行、已暂停、已停止或已重置。

-   保留呈现和捕获流的链接带宽。

-   提供对墙壁时钟寄存器和链接位置寄存器的直接访问。

-   通知客户端来自编解码器的未经请求的响应。

-   注册内核事件，使其能够接收 DMA 进度通知。

HDAUDIO \_ 总线 \_ 接口和 HDAUDIO \_ 总线 \_ 接口 \_ BDL 版本具有以下差异：

-   HDAUDIO \_ 总线 \_ 接口结构定义了 [**AllocateDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer) 和 [**FreeDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)这两个例程，这些例程在 HDAUDIO \_ BUS \_ interface \_ BDL 中不存在。

-   HDAUDIO \_ bus \_ interface \_ BDL 结构定义了3个例程： [**SetupDmaEngineWithBdl**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)、 [**ALLOCATECONTIGUOUSDMABUFFER**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)和 [**FreeContiguousDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)，它们在 HDAUDIO BUS 接口中不存在 \_ \_ 。

当客户端在第一个 DDI 版本中调用 **AllocateDmaBuffer** 例程时，HD 音频总线驱动程序：

-   分配 DMA 缓冲区和 BDL 以供 DMA 引擎使用。

-   初始化 BDL。

-   将 DMA 引擎设置为使用缓冲区和 BDL。

相反，第二个 DDI 版本中的 **AllocateContiguousDmaBuffer** 例程为 DMA 缓冲区和 BDL 分配存储，但依赖于调用方来初始化 BDL。 **SetupDmaEngineWithBdl** 例程将 DMA 引擎设置为使用缓冲区和调用方初始化的 BDL。

BDL 包含 DMA 引擎的分散/收集队列中的物理内存块的列表。 通过调用 **SetupDmaEngineWithBdl** 来设置 BDL，客户端可以在数据流中指定 DMA 引擎生成中断的点。 客户端通过在所选 BDL 项中的) 位上设置 " (完成后中断" 来执行此项。 利用此功能，客户端可以精确控制在处理音频流期间发生的 IOC 中断的时间。 音频调制解调器驱动程序还使用第二个 DDI 版本来获取准确的系统时钟信息。

有关详细信息，请参阅 *Intel 高质音频规范*。

不过，几乎所有的客户端都将使用 DDI 的 HDAUDIO \_ 总线 \_ 接口版本。 只有几个需要精确控制中断计时的客户端才会使用 HDAUDIO \_ 总线 \_ 接口 \_ BDL 版本。

 

