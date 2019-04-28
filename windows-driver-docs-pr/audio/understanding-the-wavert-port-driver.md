---
title: 了解 WaveRT 端口驱动程序
description: 了解 WaveRT 端口驱动程序
ms.assetid: 2627615a-3fde-4ed6-9f7f-f6d7e5d82b3b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c495206b0b47b05d8c099e3e76093a26e624c51a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335356"
---
# <a name="understanding-the-wavert-port-driver"></a>了解 WaveRT 端口驱动程序


WaveRT 端口驱动程序将以前的 WaveCyclic 端口驱动程序的简单性与硬件加速 WavePci 端口驱动程序的性能相结合。

WaveRT 端口驱动程序无需不断地将映射并复制通过直接访问数据缓冲区提供其主要的客户端 （通常情况下，音频引擎） 的音频数据。 这种直接访问还消除了驱动程序处理的音频流中的数据需求。 WaveRT 端口驱动程序因此适合于某些音频设备具有的直接内存访问 (DMA) 控制器的需求。

为了区分从其他波形呈现和批捕获设备本身，WaveRT 端口驱动程序注册下启用自身[ **KSCATEGORY\_实时**](https://msdn.microsoft.com/library/windows/hardware/ff548485)除了[ **KSCATEGORY\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff548261)， [ **KSCATEGORY\_呈现**](https://msdn.microsoft.com/library/windows/hardware/ff548493)并[ **KSCATEGORY\_捕获**](https://msdn.microsoft.com/library/windows/hardware/ff548325)。 在适配器驱动程序的安装期间发生此自注册。

在 Windows Vista 和更高版本操作系统中，当操作系统启动并初始化音频引擎时，音频引擎枚举表示的音频设备的 KS 筛选器。 在枚举过程音频引擎实例化它找到的音频设备的驱动程序。 此过程会导致这些设备的筛选器对象的创建。 WaveRT 音频设备生成的筛选器对象具有以下组件：

-   WaveRT 端口驱动程序管理的筛选器的一般系统函数的实例

-   WaveRT 微型端口驱动程序来处理筛选器的所有特定于硬件的函数的实例

创建筛选器对象后，音频引擎和 WaveRT 微型端口驱动程序将准备好打开音频处理所需的类型的音频流。 若要准备音频呈现 （播放） KS 筛选器，例如，音频引擎和 WaveRT 微型端口驱动程序执行以下操作以打开一个播放流：

1.  音频引擎打开 KS 筛选器，pin 和 WaveRT 微型端口驱动程序创建 pin 的实例。 当音频引擎打开 pin 时，它还到驱动程序将流的波形格式。 驱动程序使用波形格式信息在下一步中选择适当的缓冲区大小。

2.  音频引擎循环要创建一个特定大小的缓冲区将请求发送到微型端口驱动程序。 术语*循环缓冲区*指这样一个事实，当缓冲区位置注册到达播放或录制操作中的缓冲区的末尾，位置注册可以自动环绕在周围到缓冲区的开头。 与设置的物理内存的连续块 WaveCyclic 微型端口驱动程序，不同 WaveRT 微型端口驱动程序不需要是连续的物理内存中的缓冲区。 驱动程序使用[ **KSPROPERTY\_RTAUDIO\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff537370)属性可为缓冲区分配空间。 如果音频设备的硬件不能从所请求大小的缓冲区的数据流，该驱动程序将在创建最接近的大小最初请求的大小的缓冲区的音频设备的资源限制中工作。 然后，驱动程序将缓冲区映射到音频设备的 DMA 引擎，并使缓冲区可访问到音频引擎在用户模式下。

3.  音频引擎将安排一个线程来定期将音频数据写入到循环缓冲区。

4.  如果音频设备的硬件不提供直接支持的循环缓冲区，微型端口驱动程序将定期 reprograms 音频设备，若要继续使用同一缓冲区。 例如，如果硬件不支持循环缓冲区，该驱动程序必须设置 DMA 地址返回到的缓冲区开始每次到达缓冲区末尾。 可以在中断服务例程 (ISR) 或较高优先级的线程中执行此更新。

生成的配置提供支持循环缓冲区或适用于要定期更新其硬件的微型端口驱动程序的音频设备硬件上的故障复原音频信号。

若要准备 （记录） 的音频捕获 KS 筛选器，音频引擎和 WaveRT 微型端口驱动程序使用类似的步骤以打开一个记录的流。

WaveRT 端口驱动程序提供的性能改进之一是可减少在端到端处理过程中延迟的音频流批呈现或批捕获。 此延迟称为流延迟。

有关流延迟这两种类型的详细信息，请参阅以下主题。

-   [在播放期间则 Stream 延迟](stream-latency-during-playback.md)

-   [录制期间的 Stream 延迟](stream-latency-during-recording.md)

有关如何开发 WaveRT 微型端口驱动程序的补充 WaveRT 端口驱动程序的信息，请参阅[开发 WaveRT 微型端口驱动程序](developing-a-wavert-miniport-driver.md)主题。

 

 




