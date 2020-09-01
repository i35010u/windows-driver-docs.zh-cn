---
title: WavePci 微型端口驱动程序的性能问题
description: WavePci 微型端口驱动程序的性能问题
ms.assetid: 785fd743-0c78-44cd-95bf-1f961aa414b5
keywords:
- WavePci 性能问题 WDK 音频
- 流式处理服务机制 WDK 音频
- 硬件中断 WDK 音频
- 中断服务例程 WDK 音频
- Isr WDK 音频
- 计时器 Dpc WDK 音频
- 暂停/获取优化 WDK 音频
- IPreFetchOffset
- 同步基元 WDK 音频
- IPinCount
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d40e8d9ab37ad8e9f55acb9e94ee7f1697c09df5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210493"
---
# <a name="performance-issues-for-a-wavepci-miniport-driver"></a>WavePci 微型端口驱动程序的性能问题


## <span id="performance_issues_for_a_wavepci_miniport_driver"></span><span id="PERFORMANCE_ISSUES_FOR_A_WAVEPCI_MINIPORT_DRIVER"></span>


对于音频驱动程序对系统性能的影响，可遵循以下常规原则大大降低：

-   最小化在正常操作过程中运行的代码。

-   仅在必要时运行代码。

-   请考虑系统资源总消耗 (不只是 CPU 加载) 。

-   优化代码的速度和大小。

此外，WavePci 微型端口驱动程序必须解决特定于音频设备的几个性能问题。 以下讨论主要涉及音频呈现问题，不过，某些建议的技术也适用于音频捕获。

### <a name="span-idstream_servicing_mechanismsspanspan-idstream_servicing_mechanismsspanspan-idstream_servicing_mechanismsspanstream-servicing-mechanisms"></a><span id="Stream_Servicing_Mechanisms"></span><span id="stream_servicing_mechanisms"></span><span id="STREAM_SERVICING_MECHANISMS"></span>流服务机制

在讨论性能优化之前，必须先了解一些背景知识，才能了解用于处理流的 WavePci 机制。

处理波形渲染或捕获流时，音频设备需要通过微型端口驱动程序定期进行维护。 当新的映射可用于流时，驱动程序会将这些映射添加到流的 DMA 队列。 驱动程序还将从队列中删除已处理的任何映射。 有关映射的信息，请参阅 [WavePci 滞后时间](wavepci-latency.md)。

若要执行该服务，微型端口驱动程序将 * (DPC) * 或中断服务例程 (ISR) 提供延迟的过程调用，具体取决于该间隔是由系统计时器还是由 DMA 驱动的中断设置的。 在后一种情况下，DMA 硬件通常会在每次完成传输一定量的流数据时触发中断。

每次执行 DPC 或 ISR 时，它将确定哪些流需要维护。 DPC 或 ISR 通过调用 [**IPortWavePci：： Notify**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify) 方法来服务流。 此方法将流的服务组用作 [IServiceGroup](/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)类型的对象作为调用参数。 **通知**方法调用服务组的[**RequestService**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice)方法 (参阅**IServiceSink：： RequestService**) 。

服务组对象包含一组服务接收器，服务接收器是 [IServiceSink](/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)类型的对象。 [IServiceGroup](/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup) 派生自 IServiceSink，这两个接口都具有 [**RequestService**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice) 方法。 当 [**通知**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify) 方法调用服务组的 **RequestService** 方法时，服务组会通过对该组中的每个服务接收器调用 **RequestService** 方法来做出响应。

流的服务组包含至少一个服务接收器，端口驱动程序会在创建该流后立即将其添加到服务组。 端口驱动程序调用微型端口驱动程序的 [**IMiniportWavePci：： newstream.ischecked**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream) 方法来获取指向服务组的指针。 服务接收器的 [**RequestService**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice) 方法是端口驱动程序特定的流服务例程。 此例程执行以下操作：

-   调用微型端口驱动程序的 [**IMiniportWavePciStream：：服务**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service) 方法。

-   触发自上一次执行服务例程后流上任何新近挂起的位置或时钟事件。

