---
title: 查找和映射硬件资源
description: 本主题介绍在版本2中启动的内核模式驱动程序框架（KMDF）驱动程序或用户模式驱动程序框架（UMDF）驱动程序如何映射其在其 EvtDevicePrepareHardware 回调中收到的已转换内存资源（CmResourceTypeMemory）才能.
ms.assetid: 9D65D70C-FFF1-4663-8701-221C5443C425
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b9ca351a9b13b5d201b2ca37b794afb6f1a453
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842855"
---
# <a name="finding-and-mapping-hardware-resources"></a>查找和映射硬件资源


本主题介绍在版本2中启动的内核模式驱动程序框架（KMDF）驱动程序或用户模式驱动程序框架（UMDF）驱动程序如何映射其在其[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数中收到的已转换内存资源（**CmResourceTypeMemory**）。

UMDF 1.x 驱动程序还可以在其[**IPnpCallbackHardware2：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)方法中接收此类型的资源。 有关详细信息，请参阅[在 UMDF 1.X 驱动程序中查找和映射硬件资源](finding-and-mapping-hardware-resources-in-umdf-1-x-drivers.md)。

你的驱动程序会在设备的资源列表中的[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数内接收[原始和翻译](raw-and-translated-resources.md)的硬件资源版本。 驱动程序可以保存资源列表，该列表在框架调用驱动程序的[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数之前有效。

通常，驱动程序从其[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数调用[**WdfCmResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetcount) ，以确定已转换资源列表中的资源说明符数量，然后调用[**WdfCmResourceListGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetdescriptor)用于标识内存映射的寄存器、i/o 端口和中断的循环。

如果为驱动程序分配了已转换的内存资源（**CmResourceTypeMemory**），则它必须将物理地址映射到一个地址，通过该地址可以访问设备寄存器。

KMDF 驱动程序调用[**MmMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)将给定的物理地址范围映射到未分页的系统空间。 然后，它使用[**HAL 库例程**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))来读取和写入注册。

UMDF 驱动程序调用[**WdfDeviceMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicemapiospace)将物理地址映射到一个伪基址，该地址可与[WDF 注册/端口访问函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfhwaccess/)结合使用，以读取和写入寄存器和端口。

驱动程序通过从其[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数调用[**MmUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)或[**WdfDeviceUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceunmapiospace) ，messagebox 取消资源。

无需映射 i/o 空间中的资源（**CmResourceTypePort**、 **CmResourceTypeInterrupt**、 **CmResourceTypeDma**）。

如果 UMDF 驱动程序调用[**WdfDeviceMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicemapiospace)，则必须将**UmdfDirectHardwareAccess** INF 指令设置为**AllowDirectHardwareAccess**。

有关演示驱动程序如何查找和映射内存映射寄存器资源的示例，请参阅[读取和写入设备寄存器](reading-and-writing-to-device-registers.md)。

 

 





