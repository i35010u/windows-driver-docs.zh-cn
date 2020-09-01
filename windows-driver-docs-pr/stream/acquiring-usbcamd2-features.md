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
ms.openlocfilehash: 1cb99bfb6be829a7c9cc78d2c74f099ca9f3fa89
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186863"
---
# <a name="acquiring-usbcamd2-features"></a>获取 USBCAMD2 功能


必须先获取指向 [**USBCAMD \_ 接口**](/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-usbcamd_interface) 结构的指针，然后才能使用新的 USBCAMD2 功能。 若要获取指针，请从相机微型驱动程序的[**SRB \_ 初始化 \_ **](./srb-initialization-complete.md)处理程序的[*AdapterReceivePacket*](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)回调函数中构建并发送[**IRP \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md)请求。 USBCAMD2 微型驱动程序库处理此 IRP，并向照相机微型驱动程序返回 USBCAMD 接口类型的直接调用接口 \_ 。 接口实质上是函数指针的表。

以下代码演示了如何从相机微型驱动程序生成并发送 IRP \_ MN \_ 查询 \_ 接口请求：

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

 