如 [KS 事件](../stream/ks-events.md)中所述，当流到达特定位置或当时钟到达特定时间戳时，客户端可以注册以获得通知。 [**Newstream.ischecked**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)方法具有未提供服务组的选项，在这种情况下，端口驱动程序将设置自己的计时器，以标记对其服务例程的调用之间的时间间隔。

与 [**newstream.ischecked**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream) 方法一样，微型端口驱动程序的 [**IMiniportWavePci：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init) 方法还输出指向服务组的指针。 在 **Init** 调用之后，端口驱动程序会将其服务接收器添加到服务组。 此特定服务接收器包含整个筛选器的服务例程。  (上一段落介绍与筛选器上的某个 pin 关联的流的服务接收器。 ) 此服务例程调用微型端口驱动程序的 [**IMiniportWavePci：： service**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-service) 方法。 每当 DPC 或 ISR 调用向筛选器的服务组 [**发出通知**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify) 时，就会执行服务例程。 **Init**方法可以选择不提供服务组，在这种情况下，端口驱动程序永远不会调用其筛选器服务例程。

### <a name="span-idhardware_interruptsspanspan-idhardware_interruptsspanspan-idhardware_interruptsspanhardware-interrupts"></a><span id="Hardware_Interrupts"></span><span id="hardware_interrupts"></span><span id="HARDWARE_INTERRUPTS"></span>硬件中断

某些微型端口驱动程序生成的硬件间隔太多或不足。 在具有 DirectSound 硬件加速的某些 WavePci 呈现设备中，仅当映射的提供几乎用尽并且呈现引擎面临不足的风险时，才会发生硬件中断。 在其他硬件加速的 WavePci 设备中，每次完成单个映射或其他较小的时间间隔时，都会发生硬件中断。 在这种情况下，ISR 经常会发现它有很少的操作，但每个中断仍会通过寄存器交换和缓存重装使用系统资源。 提高驱动程序性能的第一步是尽可能减少中断数量，而不会给出太多的风险。 消除不必要的中断后，可以通过设计 ISR 来更有效地执行，从而提高性能。

在某些驱动程序中，Isr 会在每次发生硬件中断时调用流的 [**通知**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify) 方法，而不考虑流是否确实正在运行。 如果流不处于运行状态，则 DMA 处于非活动状态，尝试获取映射、释放映射或检查任何流中的新事件所需的任何时间都将浪费。 在有效的驱动程序中，ISR 验证在调用流的 **通知** 方法之前是否正在运行流。

但是，具有这种类型的 ISR 的驱动程序需要确保在流退出运行状态时触发流上的任何挂起事件。 否则，事件可能会延迟或丢失。 仅在 Microsoft Windows XP 之前的操作系统中运行到暂停的转换期间才会出现此问题。 在 Windows XP 和更高版本中，当流将状态从 "已暂停" 更改为 "暂停" 时，端口驱动程序会立即自动向任何未完成的位置 但是，在较早的操作系统中，微型端口驱动程序负责通过最终调用在流暂停后立即 [**发出通知**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify) 来触发任何未完成的事件。 有关详细信息，请参阅下面的暂停/获取优化。

典型的 WavePci 微型端口驱动程序从 [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)管理单个播放流。 KMixer 的当前实现最少使用三个映射 Irp 来缓冲播放流。 每个 IRP 都包含足够的缓冲区存储约10毫秒的音频。 如果微型端口驱动程序在每次 DMA 控制器完成后使用 IRP 中的最后一个映射来触发硬件中断，则中断应以相当于10毫秒的间隔发生，这是一项非常频繁的间隔，足以使 DMA 队列保持从而使。 

### <a name="span-idtimer_dpcsspanspan-idtimer_dpcsspanspan-idtimer_dpcsspantimer-dpcs"></a><span id="Timer_DPCs"></span><span id="timer_dpcs"></span><span id="TIMER_DPCS"></span>计时器 Dpc

如果驱动程序管理任何硬件加速的 DirectSound 流，则应使用计时器 DPC (查看 [计时器对象和 dpc](../kernel/timer-objects-and-dpcs.md)) 而不是 DMA 驱动的硬件中断。 与此等效，PCI 卡上带有板载计时器的 WavePci 设备可以使用计时器驱动的硬件中断，而不是 DPC。

