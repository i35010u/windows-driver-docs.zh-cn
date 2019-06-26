---
title: WavePci 微型端口驱动程序的性能问题
description: WavePci 微型端口驱动程序的性能问题
ms.assetid: 785fd743-0c78-44cd-95bf-1f961aa414b5
keywords:
- WavePci 性能问题 WDK 音频
- 维护机制 WDK 音频进行流式处理
- 硬件中断 WDK 音频
- 中断服务例程 WDK 音频
- Isr WDK 音频
- 计时器 Dpc WDK 音频
- 暂停/ACQUIRE 优化 WDK 音频
- IPreFetchOffset
- 同步基元 WDK 音频
- IPinCount
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b01f7fed0f8be3db6c5f3ddbd97fc1e97a1ab129
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362579"
---
# <a name="performance-issues-for-a-wavepci-miniport-driver"></a>WavePci 微型端口驱动程序的性能问题


## <span id="performance_issues_for_a_wavepci_miniport_driver"></span><span id="PERFORMANCE_ISSUES_FOR_A_WAVEPCI_MINIPORT_DRIVER"></span>


按照这些一般原则，就大大降低对系统的音频驱动程序的性能影响：

-   最小化在正常操作期间运行的代码。

-   运行代码仅在必要时。

-   请考虑总系统资源消耗 （而不仅仅是 CPU 加载）。

-   优化代码的速度和大小。

此外，WavePci 微型端口驱动程序必须满足几个特定于音频设备的性能问题。 下面的讨论主要处理音频呈现问题，尽管某些建议的技术适用于以及音频捕获。

### <a name="span-idstreamservicingmechanismsspanspan-idstreamservicingmechanismsspanspan-idstreamservicingmechanismsspanstream-servicing-mechanisms"></a><span id="Stream_Servicing_Mechanisms"></span><span id="stream_servicing_mechanisms"></span><span id="STREAM_SERVICING_MECHANISMS"></span>Stream 维护机制

在讨论之前的性能优化，一些背景知识有必要了解维护服务流的 WavePci 机制。

当处理批呈现或捕获流时，音频设备都需要定期维护的微型端口驱动程序。 新的映射可用于流时，该驱动程序会将相应的映射添加到流的 DMA 队列。 该驱动程序还从队列中删除已处理的任何映射。 有关映射的信息，请参阅[WavePci 延迟](wavepci-latency.md)。

若要执行维护，微型端口驱动程序提供任一*延迟过程调用 (DPC)* 或中断服务例程 (ISR)，具体取决于是否将间隔设置由系统计时器或 DMA 驱动中断。 在后一种情况下，DMA 硬件通常会触发中断每次，如果完成传输一定量的数据流。

每次 DPC 或 ISR 执行，它将确定哪些流将需要维修。 DPC 或 ISR 服务流通过调用[ **IPortWavePci::Notify** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)方法。 此方法将调用参数作为流的服务组，这是类型的对象[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)。 **通知**方法调用的服务组[ **RequestService** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicesink-requestservice)方法 (请参阅**IServiceSink::RequestService**)。

服务组对象包含一组对象的类型的服务接收器[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)。 [IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)派生自 IServiceSink，并且这两个接口具有[ **RequestService** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicesink-requestservice)方法。 当[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)方法调用的服务组**RequestService**方法，通过调用做出响应的服务组**RequestService**接收器组中的每个服务的方法。

流的服务组包含至少一个服务接收器，端口驱动程序将添加到紧跟创建流的服务组。 端口驱动程序调用微型端口驱动程序[ **IMiniportWavePci::NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)方法以获取服务组的指针。 服务接收器[ **RequestService** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicesink-requestservice)方法是端口驱动程序的特定于流的服务例程。 此例程将执行以下操作：

-   调用微型端口驱动程序[ **IMiniportWavePciStream::Service** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-service)方法。

-   自上次服务例程执行触发任何新挂起的位置或流上的时钟事件。

