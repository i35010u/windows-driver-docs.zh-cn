---
title: 实现 MiniportCancelIdleNotification 处理程序函数
description: 实现 MiniportCancelIdleNotification 处理程序函数
ms.assetid: 51C25573-5723-44F9-B498-EBEF6756F3B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7f94031ba27898a11dd9fcf2ba3fca0d3a65541
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521431"
---
# <a name="implementing-a-miniportcancelidlenotification-handler-function"></a>实现 MiniportCancelIdleNotification 处理程序函数


NDIS 调用微型端口驱动程序[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)为了取消空闲通知过程，并转换为全功率状态的网络适配器处理程序函数。 当调用此函数时，微型端口驱动程序必须执行以下步骤：

1.  微型端口驱动程序必须取消任何特定于总线的 Irp，它可能以前颁发的空闲通知。

2.  微型端口驱动程序调用[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)。 此调用通知 NDIS 空闲通知已完成。 NDIS 然后复杂选择性挂起操作通过转换为全功率状态的网络适配器。

例如，当[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)调用时，USB 微型端口驱动程序调用[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338)取消 I/O请求数据包 (IRP) USB 空闲请求 ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)). USB 微型端口驱动程序之前颁发此 IRP 中的其[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)处理程序函数。 一旦 USB 总线驱动程序已取消 IRP，它将调用 IRP 的完成例程。 当 USB 总线驱动程序调用完成例程时，它可以确认取消 IRP 和设备可以恢复到全功率状态。 在上下文中完成例程，微型端口驱动程序调用[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)。

**请注意**  USB 总线驱动程序可以调用完成例程的调用上下文中以同步方式[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338)或后，将异步[*MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)返回。

 

以下是一种[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088) USB 微型端口驱动程序的处理程序函数。 此示例演示与取消 USB 空闲请求 IRP 涉及的步骤。

```C++
//
// MiniportCancelIdleNotification()
//
// This routine is called if NDIS has to cancel an idle notification.
// All that is needed is to cancel the selective suspend IRP.
//
VOID MiniportCancelIdleNotification(
    _In_ NDIS_HANDLE MiniportAdapterContext
    )
{
    IoCancelIrp(Adapter->UsbSsIrp);
}
```

有关实现 USB 空闲请求 IRP 完成例程的指南，请参阅[实现 USB 空闲请求 IRP 完成例程](implementing-a-usb-idle-request-irp-completion-routine.md)。

 

 