对于 DirectSound 缓冲区，整个缓冲区可以附加到单个 IRP。 如果缓冲区很大，并且微型端口驱动程序仅在到达缓冲区末尾时才计划硬件中断，则连续发生的中断可能会与 DMA 队列出现的距离相差很远。 此外，如果驱动程序正在管理大量硬件加速的 DirectSound 流，并且每个流都生成其自己的中断，则所有中断的累积影响都会降低系统性能。 在这些情况下，微型端口驱动程序应避免使用硬件中断来计划各个流的维护。 相反，它应为单个 DPC 中计划在定期生成的时间间隔内运行的所有流进行服务。

通过将计时器间隔设置为10毫秒，两次播放 DPC 执行之间的时间间隔类似于在单个 KMixer 播放流的情况下硬件中断所述的间隔。 因此，DPC 还可以处理 KMixer 播放流以及硬件加速 DirectSound 流。

当最后一个流退出运行状态时，微型端口驱动程序应禁用计时器 DPC 以避免浪费系统 CPU 周期。 禁用 DPC 后，驱动程序应确保刷新之前正在运行的流上挂起的任何时钟或位置事件。 在 Windows 98/Me 和 Windows 2000 中，驱动程序应调用 [**Notify**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify) 来触发正在暂停的流上的任何挂起事件。 在 Windows XP 和更高版本中，当流退出运行状态时，操作系统将自动触发任何挂起事件，无需通过微型端口驱动程序介入。

### <a name="span-idpause_acquire_optimizationsspanspan-idpause_acquire_optimizationsspanspan-idpause_acquire_optimizationsspanpauseacquire-optimizations"></a><span id="PAUSE_ACQUIRE_Optimizations"></span><span id="pause_acquire_optimizations"></span><span id="PAUSE_ACQUIRE_OPTIMIZATIONS"></span>暂停/获取优化

在 Windows 98/Me 和 Windows 2000 中，无论流是否处于运行状态，WavePci 端口驱动程序的流服务例程 ([**RequestService**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice) 方法) 始终会生成对微型端口驱动程序的 [**IMiniportWavePciStream：： service**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service) 方法的调用。 在这些操作系统中， **服务** 方法应检查流是否正在运行，然后花时间执行实际工作。  (但是，如果已将微型端口驱动程序的 DPC 或 ISR 优化为仅为正在运行的流调用 [**通知**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify) ，则将此检查添加到 **服务** 方法可能是冗余的。 ) 

在 Windows XP 和更高版本中，此优化是不必要的，因为 [**Notify**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify) 方法仅对运行的流调用 [**服务**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service) 方法。

### <a name="span-idusing_the_iprefetchoffset_interfacespanspan-idusing_the_iprefetchoffset_interfacespanspan-idusing_the_iprefetchoffset_interfacespanusing-the-iprefetchoffset-interface"></a><span id="Using_the_IPreFetchOffset_Interface"></span><span id="using_the_iprefetchoffset_interface"></span><span id="USING_THE_IPREFETCHOFFSET_INTERFACE"></span>使用 IPreFetchOffset 接口

DirectSound 用户熟悉播放光标和写入光标的两个概念。 播放光标指示从设备发出的数据在流中的位置 (驱动程序对当前 DAC) 的示例的最佳估算。 写入位置是客户端用于写入其他数据的下一个安全位置流中的位置。 对于 WavePci，默认假设是写入游标位于最后请求的映射的末尾。 如果微型端口驱动程序已获取大量未完成的映射，则播放光标与写入光标之间的偏移量可能会非常大，足以使某些 WHQL 音频位置测试失败。 在 Windows XP 和更高版本中， [IPreFetchOffset](/windows-hardware/drivers/ddi/portcls/nn-portcls-iprefetchoffset) 接口解决了这些问题。

