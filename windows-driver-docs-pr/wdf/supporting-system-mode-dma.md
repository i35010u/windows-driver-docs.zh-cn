---
title: 支持系统模式 DMA
description: 介绍 KMDF 驱动程序提供在其事件的代码，用于处理系统模式 DMA 设备的 I/O 请求的回调函数。
ms.assetid: CCC77C15-69CA-44CB-8DEB-29F3EAEA44F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d629648ae39ec68f5817d8f58fbda8ff75e685c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547229"
---
# <a name="supporting-system-mode-dma"></a>支持系统模式 DMA


\[仅适用于 KMDF\]

系统模式 DMA，到相反*总线 master* DMA，介绍了多个设备共享的单一、 通常多渠道 DMA 控制器的配置。

从开始在内核模式驱动程序框架 (KMDF) 版本 1.11，框架在芯片 (SoC) 上的系统上支持系统模式 DMA – 基于 Windows 8 或更高版本的 Windows 操作系统上运行的系统。

本主题介绍 KMDF 驱动程序必须提供其事件回调函数，以及它可以注册的可选事件回调函数中的代码来处理系统模式 DMA 设备的 I/O 请求。

有关 KMDF 和总线 master DMA 的信息，请参阅[总线 Master DMA 设备 KMDF 驱动程序中处理 I/O 请求](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)。

下图显示该事件回叫函数，您的驱动程序使用支持系统模式 DMA 到：

![系统模式 dma 实现 kmdf 驱动程序中](images/sys-mode-dma-in-kmdf.png)

## <a name="creating-a-system-mode-dma-enabler"></a>创建系统模式 DMA 启用程序


创建系统模式 DMA 配置文件是一个两步过程。 以下步骤表示典型方案：

1.  通常在其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数、 驱动程序调用[ **WDF\_DMA\_促成因素\_配置\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff551292)，并设置**配置文件**参数**SystemMode**或者**SystemModeDuplex**。 然后，该驱动程序调用[ **WdfDmaEnablerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff546983)，并传递[ **WDF\_DMA\_促成因素\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551290)结构刚接收到它。

    该驱动程序或者可能创建期间推动[ *EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)。

2.  您的驱动程序[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数将 DMA 促成因素与其 DMA 资源关联通过调用[ **WdfDmaEnablerConfigureSystemProfile** ](https://msdn.microsoft.com/library/windows/hardware/hh451108)方法。 对于双工的促成因素，驱动程序调用[ **WdfDmaEnablerConfigureSystemProfile** ](https://msdn.microsoft.com/library/windows/hardware/hh451108)两次，一次用来配置每个传输方向。

    该驱动程序可以调用[ **WdfDmaEnablerConfigureSystemProfile** ](https://msdn.microsoft.com/library/windows/hardware/hh451108)后[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)已完成，但初始化 DMA 事务之前，驱动程序必须调用此方法。

## <a name="providing-optional-callback-functions"></a>提供可选的回调函数


### <a href="" id="configuring-a-system-mode-dma-enabler"></a>配置 DMA 通道

通常情况下，KMDF 驱动程序未配置 DMA 通道。 但是，在某些情况下，驱动程序可能需要执行特定于通道的配置。 例如，驱动程序可能调用通过使用以下步骤实现由 DMA 控制器的自定义函数：

1.  中的驱动程序之一[请求处理程序](request-handlers.md)，驱动程序调用[ **WdfDmaTransactionSetChannelConfigurationCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh451184)注册[ *EvtDmaTransactionConfigureDmaChannel* ](https://msdn.microsoft.com/library/windows/hardware/hh406414)回调函数。
2.  您的驱动程序[ *EvtDmaTransactionConfigureDmaChannel* ](https://msdn.microsoft.com/library/windows/hardware/hh406414)回调函数调用[ **WdfDmaEnablerWdmGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff547020)到检索指向 WDM [ **DMA\_适配器**](https://msdn.microsoft.com/library/windows/hardware/ff544062)。 此结构是表示驱动程序的系统模式 DMA 通道的适配器对象。
3.  然后，该驱动程序可以调用[ **ConfigureAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/hh450939)启用 DMA 控制器实现的自定义函数。 此例程是仅调用从中返回的地址指针[ **DMA\_OPERATIONS** ](https://msdn.microsoft.com/library/windows/hardware/ff544071)结构。
4.  您的驱动程序[ *EvtDmaTransactionConfigureDmaChannel* ](https://msdn.microsoft.com/library/windows/hardware/hh406414)回调函数返回 TRUE，如果它已成功配置 DMA 通道。
5.  框架将调用的驱动程序[ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)回调函数。

### <a name="receiving-notification-of-transfer-completion"></a>接收通知的传输完成

与使用总线主控控制器的设备，不同系统模式 DMA 设备的硬件不可能通过发出中断指示 DMA 传输已完成。

如果你的设备不会引发中断以指示 DMA 传输已完成，可以提供您的驱动程序[ *EvtDmaTransactionDmaTransferComplete* ](https://msdn.microsoft.com/library/windows/hardware/hh406418)框架在调用时的事件的回调函数系统模式 DMA 传输已完成。

若要注册此回调函数，驱动程序调用[ **WdfDmaTransactionSetTransferCompleteCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh439261)从其中一个其[请求处理程序](request-handlers.md)。

 

 





