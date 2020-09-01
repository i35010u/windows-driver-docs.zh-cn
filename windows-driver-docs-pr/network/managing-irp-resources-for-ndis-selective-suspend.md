---
title: 管理 NDIS 选择性挂起的 IRP 资源
description: 管理 NDIS 选择性挂起的 IRP 资源
ms.assetid: 542A96A7-AD6D-4780-8FEF-34730A663C1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45647fead0cceef80c16a058c4315deab3988119
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206741"
---
# <a name="managing-irp-resources-for-ndis-selective-suspend"></a>管理 NDIS 选择性挂起的 IRP 资源


如果微型端口驱动程序支持并启用 NDIS 选择性挂起，NDIS 将调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) ，以便在网络适配器变为非活动状态时向驱动程序发出空闲通知。 当微型端口驱动程序处理此通知时，可能需要发出 i/o 请求数据包 (Irp) 到基础总线驱动程序。 这些 Irp 通知总线驱动程序适配器的空闲状态，并请求确认适配器可以转换为低功耗状态。

由微型端口驱动程序颁发的 Irp 是特定于总线的。 例如，当 NDIS 调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)时，usb 微型端口发出 usb 空闲请求 ([**IOCTL \_ 内部 \_ USB \_ 提交 \_ 空闲 \_ 通知**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) IRP 到基础 USB 总线驱动程序。

初始化驱动程序之后，NDIS 可能多次向微型端口驱动程序发出空闲通知。 因此，建议驱动程序在调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数的上下文中为 USB IDLE 请求 IRP 分配资源。

以下示例演示了微型端口驱动程序如何分配 IRP 资源。

```C++
//
// MiniportInitializeEx()
//
// In the miniport's initialization routine, the miniport should allocate
// an IRP.  It can also set up the USB_IDLE_CALLBACK_INFO structure that
// will be used with each successive USB idle request.
//
NDIS_STATUS MiniportInitializeEx(
    _In_ NDIS_HANDLE MiniportAdapterHandle,
    _In_ NDIS_HANDLE MiniportDriverContext,
    _In_ PNDIS_MINIPORT_INIT_PARAMETERS MiniportInitParameters
    )
    {
    PIRP UsbSsIrp;
    USB_IDLE_CALLBACK_INFO UsbSsCallback;
    ...

    UsbSsIrp = IoAllocateIrp(Adapter->Fdo->StackSize, FALSE);
    if (!UsbSsIrp)
       {
       // Handle failure
       return NDIS_STATUS_RESOURCES;
       }

    UsbSsCallback.IdleCallback = MiniportUsbIdleRequestCallback;
    UsbSsCallback.IdleContext = Adapter;

    // Save these in the adapter structure for later use
    Adapter->UsbSsIrp = UsbSsIrp;
    Adapter->UsbSsCallback = UsbSsCallback;
    ...
    }
```

如果微型端口驱动程序在对 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用期间分配 IRP 资源，则驱动程序必须在对 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)的调用过程中释放这些资源。

以下示例演示了微型端口驱动程序如何释放 IRP 资源。

```C++
//
// MiniportHaltEx
//
// During halt (or when the miniport performs its cleanup from 
// MiniportInitializeEx) the miniport should free the IRP allocated 
// earlier.
//
VOID MiniportHaltEx(
     _In_  NDIS_HANDLE MiniportAdapterContext,
     _In_  NDIS_HALT_ACTION HaltAction
    )
    {
    ...
    if (Adapter->UsbSsIrp)
        {
        IoFreeIrp(Adapter->UsbSsIrp);
        Adapter->UsbSsIrp = NULL;
        }
    ...
    }

```