---
title: 注册 NDIS 选择性挂起处理程序函数
description: 注册 NDIS 选择性挂起处理程序函数
ms.assetid: D4125F14-8356-4D9E-A287-D35D3BF69182
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e58c49930c2e7ab04e76979ac12005cf81619f2e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211981"
---
# <a name="registering-ndis-selective-suspend-handler-functions"></a>注册 NDIS 选择性挂起处理程序函数


如果微型端口驱动程序支持 NDIS 选择性挂起，NDIS 会通知驱动程序基础网络适配器已进入空闲状态。 微型端口驱动程序必须提供以下函数来处理这些空闲通知：

<a href="" id="miniportidlenotification"></a>[*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)  
NDIS 调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 处理程序函数，通知微型端口驱动程序网络适配器已进入空闲状态。 微型端口驱动程序通过确定网络适配器是否可以过渡到低功耗状态来处理空闲通知。 微型端口驱动程序以特定于总线的方式执行此确定。

例如，USB 微型端口驱动程序通过发出 USB 空闲请求的 i/o 请求数据包 (IRP) 来确定网络适配器是否可以转换为低功耗状态， ([**IOCTL \_ 内部) \_ USB \_ \_ \_ **](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification) 向底层 usb 总线驱动程序发送请求。 通过处理此 IRP，会通知微型端口驱动程序适配器处于空闲状态，并且可以转换为低功耗状态。

<a href="" id="miniportcancelidlenotification"></a>[*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)  
NDIS 调用 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 处理程序函数以取消未完成的空闲通知。 调用此函数时，微型端口驱动程序会取消之前为空闲通知发出的任何特定于总线的 Irp。

例如，当调用 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 时，USB 微型端口必须取消以前颁发的 usb 空闲请求 IRP。 取消 IRP 后，会通知微型端口驱动程序，此时适配器可以转换为完全电源状态。

调用微型端口驱动程序的 [**DriverEntry**](./initializing-a-miniport-driver.md) 函数时，驱动程序会按照以下步骤注册其 NDIS 选择性挂起处理程序函数：

1.  微型端口驱动程序必须将[**NDIS \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构的**SetOptionsHandler**成员设置为驱动程序的[*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数的入口点。 驱动程序调用 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) ，以通过 ndis 注册其 **ndis \_ 微型端口 \_ 驱动程序 \_ 特征** 结构。

2.  NDIS 在调用[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)的上下文中调用[*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数。

    调用 [*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options) 时，微型端口驱动程序使用指向处理程序函数的指针初始化 [**NDIS \_ 微型端口 \_ SS \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_ss_characteristics) 结构。 然后，微型端口驱动程序调用 [**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers) ，并将 *OptionalHandlers* 参数设置为指向 **NDIS \_ 微型端口 \_ SS \_ 特征** 结构的指针。

有关如何处理 NDIS 选择性挂起的空闲通知的详细信息，请参阅 [Ndis 选择性挂起空闲通知](ndis-selective-suspend-idle-notifications.md)。

 

