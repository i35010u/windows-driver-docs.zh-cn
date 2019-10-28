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
ms.openlocfilehash: 919fb3ebe55b60bab3677ab48601fbad458396e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843367"
---
# <a name="acquiring-usbcamd2-features"></a>获取 USBCAMD2 功能


必须先获取指向[**USBCAMD\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-usbcamd_interface)结构的指针，然后才能使用新的 USBCAMD2 功能。 若要获取指针，请生成并发送[**IRP\_MN\_QUERY\_INTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) request from 微型驱动程序的[**SRB\_\_初始化**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialization-complete) [*AdapterReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)回调中的完成处理程序才能. USBCAMD2 微型驱动程序库处理此 IRP，并向照相机微型驱动程序返回 USBCAMD\_接口类型的直接调用接口。 接口实质上是函数指针的表。

以下代码演示了如何从相机微型驱动程序生成和发送 IRP\_MN\_QUERY\_接口请求：

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

 

 