如中所述[KS 事件](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)，可以注册客户端流达到某个特定位置或在一个时钟到达特定时间戳时收到通知。 [ **NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)方法具有不提供服务组，在其中用例端口驱动程序设置其自己的计时器划出到其服务例程的调用之间的时间间隔的选项。

像[ **NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)方法、 微型端口驱动程序[ **IMiniportWavePci::Init** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-init)方法还会输出指向服务组. 遵循**Init**调用时，端口驱动程序将其服务接收器添加到服务组。 此特定服务接收器作为一个整体包含筛选器的服务例程。 （上一段中介绍的筛选器上的 pin 与关联的流的服务接收器。）此服务例程调用微型端口驱动程序[ **IMiniportWavePci::Service** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-service)方法。 服务例程执行每次的 DPC 或 ISR 调用[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)与服务组的筛选器。 **Init**方法具有不提供用例端口驱动程序永远不会调用其筛选器服务例程的服务组的选项。

### <a name="span-idhardwareinterruptsspanspan-idhardwareinterruptsspanspan-idhardwareinterruptsspanhardware-interrupts"></a><span id="Hardware_Interrupts"></span><span id="hardware_interrupts"></span><span id="HARDWARE_INTERRUPTS"></span>硬件中断

某些微型端口驱动程序生成过多或没有足够的硬件中断。 DirectSound 采用硬件加速某些 WavePci 呈现设备中的硬件中断时发生仅可以提供的映射是几乎已耗尽，呈现引擎处于资源不足的风险。 在其他硬件加速 WavePci 设备的硬件中断上完成每个单个映射或其他相对较小的间隔发生。 在这种情况下，ISR 经常发现它几乎没有什么要做，但每个中断仍会消耗系统资源使用寄存器交换和缓存重新加载。 提高驱动程序性能的第一步是降低的最大程度地中断的数量，而不会有资源不足的风险。 消除不必要的中断之后, 可以通过设计 ISR 来更高效地执行实现额外的性能提升。

在某些驱动程序，Isr 浪费时间通过调用的流[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)方法每次发生时的硬件中断-而不考虑是否真正运行流。 如果任何流不都处于运行状态，然后 DMA 为非活动状态，和尝试获取映射、 发布映射，所用的任何时间或浪费任何流中的新事件中查找。 高效的驱动程序，ISR 验证调用的流之前，正在运行的流**通知**方法。

但是，使用这种类型的 ISR 的驱动程序需要确保所有挂起的上一个流的事件流退出运行状态时触发。 否则为事件可能会延迟或丢失。 仅在早于 Microsoft Windows XP 操作系统中运行暂停转换过程中出现此问题。 在 Windows XP 及更高版本，端口驱动程序会自动向发出信号，任何未完成的位置事件流更改状态时立即运行暂停。 在旧版本的操作系统，但是，微型端口驱动程序是负责触发任何未完成的事件，从而最终调用[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)立即暂停流之后。 有关详细信息，请参阅下面暂停/ACQUIRE 优化。

典型的 WavePci 微型端口驱动程序管理中的单个播放流[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)。 KMixer 的当前实现将三个映射 Irp 的最少的数据进行缓冲播放流。 每个 IRP 包含约为 10 毫秒的音频足够缓冲区存储。 如果微型端口驱动程序触发的硬件中断 DMA 控制器完成 IRP 中的最后一个映射与每个时间，中断应定期出现相当 10 毫秒，这是频繁地占用保持 DMA 队列。 

### <a name="span-idtimerdpcsspanspan-idtimerdpcsspanspan-idtimerdpcsspantimer-dpcs"></a><span id="Timer_DPCs"></span><span id="timer_dpcs"></span><span id="TIMER_DPCS"></span>计时器 dpc 进行标记

