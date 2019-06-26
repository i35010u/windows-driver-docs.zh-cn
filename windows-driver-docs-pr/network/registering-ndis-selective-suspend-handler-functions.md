---
title: 注册 NDIS 选择性挂起处理程序函数
description: 注册 NDIS 选择性挂起处理程序函数
ms.assetid: D4125F14-8356-4D9E-A287-D35D3BF69182
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5079cb05693596efa5c0e84e1fe9e28eedd41289
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374743"
---
# <a name="registering-ndis-selective-suspend-handler-functions"></a>注册 NDIS 选择性挂起处理程序函数


如果微型端口驱动程序支持 NDIS 选择性挂起，NDIS 会通知驱动程序的基础网络适配器已进入空闲状态。 微型端口驱动程序必须提供用于处理这些空闲通知的以下函数：

<a href="" id="miniportidlenotification"></a>[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)  
NDIS 调用[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)处理程序函数，以通知微型端口驱动程序的网络适配器已进入空闲状态。 微型端口驱动程序通过确定网络适配器是否可以转换到低功耗状态来处理空闲状态的通知。 微型端口驱动程序执行的特定于总线的方式确定。

例如，USB 微型端口驱动程序确定是否将网络适配器可以过渡到低功耗状态通过发出 USB 空闲状态请求的 I/O 请求数据包 (IRP) ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 为基础的 USB 总线驱动程序。 通过此 IRP 的处理，适配器处于空闲状态，并将转换为低功耗状态通知微型端口驱动程序。

<a href="" id="miniportcancelidlenotification"></a>[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)  
NDIS 调用[ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)要取消未完成的空闲通知处理程序函数。 当调用此函数时，微型端口驱动程序将取消任何特定于总线的 Irp，它可能以前颁发的空闲通知。

例如，当[ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)调用时，USB 微型端口必须取消以前颁发 USB 空闲请求 IRP。 当取消 IRP 时，微型端口驱动程序将通知适配器现在可以将转换为全功率状态。

当微型端口驱动程序[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)调用函数时，驱动程序寄存器其 NDIS 选择性挂起的处理程序函数通过执行以下步骤：

1.  微型端口驱动程序必须设置**SetOptionsHandler**的成员[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构的驱动程序的入口点[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 驱动程序调用[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)注册其**NDIS\_微型端口\_驱动程序\_特征**使用 NDIS 结构。

2.  NDIS 调用[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数的调用上下文中[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)。

    当[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)调用时，微型端口驱动程序初始化[ **NDIS\_微型端口\_SS\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_ss_characteristics)与处理程序函数的指针的结构。 然后调用微型端口驱动程序[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)并设置*OptionalHandlers*参数指向的指针**NDIS\_微型端口\_SS\_特征**结构。

详细了解如何处理空闲通知 ndis 选择性挂起，请参阅[NDIS 选择性挂起空闲通知](ndis-selective-suspend-idle-notifications.md)。

 

 