微型端口驱动程序使用 [IPreFetchOffset](/windows-hardware/drivers/ddi/portcls/nn-portcls-iprefetchoffset) 来指定总线主机硬件的预提取特征，这主要取决于硬件 FIFO 大小。 音频子系统使用此数据设置播放光标与写入光标之间的恒定偏移量。 此常量偏移量明显小于默认偏移量，它利用了这样一种情况：即使在将映射传递到硬件后，可以将数据写入映射，只要播放光标离写入数据的位置远得多。  (此语句假定该驱动程序不复制或以其他方式处理映射中的数据。 ) 典型的偏移可能按64示例的顺序进行，具体取决于引擎设计。 对于这小的偏移量，WavePci 驱动程序在请求大量映射时可以完全响应并正常运行。

请注意，DirectSound 当前将硬件加速 pin 的写入游标填充10毫秒。

有关详细信息，请参阅 [预提取偏移量](prefetch-offsets.md)。

### <a name="span-idprocessing_data_in_mappingsspanspan-idprocessing_data_in_mappingsspanspan-idprocessing_data_in_mappingsspanprocessing-data-in-mappings"></a><span id="Processing_Data_in_Mappings"></span><span id="processing_data_in_mappings"></span><span id="PROCESSING_DATA_IN_MAPPINGS"></span>在映射中处理数据

如果可能，请避免硬件驱动程序接触到映射中的数据。 映射中包含的数据的任何软件处理都应拆分为独立于硬件驱动程序的软件筛选器。 硬件驱动程序执行此类处理会降低其效率并导致延迟问题。

硬件驱动程序应尽量使其真实的硬件功能变得透明。 驱动程序绝不应声明为在软件中实际执行的数据转换提供硬件支持。

### <a name="span-idsynchronization_primitivesspanspan-idsynchronization_primitivesspanspan-idsynchronization_primitivesspansynchronization-primitives"></a><span id="Synchronization_Primitives"></span><span id="synchronization_primitives"></span><span id="SYNCHRONIZATION_PRIMITIVES"></span>同步基元

现在，如果驱动程序的代码被设计为尽可能避免被阻止，则该驱动程序不太可能会出现死锁或性能问题。 具体而言，驱动程序的执行线程应在等待其他线程或资源的同时，尝试运行到完成，而不会有停止的风险。 例如，驱动程序线程可以使用联锁*Xxx* 函数 (例如，请参阅 [**InterlockedIncrement**](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)) ，协调它们对某些共享资源的访问，而不会受到阻止。

尽管这些是功能强大的技术，但您可能无法安全地从执行路径中删除所有旋转锁、互斥体和其他阻止同步基元。 慎用互锁*Xxx* 功能，了解无限期等待可能导致数据不足的情况。

毕竟，不要创建自定义同步基元。 内置的 Windows 基元 (互斥体、旋转锁等) 可能会根据需要进行修改，以支持将来的新计划程序功能，而使用自定义构造的驱动程序在将来确实不能正常工作。

### <a name="span-idipincount_interfacespanspan-idipincount_interfacespanspan-idipincount_interfacespanipincount-interface"></a><span id="IPinCount_Interface"></span><span id="ipincount_interface"></span><span id="IPINCOUNT_INTERFACE"></span>IPinCount 接口

在 Windows XP 和更高版本中， [IPinCount](/windows-hardware/drivers/ddi/portcls/nn-portcls-ipincount) 接口为微型端口驱动程序提供了一种方法，以便更准确地考虑分配 pin 所使用的硬件资源。 通过调用微型端口驱动程序的 [**IPinCount：:P incount**](/windows-hardware/drivers/ddi/portcls/nf-portcls-ipincount-pincount) 方法，端口驱动程序会执行以下操作：

-   公开由端口驱动程序 (维护的筛选器的当前 pin 计数) 到微型端口驱动程序。

-   为微型端口驱动程序提供修订 pin 计数以动态反映硬件资源当前可用性的机会。

对于某些音频设备，具有不同属性 (3-d、立体声/mono 等) 的波形流在其消耗的硬件资源数量方面可能还具有不同的 "权重"。 打开或关闭 "轻型" 流时，驱动程序会递增或递减可用 pin 的计数。 但打开 "重型" 流时，微型端口驱动程序可能需要将可用的 pin 计数减少两个（而不是一个），以便更准确地指示可以使用剩余资源创建的 pin 数。

关闭重型流时，将反向处理。 可用的 pin 计数可能会增加多个，以反映可以从新释放的资源创建两个或多个轻型流这一事实。

 