如果驱动程序管理任何硬件加速 DirectSound 流，则应使用计时器 DPC (请参阅[计时器对象和 dpc 进行标记](https://docs.microsoft.com/windows-hardware/drivers/kernel/timer-objects-and-dpcs)) 而不是 DMA 驱动硬件中断。 同样地，载入计时器 PCI 张数据卡 WavePci 设备可以使用而不是 DPC 的计时器驱动的硬件中断。

DirectSound 缓冲区中，对于整个缓冲区可以附加到单个 IRP。 如果缓冲区很大，并且仅在它达到缓冲区的末尾时，微型端口驱动程序计划的硬件中断，后续中断可能因此大 DMA 队列解决。 此外，如果驱动程序管理大量的硬件加速 DirectSound 流，并且每个流生成其自己的中断时，所有中断的累积影响会降低系统性能。 在这些情况下，微型端口驱动程序应避免使用硬件中断计划维护的各个流。 相反，它应为服务中计划定期运行计时器生成单个 DPC 的所有流。

通过将计时器间隔设置为 10 毫秒，连续 DPC 执行之间的间隔为类似于前面所述的在单个 KMixer 播放流的情况下的硬件中断。 因此，DPC 可以处理 KMixer 播放流除硬件加速 DirectSound 流。

当最后一个流退出运行状态时，微型端口驱动程序应禁用此计时器 DPC，若要避免浪费系统 CPU 周期。 立即禁用之后 DPC，该驱动程序应确保刷新任何时钟或位置上的事件挂起之前运行流。 在 Windows 98 / Me 和 Windows 2000 中，该驱动程序应调用[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)触发任何挂起的上在暂停的流的事件。 在 Windows XP 及更高版本，操作系统会触发任何挂起的事件流退出运行状态，而无需干预的微型端口驱动程序时自动。

### <a name="span-idpauseacquireoptimizationsspanspan-idpauseacquireoptimizationsspanspan-idpauseacquireoptimizationsspanpauseacquire-optimizations"></a><span id="PAUSE_ACQUIRE_Optimizations"></span><span id="pause_acquire_optimizations"></span><span id="PAUSE_ACQUIRE_OPTIMIZATIONS"></span>暂停/ACQUIRE 优化

在 Windows 98 / Me 和 Windows 2000，WavePci 端口驱动程序流式传输服务例程 ( [ **RequestService** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicesink-requestservice)方法) 始终生成微型端口驱动程序调用[ **IMiniportWavePciStream::Service** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-service)方法而不考虑该流是否处于运行状态。 在这些操作系统**服务**方法应检查流是否正在运行的时间之前执行实际工作。 (但是，如果微型端口驱动程序的 DPC 或 ISR 具有已经过优化，可调用[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)仅为流的运行，将添加到此检查**服务**方法可能是冗余。）

此优化不需要在 Windows XP 和更高版本，因为[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)方法调用[**服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-service)方法仅在正在运行的流。

### <a name="span-idusingtheiprefetchoffsetinterfacespanspan-idusingtheiprefetchoffsetinterfacespanspan-idusingtheiprefetchoffsetinterfacespanusing-the-iprefetchoffset-interface"></a><span id="Using_the_IPreFetchOffset_Interface"></span><span id="using_the_iprefetchoffset_interface"></span><span id="USING_THE_IPREFETCHOFFSET_INTERFACE"></span>使用 IPreFetchOffset 接口

DirectSound 用户熟悉双 play 游标和写入光标的概念。 Play 光标指示正在从设备 （目前为 DAC 的示例驱动程序的最佳估计） 发出的数据的流中的位置。 写入位置是客户端写入其他数据的下一个安全位置的流中的位置。 对于 WavePci，默认的假设是映射的写入光标位于末尾的最后一个请求。 如果微型端口驱动程序已获得大量的未完成的映射，play 游标和写入光标之间的偏移量可能会非常大，足以某些 WHQL 音频位置测试失败。 在 Windows XP 及更高版本， [IPreFetchOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iprefetchoffset)接口，解决这些问题。

微型端口驱动程序将使用[IPreFetchOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iprefetchoffset)指定总线 master 硬件预提取特征，很大程度上由硬件先进先出的大小。 音频子系统使用此数据来设置 play 游标和写入光标之间的常量偏移量。 此常量偏移量，可以显著小于默认偏移量，充分利用这一事实数据可将写入一个映射即使映射交给硬件，前提是 play 游标是足够的距离位置在其中写入数据。 （此语句假定该驱动程序不会复制或以其他方式操作映射中的数据）。典型的偏移量可能会达到大约 64 示例，具体取决于引擎设计中。 在如此小的偏移量，与 WavePci 驱动程序时，可以是完全响应能力和功能仍在请求大量的映射。

请注意 DirectSound 当前 10 毫秒填充写入光标的硬件加速的 pin。

有关详细信息，请参阅[预提取偏移量](prefetch-offsets.md)。

### <a name="span-idprocessingdatainmappingsspanspan-idprocessingdatainmappingsspanspan-idprocessingdatainmappingsspanprocessing-data-in-mappings"></a><span id="Processing_Data_in_Mappings"></span><span id="processing_data_in_mappings"></span><span id="PROCESSING_DATA_IN_MAPPINGS"></span>在映射中处理数据

避免接触映射中的数据，如有可能你的硬件驱动程序。 应将数据映射中包含的任何软件处理拆分为独立于硬件的驱动程序软件筛选器。 具有执行此类处理的硬件驱动程序可减少其效率，并创建延迟问题。

硬件驱动程序应尽可能透明有关其的真实硬件功能。 该驱动程序应永远不会声明实际上在软件中执行数据转换为提供硬件支持。

### <a name="span-idsynchronizationprimitivesspanspan-idsynchronizationprimitivesspanspan-idsynchronizationprimitivesspansynchronization-primitives"></a><span id="Synchronization_Primitives"></span><span id="synchronization_primitives"></span><span id="SYNCHRONIZATION_PRIMITIVES"></span>同步基元

驱动程序是不太可能具有现在和将来的死锁或性能问题，如果其代码设计为避免只要有可能受到阻止。 具体而言，应尽可能驱动程序的执行线程运行到完成，无需停止等待另一个线程或资源时的风险。 例如，驱动程序线程可以使用 Interlocked*Xxx*函数 (有关示例，请参阅[ **InterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedincrement)) 来协调对某些共享其访问没有被阻止的风险的资源。

尽管这些是功能强大的技术，您可能不能安全地从执行路径中移除所有自旋锁、 互斥体和其他阻塞的同步基元。 使用 Interlocked*Xxx*明智地，函数与无限期等待可能会导致数据资源不足的知识。

最重要的是，不要创建自定义同步基元。 内置的 Windows 基元 （互斥锁、 自旋锁等） 有可能在将来，支持新的计划程序功能所需修改和使用自定义构造的驱动程序完全可以保证不能够在未来处理。

### <a name="span-idipincountinterfacespanspan-idipincountinterfacespanspan-idipincountinterfacespanipincount-interface"></a><span id="IPinCount_Interface"></span><span id="ipincount_interface"></span><span id="IPINCOUNT_INTERFACE"></span>IPinCount Interface

在 Windows XP 及更高版本， [IPinCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-ipincount)接口提供一种方法的更准确地说由分配 pin 的硬件资源的帐户的微型端口驱动程序。 通过调用微型端口驱动程序[ **IPinCount::PinCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-ipincount-pincount)方法中，端口驱动程序执行以下操作：

-   显示筛选器的最新的 pin 计数 （如将端口驱动程序维护） 到微型端口驱动程序。

-   提供微型端口驱动程序修改 pin 的机会计数到动态反映当前的硬件资源可用性。

对于某些音频设备，具有不同的属性 （三维、 立体声/mono 等） 的批流可能还必须在它们占用了多少硬件资源方面不同"权重"。 当打开或关闭"轻型"流、 驱动程序递增或递减通过其中一个可用的 pin 的计数。 在打开的"重量级"流，但是，微型端口驱动程序可能需要由两个而不是由一个递减可用 pin 计数，以便更准确地指示可以使用剩余的资源创建的 pin 数。

重量级流关闭时，其过程正好相反。 可用 pin 计数可能会增加的多个以反映这一事实的两个或更轻量的流可以创建从新释放资源。

 

 




