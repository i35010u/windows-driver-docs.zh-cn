---
title: 支持适用于 DMA 设备的电源管理
description: 支持适用于 DMA 设备的电源管理
keywords:
- DMA 操作 WDK KMDF，电源管理
- 总线主控 DMA WDK KMDF，电源管理
- 电源管理 WDK KMDF，DMA 设备
- DMA 启用程序对象 WDK KMDF
- 启用程序对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 979ba9b463ebff52ea4fdfcad2b749fd2f212581
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834837"
---
# <a name="supporting-power-management-for-dma-devices"></a>支持适用于 DMA 设备的电源管理


\[仅适用于 KMDF\]

DMA 启用码对象定义一组可选的事件回调函数，DMA 设备的驱动程序可以使用这些函数来管理进出设备工作 (D0) 状态的转换。

当 DMA 设备每次进入其工作状态，并且在框架调用了驱动程序的 [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调函数后，框架将按照它们列出的顺序调用以下 DMA 回调函数：

<a href="" id="---------evtdmaenablerfill--------"></a>[*EvtDmaEnablerFill*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)  
分配设备的 DMA 缓冲区。

<a href="" id="---------evtdmaenablerenable--------"></a>[*EvtDmaEnablerEnable*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)  
设备进入工作 (D0) 状态后，启用设备 DMA 功能。

<a href="" id="---------evtdmaenablerselfmanagediostart--------"></a>[*EvtDmaEnablerSelfManagedIoStart*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)  
启动 DMA 设备的自行管理 i/o 操作。

当 DMA 设备每次离开其工作状态，并且在框架调用驱动程序的 [*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) 回调函数之前，框架将按照它们列出的顺序调用以下 DMA 回调函数：

<a href="" id="---------evtdmaenablerselfmanagediostop--------"></a>[*EvtDmaEnablerSelfManagedIoStop*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)  
停止 DMA 设备的自行管理 i/o 操作。

<a href="" id="---------evtdmaenablerdisable--------"></a>[*EvtDmaEnablerDisable*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)  
在设备处于工作状态 (D0) 状态之前禁用设备 DMA 功能。

<a href="" id="---------evtdmaenablerflush--------"></a>[*EvtDmaEnablerFlush*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)  
释放设备的 DMA 缓冲区。

有关框架调用驱动程序的事件回调函数的顺序的详细信息，请参阅 [PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

 

