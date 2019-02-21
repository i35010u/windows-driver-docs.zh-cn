---
title: 查找和映射硬件资源
description: 本主题介绍如何将内核模式驱动程序框架 (KMDF) 驱动程序或用户模式驱动程序框架 (UMDF) 驱动程序从版本 2 映射中其 EvtDevicePrepareHardware 回调接收的已翻译的内存资源 (CmResourceTypeMemory)函数。
ms.assetid: 9D65D70C-FFF1-4663-8701-221C5443C425
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fb22e5d332435ae6159fdfb3d6cca96fb2d97eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525990"
---
# <a name="finding-and-mapping-hardware-resources"></a>查找和映射硬件资源


本主题介绍内核模式驱动程序框架 (KMDF) 驱动程序或用户模式驱动程序框架 (UMDF) 驱动程序从版本 2 将已翻译的内存资源的映射 (**CmResourceTypeMemory**)，它接收其[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数。

UMDF 1.x 驱动程序还可以接收此类中的资源及其[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)方法。 有关详细信息，请参阅[查找和 UMDF 1.x 驱动程序中映射硬件资源](finding-and-mapping-hardware-resources-in-umdf-1-x-drivers.md)。

您的驱动程序收到[原始和已翻译](raw-and-translated-resources.md)版本的设备的资源列表中的硬件资源及其[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数。 该驱动程序可以保存资源的列表，该框架将调用的驱动程序才有效[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)回调函数。

通常情况下，驱动程序调用[ **WdfCmResourceListGetCount** ](https://msdn.microsoft.com/library/windows/hardware/ff545687)从其[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)到回调函数确定资源在翻译后的资源的列表，并随后将调用的说明符的数目[ **WdfCmResourceListGetDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff545688)在一个循环，以便识别内存映射寄存器，I/O 端口和中断。

如果驱动程序分配的已翻译的内存资源 (**CmResourceTypeMemory**)，它必须将物理地址映射到它能够访问设备寄存器的地址。

KMDF 驱动程序调用[ **MmMapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff554618)将给定的物理地址范围映射到非分页的系统空间。 然后，它使用[ **HAL 库例程**](https://msdn.microsoft.com/library/windows/hardware/ff546644)读取和写入到寄存器。

UMDF 驱动程序调用[ **WdfDeviceMapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/dn265605)物理地址映射到它可以结合使用伪基址[WDF 注册/端口访问函数](https://msdn.microsoft.com/library/windows/hardware/dn265662)若要读取和写入到寄存器和端口。

该驱动程序取消资源映射通过调用[ **MmUnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff556387)或[ **WdfDeviceUnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/dn265610)从其[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)回调函数。

不需要映射 I/O 空间中的资源 (**CmResourceTypePort**， **CmResourceTypeInterrupt**， **CmResourceTypeDma**)。

如果 UMDF 驱动程序调用[ **WdfDeviceMapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/dn265605)，则必须设置**UmdfDirectHardwareAccess** INF 指令**AllowDirectHardwareAccess**.

有关演示如何将驱动程序查找和内存映射的映射注册资源的示例，请参阅[读取和写入设备注册](reading-and-writing-to-device-registers.md)。

 

 





