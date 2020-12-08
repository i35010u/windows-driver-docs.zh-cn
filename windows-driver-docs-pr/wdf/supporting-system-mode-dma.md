---
title: 支持系统模式 DMA
description: 介绍 KMDF 驱动程序在其事件回调函数中提供的用于处理系统模式 DMA 设备 i/o 请求的代码。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5ea810a451b7d1640e9e2c072214003b24f47b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836593"
---
# <a name="supporting-system-mode-dma"></a>支持系统模式 DMA


\[仅适用于 KMDF\]

与 *主线主机* dma 相比，系统模式 dma 介绍了多个设备共享单个（通常是多个多通道 DMA 控制器）的配置。

从 Kernel-Mode Driver Framework (KMDF) 1.11 版开始，该框架支持在 Windows 8 或更高版本的 Windows 操作系统的 Windows 8 或更高版本上运行的)  (芯片上的系统上的系统模式 DMA。

本主题介绍 KMDF 驱动程序在其事件回调函数中必须提供的代码，以及可注册的可选事件回调函数，以处理系统模式 DMA 设备的 i/o 请求。

有关 KMDF 和 bus-master DMA 的信息，请参阅 [处理 Bus-Master DMA 设备的 KMDF 驱动程序中的 I/o 请求](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)。

下图显示了驱动程序用于支持系统模式 DMA 的事件回调函数：

![kmdf 驱动程序中的系统模式 dma 实现](images/sys-mode-dma-in-kmdf.png)

## <a name="creating-a-system-mode-dma-enabler"></a>创建 System-Mode DMA 启用程序


创建系统模式 DMA 配置文件的过程分为两个步骤。 以下步骤表示典型方案：

1.  通常在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中，驱动程序 [**调用 \_ WDF \_ DMA 启用码 \_ \_ INIT**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdf_dma_enabler_config_init)，并将 **配置文件** 参数设置为 **SystemMode** 或 **SystemModeDuplex**。 然后，该驱动程序调用 [**WdfDmaEnablerCreate**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)，同时传递其刚收到的 [**WDF \_ DMA \_ 启用码 \_ 配置**](/windows-hardware/drivers/ddi/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config) 结构。

    驱动程序可以在 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)过程中创建启用程序。

2.  驱动程序的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数通过调用 [**WDFDMAENABLERCONFIGURESYSTEMPROFILE**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile) 方法将 DMA 启用码与其 dma 资源关联起来。 对于双工启用程序，驱动程序将调用 [**WdfDmaEnablerConfigureSystemProfile**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile) 两次，一次配置每个传输方向。

    在 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)完成之后，驱动程序可以调用 [**WdfDmaEnablerConfigureSystemProfile**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile) ，但驱动程序必须在初始化 DMA 事务之前调用此方法。

## <a name="providing-optional-callback-functions"></a>提供可选的回调函数


### <a name="configuring-a-dma-channel"></a><a href="" id="configuring-a-system-mode-dma-enabler"></a>配置 DMA 通道

通常，KMDF 驱动程序不会配置 DMA 通道。 但是，在某些情况下，驱动程序可能需要执行特定于通道的配置。 例如，驱动程序可以使用以下步骤调用由 DMA 控制器实现的自定义函数：

1.  在其中一个驱动程序的 [请求处理](request-handlers.md)程序中，驱动程序调用 [**WdfDmaTransactionSetChannelConfigurationCallback**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetchannelconfigurationcallback) 来注册 [*EvtDmaTransactionConfigureDmaChannel*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_configure_dma_channel) 回调函数。
2.  驱动程序的 [*EvtDmaTransactionConfigureDmaChannel*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_configure_dma_channel) 回调函数调用 [**WDFDMAENABLERWDMGETDMAADAPTER**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter) 来检索 WDM [**DMA \_ 适配器**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_adapter)的指针。 此结构是表示驱动程序的系统模式 DMA 通道的适配器对象。
3.  然后，该驱动程序可以调用 [**ConfigureAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pconfigure_adapter_channel) 来启用 DMA 控制器实现的自定义函数。 仅可通过 [**DMA \_ 操作**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations) 结构中返回的地址的指针调用此例程。
4.  如果已成功配置 DMA 通道，则驱动程序的 [*EvtDmaTransactionConfigureDmaChannel*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_configure_dma_channel) 回调函数将返回 TRUE。
5.  框架调用驱动程序的 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 回调函数。

### <a name="receiving-notification-of-transfer-completion"></a>接收传输完成通知

不同于使用总线控制控制器的设备，系统模式 DMA 设备的硬件可能无法通过发出中断来表明 DMA 传输已完成。

如果设备不引发中断来表明 DMA 传输结束，则驱动程序可以提供一个 [*EvtDmaTransactionDmaTransferComplete*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_dma_transfer_complete) 事件回调函数，该函数在系统模式 DMA 传输完成后，框架将调用该函数。

若要注册此回调函数，驱动程序从其一个 [请求处理程序](request-handlers.md)调用 [**WdfDmaTransactionSetTransferCompleteCallback**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsettransfercompletecallback) 。

 

