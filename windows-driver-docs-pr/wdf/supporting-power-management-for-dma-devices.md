---
title: 支持适用于 DMA 设备的电源管理
description: 支持适用于 DMA 设备的电源管理
ms.assetid: abbb8f60-560f-41c9-85c5-1ec82078b99e
keywords:
- DMA 操作 WDK KMDF，电源管理
- 主总线 DMA WDK KMDF，电源管理
- 电源管理 WDK KMDF，DMA 的设备
- DMA 促成因素对象 WDK KMDF
- 启用程序对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3800f26cbbe5626bfd6bda2925ff40708fdccc20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368050"
---
# <a name="supporting-power-management-for-dma-devices"></a>支持适用于 DMA 设备的电源管理


\[仅适用于 KMDF\]

DMA 促成因素对象定义一组可选事件回叫函数，DMA 设备的驱动程序可用于管理转换入和移出设备的使用 (D0) 状态。

每次 DMA 设备进入其工作状态，且后框架已调用的驱动程序[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数，框架将调用以下 DMA 回调函数，在所列的顺序：

<a href="" id="---------evtdmaenablerfill--------"></a>[*EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)  
分配设备的 DMA 缓冲区。

<a href="" id="---------evtdmaenablerenable--------"></a>[*EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)  
在设备进入其工作 (D0) 状态后启用 DMA 的设备的功能。

<a href="" id="---------evtdmaenablerselfmanagediostart--------"></a>[*EvtDmaEnablerSelfManagedIoStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)  
启动 DMA 设备的自托管的 I/O 操作。

每次 DMA 设备离开它的工作状态，且 framework 之前已调用驱动程序的[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)回调函数，框架将调用以下 DMA 回调函数，在所列的顺序：

<a href="" id="---------evtdmaenablerselfmanagediostop--------"></a>[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)  
停止 DMA 设备的自托管的 I/O 操作。

<a href="" id="---------evtdmaenablerdisable--------"></a>[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)  
设备离开其工作 (D0) 状态之前，请禁用 DMA 的设备的功能。

<a href="" id="---------evtdmaenablerflush--------"></a>[*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)  
解除分配设备的 DMA 缓冲区。

有关在其中框架调用驱动程序的事件回调函数的顺序的详细信息，请参阅[PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

 

 





