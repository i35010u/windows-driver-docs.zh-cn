---
title: 查找和映射硬件资源
description: 本主题介绍在版本2中启动的内核模式驱动程序框架 (KMDF) 驱动程序或用户模式驱动程序框架 (UMDF) 驱动程序如何在其 EvtDevicePrepareHardware 回调函数中映射已转换的内存资源 (CmResourceTypeMemory) 。
ms.assetid: 9D65D70C-FFF1-4663-8701-221C5443C425
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bc40b0fe55b74c9da29b903993c75e1f922b6ba
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187225"
---
# <a name="finding-and-mapping-hardware-resources"></a>查找和映射硬件资源


本主题介绍在版本2中启动的内核模式驱动程序框架 (KMDF) 驱动程序或用户模式驱动程序框架 (UMDF) 驱动程序如何在其[*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数中映射已转换的内存资源 (**CmResourceTypeMemory**) 。

UMDF 1.x 驱动程序还可以在其 [**IPnpCallbackHardware2：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware) 方法中接收此类型的资源。 有关详细信息，请参阅 [在 UMDF 1.X 驱动程序中查找和映射硬件资源](finding-and-mapping-hardware-resources-in-umdf-1-x-drivers.md)。

你的驱动程序会在设备的资源列表中的[*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数内接收[原始和翻译](raw-and-translated-resources.md)的硬件资源版本。 驱动程序可以保存资源列表，该列表在框架调用驱动程序的 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) 回调函数之前有效。

通常，驱动程序从其[*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数调用[**WdfCmResourceListGetCount**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetcount) ，以确定已转换资源列表中的资源说明符数量，然后在循环中调用[**WdfCmResourceListGetDescriptor**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetdescriptor)来识别内存映射的寄存器、i/o 端口和中断。

如果为驱动程序分配了一个 (**CmResourceTypeMemory**) 的已翻译内存资源，则必须将该物理地址映射到一个地址，通过该地址可以访问设备寄存器。

KMDF 驱动程序调用 [**MmMapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) 将给定的物理地址范围映射到未分页的系统空间。 然后，它使用 [**HAL 库例程**](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)) 来读取和写入注册。

UMDF 驱动程序调用 [**WdfDeviceMapIoSpace**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicemapiospace) 将物理地址映射到一个伪基址，该地址可与 [WDF 注册/端口访问函数](/windows-hardware/drivers/ddi/wdfhwaccess/) 结合使用，以读取和写入寄存器和端口。

驱动程序通过从其[*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数调用[**MmUnmapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)或[**WdfDeviceUnmapIoSpace**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceunmapiospace) ，messagebox 取消资源。

不需要将 i/o 空间中的资源映射 (**CmResourceTypePort**， **CmResourceTypeInterrupt**， **CmResourceTypeDma**) 。

如果 UMDF 驱动程序调用 [**WdfDeviceMapIoSpace**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicemapiospace)，则必须将 **UmdfDirectHardwareAccess** INF 指令设置为 **AllowDirectHardwareAccess**。

有关演示驱动程序如何查找和映射内存映射寄存器资源的示例，请参阅 [读取和写入设备寄存器](reading-and-writing-to-device-registers.md)。

 

