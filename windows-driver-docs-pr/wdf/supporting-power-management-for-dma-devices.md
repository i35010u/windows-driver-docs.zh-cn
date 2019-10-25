---
title: 支持适用于 DMA 设备的电源管理
description: 支持适用于 DMA 设备的电源管理
ms.assetid: abbb8f60-560f-41c9-85c5-1ec82078b99e
keywords:
- DMA 操作 WDK KMDF，电源管理
- 总线主控 DMA WDK KMDF，电源管理
- 电源管理 WDK KMDF，DMA 设备
- DMA 启用程序对象 WDK KMDF
- 启用程序对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00c4175035dcf51c015f0c88f50a467f2144ed8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831698"
---
# <a name="supporting-power-management-for-dma-devices"></a>支持适用于 DMA 设备的电源管理


\[仅适用于 KMDF\]

DMA 启用码对象定义一组可选的事件回调函数，DMA 设备的驱动程序可以使用这些函数来管理进出设备工作（D0）状态的转换。

当 DMA 设备每次进入其工作状态，并且在框架调用了驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数后，框架将按照它们列出的顺序调用以下 DMA 回调函数：

<a href="" id="---------evtdmaenablerfill--------"></a>[*EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)  
分配设备的 DMA 缓冲区。

<a href="" id="---------evtdmaenablerenable--------"></a>[*EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)  
设备进入工作（D0）状态后，启用设备 DMA 功能。

<a href="" id="---------evtdmaenablerselfmanagediostart--------"></a>[*EvtDmaEnablerSelfManagedIoStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)  
启动 DMA 设备的自行管理 i/o 操作。

当 DMA 设备每次离开其工作状态，并且在框架调用驱动程序的[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)回调函数之前，框架将按照它们列出的顺序调用以下 DMA 回调函数：

<a href="" id="---------evtdmaenablerselfmanagediostop--------"></a>[*EvtDmaEnablerSelfManagedIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)  
停止 DMA 设备的自行管理 i/o 操作。

<a href="" id="---------evtdmaenablerdisable--------"></a>[*EvtDmaEnablerDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)  
禁用设备的 DMA 功能，使设备保持正常运行（D0）状态。

<a href="" id="---------evtdmaenablerflush--------"></a>[*EvtDmaEnablerFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)  
释放设备的 DMA 缓冲区。

有关框架调用驱动程序的事件回调函数的顺序的详细信息，请参阅[PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

 

 





