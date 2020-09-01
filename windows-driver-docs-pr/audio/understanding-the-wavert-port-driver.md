---
title: 了解 WaveRT 端口驱动程序
description: 了解 WaveRT 端口驱动程序
ms.assetid: 2627615a-3fde-4ed6-9f7f-f6d7e5d82b3b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f801002504e67e72c181f6ec55e4a3bfde1d674b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210319"
---
# <a name="understanding-the-wavert-port-driver"></a>了解 WaveRT 端口驱动程序


WaveRT 端口驱动程序将上一 WaveCyclic 端口驱动程序的简单性与 WavePci 端口驱动程序的硬件加速性能相结合。

WaveRT 端口驱动程序无需通过提供其主客户端 (（通常为音频引擎) 并直接访问数据缓冲区）来持续映射和复制音频数据。 这种直接访问还消除了驱动程序在音频流中操作数据的需要。 因此，WaveRT 端口驱动程序可满足某些音频设备 (DMA) 控制器的直接内存访问需求。

若要将自身与其他波形呈现和 wave 捕获设备区分开来，WaveRT 端口驱动程序除了[**KSCATEGORY \_ 音频**](../install/kscategory-audio.md)、 [**KSCATEGORY \_ 呈现**](../install/kscategory-render.md)和[**KSCATEGORY \_ 捕获**](../install/kscategory-capture.md)外，还会将其自身注册到[**KSCATEGORY \_ 实时**](../install/kscategory-realtime.md)。 此自注册在安装适配器驱动程序的过程中发生。

在 Windows Vista 和更高版本的操作系统中，当操作系统启动并初始化音频引擎时，音频引擎会枚举代表音频设备的 KS 筛选器。 在枚举过程中，音频引擎实例化所找到的音频设备的驱动程序。 此过程将导致为这些设备创建筛选器对象。 对于 WaveRT 音频设备，生成的筛选器对象具有以下组件：

-   用于管理筛选器的泛型系统函数的 WaveRT 端口驱动程序的实例

-   用于处理筛选器的所有硬件特定函数的 WaveRT 微型端口驱动程序的实例

创建筛选器对象后，音频引擎和 WaveRT 微型端口驱动程序可以为所需的音频处理类型打开音频流。 若要为 (播放) 的音频呈现准备 KS 筛选器，例如音频引擎和 WaveRT 微型端口驱动程序，请执行以下操作来打开播放流：

1.  音频引擎打开 KS 筛选器上的 pin，WaveRT 微型端口驱动程序创建 pin 的实例。 当音频引擎打开 pin 时，它还会将流的波形格式传递给驱动程序。 驱动程序使用波形格式信息在下一步中选择适当的缓冲区大小。

2.  对于要创建的特定大小的循环缓冲区，音频引擎会将请求发送到微型端口驱动程序。 术语 " *循环缓冲区* " 是指当缓冲区位置寄存器在播放或记录操作中到达缓冲区末尾时，位置寄存器可自动环绕到缓冲区的开头。 与设置连续物理内存块的 WaveCyclic 微型端口驱动程序不同，WaveRT 微型端口驱动程序不需要在物理内存中连续的缓冲区。 驱动程序使用 [**KSPROPERTY \_ RTAUDIO \_ BUFFER**](./ksproperty-rtaudio-buffer.md) 属性为缓冲区分配空间。 如果音频设备的硬件无法从请求大小的缓冲区进行流式处理，则驱动程序将在音频设备的资源限制内工作，以创建最接近原始请求大小的缓冲区。 然后，该驱动程序将缓冲区映射到音频设备的 DMA 引擎，并使音频引擎在用户模式下可以访问该缓冲区。

3.  音频引擎计划一个线程定期将音频数据写入循环缓冲区。

4.  如果音频设备的硬件不提供对循环缓冲区的直接支持，微型端口驱动程序会定期 reprograms 音频设备，以便继续使用同一缓冲区。 例如，如果硬件不支持缓冲区循环，则每次到达缓冲区末尾时，驱动程序必须将 DMA 地址设置回缓冲区的起始处。 此更新可在 (ISR) 或高优先级线程的中断服务例程中完成。

生成的配置在音频设备硬件上提供了有问题的复原音频信号，该信号支持循环缓冲或与微型端口驱动程序一起定期更新其硬件。

若要为音频捕获准备 KS 筛选器 (录制) ，音频引擎和 WaveRT 微型端口驱动程序使用类似的步骤打开记录流。

WaveRT 端口驱动程序所提供的性能改进之一是减少波形渲染或波形捕获期间音频流的端到端处理延迟。 此延迟称为流延迟。

有关这两种类型的流延迟的详细信息，请参阅以下主题。

-   [播放期间的流延迟](stream-latency-during-playback.md)

-   [录制过程中的流延迟](stream-latency-during-recording.md)

有关如何开发补充 WaveRT 端口驱动程序的 WaveRT 微型端口驱动程序的信息，请参阅 [开发 WaveRT 微型端口驱动程序](developing-a-wavert-miniport-driver.md) 主题。

 

