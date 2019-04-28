---
title: 管理 NDIS 选择性挂起的 IRP 资源
description: 管理 NDIS 选择性挂起的 IRP 资源
ms.assetid: 542A96A7-AD6D-4780-8FEF-34730A663C1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f78cf1cc0efba4782c5590cec27aa7abcb3894
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343601"
---
# <a name="managing-irp-resources-for-ndis-selective-suspend"></a>管理 NDIS 选择性挂起的 IRP 资源


如果微型端口驱动程序支持并启用 NDIS 选择性挂起，NDIS 调用[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)向驱动程序发出的空闲通知，如果网络适配器变为非活动状态。 当微型端口驱动程序处理此通知时，它可能需要向基础总线驱动程序发出 I/O 请求数据包 (Irp)。 这些 Irp 通知有关适配器的空闲状态，适配器可以切换为低功耗状态的请求确认总线驱动程序。

总线特定于 Irp 颁发的微型端口驱动程序。 例如，当 NDIS 调用[ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)，USB 微型端口发出一个 USB 空闲请求 ([**IOCTL\_内部\_USB\_提交\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) IRP 到基础 USB 总线驱动程序。

NDIS 可能空闲通知向发出微型端口驱动程序多次初始化后，驱动程序。 因此，我们建议驱动程序分配的资源的 USB 驱动程序的调用的上下文中的空闲请求 IRP [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。

下面的示例演示微型端口驱动程序将 IRP 资源的分配。

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

如果微型端口驱动程序会将 IRP 资源分配到在调用期间[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)，该驱动程序必须在调用释放这些资源[ *MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)。

下面的示例演示如何微型端口驱动程序释放的 IRP 资源。

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
