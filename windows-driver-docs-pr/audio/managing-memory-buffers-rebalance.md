---
title: 在音频资源重新平衡和意外删除操作期间管理内存缓冲区
description: 对于需要重新分配内存资源的某些 PCI 方案，将使用 PnP 重新平衡。 需要正确管理内存缓冲区以避免出现问题。
ms.date: 12/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2b1e068308e4fe7794ea608fd236b78adb3f7d29
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211421"
---
# <a name="managing-memory-buffers-during-audio-resource-rebalance-and-surprise-removal-operations"></a>在音频资源重新平衡和意外删除操作期间管理内存缓冲区

## <a name="pnp-rebalance-overview"></a>PnP 重新平衡概述

对于需要重新分配内存资源的某些 PCI 方案，将使用 PnP 重新平衡。 Windows 10 版本1511及更高版本的 Windows 中提供了 PnP 重新平衡。 有关重新平衡的一般信息，请参阅 [实现 PortCls 音频驱动程序的 PnP 再平衡](implement-pnp-rebalance-for-portcls-audio-drivers.md)。

## <a name="pnp-surprise-removal-overview"></a>PnP 意外删除概述

PnP "意外删除" (SR) 在设备意外从计算机中删除并且不再可用于 i/o 操作时发生。 有关其他信息，请参阅 [PnP 设备的状态转换](../kernel/state-transitions-for-pnp-devices.md) 和 [处理 IRP_MN_SURPRISE_REMOVAL 请求](../kernel/handling-an-irp-mn-surprise-removal-request.md)。

## <a name="managing-memory-buffers-during-audio-resource-rebalance-and-surprise-removal-operations"></a>在音频资源重新平衡和意外删除操作期间管理内存缓冲区

本部分介绍如何管理内存缓冲区，以及如何在音频资源重新平衡和 PnP SR 操作中对 HD 音频编解码器驱动程序执行内存缓冲区清理操作。

请注意，本主题中所述的对缓冲区管理方法的操作系统支持将在2019更新后的下一主要功能版本中提供。

如果无法正确地分配和释放支持的内存缓冲区，则可能导致内存损坏、软挂起和故障，如 [Bug 检查0x9F： DRIVER_POWER_STATE_FAILURE](../debugger/bug-check-0x9f--driver-power-state-failure.md)。


**关闭流句柄行为**

当 portcls 收到关闭流句柄时，portcls 将调用以下函数以将流状态设置为 "停止"，并释放缓冲区：

如果流尚未处于 "停止" 状态，则*设置流状态* (。 ) 

[IMiniportWaveRTStream：： SetState](/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))

*版本缓冲区*  

[IMiniportWaveRTStream：： FreeAudioBuffer] ([IMiniportWaveRTStream：： SetState](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85)) 或 [IMiniportWaveRTStreamNotification：： FreeBufferWithNotification](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstreamnotification-freebufferwithnotification)

请注意，portcls 微型端口驱动程序应成功将状态转换从较高的值转换为较小的值， (RUN = = 3，PAUSE = = 2，获取 = = 1，STOP = = 0) 当驱动程序在 SR/STOP (操作期间已被驱动程序停止时（即，在接近关闭句柄请求之前，SR/STOP 会) 。

**缓冲区处理**

当在正常操作过程中关闭流时，portcls 会调用波形 RT 的回调，使驱动程序停止其 DMA 操作并释放其关联的缓冲区：

[IMiniportWaveRTStream：： SetState](/previous-versions/windows/hardware/drivers/ff536756(v=vs.85)) -> SETDMAENGINESTATE (HD 音频总线 DDI) 。 采取操作来启动/暂停 DMA。

[IMiniportWaveRTStream：： FreeAudioBuffer](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-freeaudiobuffer) 或 [IMiniportWaveRTStreamNotification：： FreeBufferWithNotification](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstreamnotification-freebufferwithnotification)-> FreeDmaBuffer (HD 音频总线 DDI) 。

IMiniportWaveRTStream [Notification] 的析构函数-> FreeDmaEngine (HD 音频总线 DDI) 。 

如果设备意外删除，微型端口必须释放其所有的 h/w 资源，而不会等待打开的流句柄关闭。 这意味着，在将 PnP 请求转发到带有 [PcDisptachIrp](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdispatchirp) DDI 的 PortCls 之前，微型端口必须停止、重置和释放所有已分配的 DMA 引擎。 另一方面，在关闭流句柄并 PortCls 用 FreeAudioBuffer/FreeBufferWithNotification 回调通知微型端口之前，微型端口不得释放音频波形 RT 缓冲区。

当设备因选择支持重新平衡而停止时，无需等待打开的流句柄关闭，微型端口就必须释放所有的硬件资源。 这意味着，小型端口必须停止、重置和释放由 portcls 调用的 PnP 回调中的所有已分配 DMA 引擎。 另一方面，在关闭流句柄并 PortCls 用 FreeAudioBuffer/FreeBufferWithNotification 回调通知微型端口之前，微型端口不得释放音频波形 RT 缓冲区。

请注意，正常的关闭流操作可以同时作为 SR/Stop 操作发生，这意味着小型端口必须在这些线程之间实现正确的同步。

操作示例假设 SR/STOP 和 Close 线程之间存在正确的序列化代码：


关闭：

```
STOP_DMA

FREE_BUFFER

FREE_DMA_ENGINE
```

在 SR/Stop 上：

```
STOP_DMA

FREE_DMA_ENGINE
```

这是伪代码中这些操作的定义。

```
STOP_DMA:
if (DmaEngineState != ResetState)
{
\\Set DMA Engine state to not running
SetDmaEngineState(context, StopState, 1, &dma);
SetDmaEngineState(context, ResetState, 1, &dma);
DmaEngineState = ResetState;
}
```


```
FREE_BUFFER:
\\Free DMA buffer
FreeDmaEBuffer(context, dma);
```


```
FREE_DMA_ENGINE:
if (DMAEngineAllocated==true)
{
\\Free DMA engine
FreeDmaEngine (context, dma);
DMAEngineAllocated=false
}
```

有关详细信息，请参阅：

[PSET_DMA_ENGINE_STATE 回调函数](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[HDAUDIO_STREAM_STATE 枚举](/windows-hardware/drivers/ddi/hdaudio/ne-hdaudio-_hdaudio_stream_state)

[PFREE_DMA_ENGINE 回调函数](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[PSET_DMA_ENGINE_STATE 回调函数](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[IMiniportWaveRTStreamNotification 接口](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstreamnotification)

[IMiniportWaveRTStreamNotification：： FreeBufferWithNotification 方法](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstreamnotification-freebufferwithnotification)

[PcDisptachIrp](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdispatchirp)