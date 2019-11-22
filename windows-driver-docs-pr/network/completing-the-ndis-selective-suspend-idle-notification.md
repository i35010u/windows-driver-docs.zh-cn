---
title: 完成 NDIS 选择性挂起空闲通知
description: 完成 NDIS 选择性挂起空闲通知
ms.assetid: 2330A8EE-DC8B-4244-935C-DEF20A6EB5E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9132bcc874fca29dfe1440a81e1da3f6ef665160
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835158"
---
# <a name="completing-the-ndis-selective-suspend-idle-notification"></a>完成 NDIS 选择性挂起空闲通知


NDIS 调用[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数来通知驱动程序，基础网络适配器似乎处于空闲状态。 有关此操作的详细信息，请参阅[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

发出空闲通知后，小型端口驱动程序会在以下情况下完成 NDIS 选择性挂起空闲通知：

-   NDIS 通过调用基础微型端口驱动程序的[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)处理程序函数来取消空闲通知。

-   微型端口驱动程序完成空闲通知。 执行此操作的原因特定于驱动程序和适配器的设计和要求。 例如，如果在网络适配器上检测到 "接收" 活动，则驱动程序可以完成空闲通知。

**请注意**  微型端口驱动程序无法显式取消空闲通知。 当 NDIS 取消空闲通知时，微型端口驱动程序必须按照本主题中所述完成通知。 有关详细信息，请参阅[取消 NDIS 选择性挂起空闲通知](canceling-the-ndis-selective-suspend-idle-notification.md)。

 

在任一情况下，微型端口驱动程序都必须完成空闲通知，才能将适配器恢复到完全电源状态。 若要完成空闲通知，微型端口驱动程序必须取消任何特定于总线的 i/o 请求包（Irp），该包先前可能已针对空闲通知发出。 最后，驱动程序调用[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)来通知 NDIS 网络适配器可以转换为全电源状态。

例如，USB 网络适配器的微型端口驱动程序通过执行以下步骤来完成空闲通知：

1.  微型端口驱动程序将取消挂起的 USB 空闲请求（[**IOCTL\_内部\_usb\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)） IRP。 当 NDIS 调用驱动程序的[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)函数时，小型端口驱动程序先前将此 IRP 颁发给基础 USB 总线驱动程序。 微型端口驱动程序通过调用[**IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)来取消此 IRP。

2.  当总线驱动程序取消 USB 空闲请求 IRP 后，它将调用 IRP 的微型端口驱动程序的完成例程。 此调用会通知驱动程序 IRP 已完成，并且网络适配器可以转换为完全电源状态。 从完成例程的上下文中，驱动程序调用[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)来通知 NDIS，网络适配器可以转换为完全电源状态。

    有关如何实现 USB 空闲请求 IRP 完成例程的详细信息，请参阅[实现 Usb 空闲请求 Irp 完成例程](implementing-a-usb-idle-request-irp-completion-routine.md)。

**请注意**  根据用于取消特定于总线的空闲请求的依赖项，微型端口驱动程序会在调用[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)或在*MiniportCancelIdleNotification*返回后以异步方式调用[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete) 。

 

在微型端口驱动程序为空闲通知取消任何特定于总线的 Irp 后，它将调用[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)。 此调用会通知 NDIS 空闲通知已完成。 然后，NDIS 通过将网络适配器转换为完全电源状态来完成选择性挂起操作。

调用[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)时，NDIS 执行以下步骤：

1.  NDIS 问题[**IRP\_MN\_将\_电源设置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)为底层总线驱动程序。 此 IRP 请求总线驱动程序将网络适配器的电源状态设置为 PowerDeviceD0。

2.  NDIS 发出[\_PNP\_设置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)的对象标识符（oid）设置请求，\_微型端口驱动程序。 在此 OID 请求中，NDIS 指定网络适配器现在正在转换为 NdisDeviceStateD0 的完全电源状态。

    当它处理此 OID 集请求时，驱动程序会准备适配器以实现完全电源操作。 这包括将接收和发送引擎还原到在转换到低功耗状态之前所处的状态。 然后，该驱动程序完成 OID 请求，并将 NDIS\_状态\_SUCCESS。

下图显示了在微型端口驱动程序完成 USB 网络适配器的空闲通知时所涉及的步骤。

![显示空闲通知恢复过程的示意图](images/ndis-ss-idle-notification-complete.png)

**请注意**  当微型端口驱动程序完成空闲通知时，它不能为以前通过调用[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)而完成的空闲通知调用[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm) 。

 

 

 





