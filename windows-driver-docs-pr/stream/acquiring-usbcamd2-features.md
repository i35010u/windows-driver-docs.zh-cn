---
title: 获取 USBCAMD2 功能
description: 获取 USBCAMD2 功能
ms.assetid: 39db38a8-8279-4c61-9010-cc6d4767efc2
keywords:
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- USBCAMD2 功能 WDK Windows 2000 内核流式处理
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
- IRP_MN_QUERY_INTERFACE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f034a961b20c35ef596688395fd7973b44c9237
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357187"
---
# <a name="acquiring-usbcamd2-features"></a>获取 USBCAMD2 功能


您必须获取一个指向[ **USBCAMD\_界面**](https://msdn.microsoft.com/library/windows/hardware/ff568605)结构，然后才能使用新的 USBCAMD2 功能。 若要获取的指针，生成并发送[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)从照相机微型驱动程序的请求[ **SRB\_初始化\_完成**](https://msdn.microsoft.com/library/windows/hardware/ff568182)中的处理程序[ *AdapterReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff554080)回调函数。 处理此 IRP USBCAMD2 微型驱动程序库，并返回类型 USBCAMD 的直接调用接口\_照相机微型驱动程序的接口。 接口是实质上是一个表的函数指针。

下面的代码演示如何生成和发送 IRP\_MN\_查询\_接口请求从照相机微型驱动程序：

```cpp
KeInitializeEvent(&Event, NotificationEvent, FALSE);
Irp = IoBuildSynchronousFsdRequest(
    IRP_MJ_PNP,
    pDeviceObject,
    NULL,
    0,
    NULL,
    &Event,
    &IoStatusBlock);

if (NULL != Irp)
{
    Irp->RequestorMode = KernelMode;
    IrpStackNext = IoGetNextIrpStackLocation(Irp);
    //
    // Create an interface query out of the Irp.
    //
    IrpStackNext->MinorFunction = IRP_MN_QUERY_INTERFACE;
    IrpStackNext->Parameters.QueryInterface.InterfaceType = (GUID*)&GUID_USBCAMD_INTERFACE;
    IrpStackNext->Parameters.QueryInterface.Size = sizeof(*pUsbcamdInterface);
    IrpStackNext->Parameters.QueryInterface.Version = USBCAMD_VERSION_200;
    IrpStackNext->Parameters.QueryInterface.Interface = (PINTERFACE)pUsbcamdInterface;
    IrpStackNext->Parameters.QueryInterface.InterfaceSpecificData = NULL;
    Status = IoCallDriver(pDeviceObject, Irp);
    if (STATUS_PENDING == Status)
    {
        //
        // This  waits using KernelMode so that the stack, and therefore the
        // event on that stack, is not paged out.
        //
        KeWaitForSingleObject(&Event, Executive, KernelMode, FALSE, NULL);
        Status = IoStatusBlock.Status;
    }

}
else
{
    Status = STATUS_INSUFFICIENT_RESOURCES;
}
```

 

 




