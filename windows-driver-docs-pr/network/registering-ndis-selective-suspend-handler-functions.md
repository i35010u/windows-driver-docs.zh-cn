---
title: 注册 NDIS 选择性挂起处理程序函数
description: 注册 NDIS 选择性挂起处理程序函数
ms.assetid: D4125F14-8356-4D9E-A287-D35D3BF69182
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18a5ed25d93b7ed124fe9b3c31a0d404d27bb749
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842070"
---
# <a name="registering-ndis-selective-suspend-handler-functions"></a>注册 NDIS 选择性挂起处理程序函数


如果微型端口驱动程序支持 NDIS 选择性挂起，NDIS 会通知驱动程序基础网络适配器已进入空闲状态。 微型端口驱动程序必须提供以下函数来处理这些空闲通知：

<a href="" id="miniportidlenotification"></a>[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)  
NDIS 调用[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数，通知微型端口驱动程序网络适配器已进入空闲状态。 微型端口驱动程序通过确定网络适配器是否可以过渡到低功耗状态来处理空闲通知。 微型端口驱动程序以特定于总线的方式执行此确定。

例如，USB 微型端口驱动程序通过为 USB 空闲请求发出 i/o 请求数据包（IRP）来确定网络适配器是否可以过渡到低功耗状态（[**IOCTL\_内部\_usb\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)）到基础 USB 总线驱动程序。 通过处理此 IRP，会通知微型端口驱动程序适配器处于空闲状态，并且可以转换为低功耗状态。

<a href="" id="miniportcancelidlenotification"></a>[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)  
NDIS 调用[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)处理程序函数以取消未完成的空闲通知。 调用此函数时，微型端口驱动程序会取消之前为空闲通知发出的任何特定于总线的 Irp。

例如，当调用[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)时，USB 微型端口必须取消以前颁发的 usb 空闲请求 IRP。 取消 IRP 后，会通知微型端口驱动程序，此时适配器可以转换为完全电源状态。

调用微型端口驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)函数时，驱动程序会按照以下步骤注册其 NDIS 选择性挂起处理程序函数：

1.  微型端口驱动程序必须将[**NDIS\_微型端口\_驱动\_程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)的**SetOptionsHandler**成员设置为驱动程序的[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数的入口点。 驱动程序调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) ，以将其**NDIS\_微型端口\_驱动程序\_特征**结构与 NDIS 一起注册。

2.  NDIS 在调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)的上下文中调用[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数。

    调用[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)时，微型端口驱动程序使用指向处理程序函数的指针初始化[**NDIS\_微型\_SS\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_ss_characteristics)结构。 然后，微型端口驱动程序调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers) ，并将*OptionalHandlers*参数设置为指向**NDIS\_微型端口\_SS\_特征**结构的指针。

有关如何处理 NDIS 选择性挂起的空闲通知的详细信息，请参阅[Ndis 选择性挂起空闲通知](ndis-selective-suspend-idle-notifications.md)。

 

 





