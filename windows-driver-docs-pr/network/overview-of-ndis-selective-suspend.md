---
title: NDIS 选择性挂起概述
description: NDIS 选择性挂起概述
ms.assetid: D23E103E-893E-4B42-8EFD-0524846EF45F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 930e737e9911b1510002fe394a3d03882ce1adaf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843738"
---
# <a name="overview-of-ndis-selective-suspend"></a>NDIS 选择性挂起概述


从 NDIS 6.30 开始，NDIS 选择性挂起接口允许 NDIS 通过将适配器转换为低功耗状态来挂起空闲网络适配器。 这使系统能够降低适配器的 CPU 和电源开销。

对于基于 USB v2.0 和 v2.0 接口的网络适配器，NDIS 选择性挂起特别有用。 这些适配器会持续轮询接收的数据包，而不管它们是处于活动状态还是空闲状态。 通过暂停闲置 USB 适配器，可以将 CPU 开销减少10%。

NDIS 选择性挂起基于[USB 选择性挂起](../usbcon/usb-selective-suspend.md)技术。 但是，NDIS 选择性挂起旨在与总线无关。 通过这种方式，可选择挂起的与总线无关的 i/o 请求数据包（Irp）由 NDIS 发出。 这会使微型端口驱动程序负责发出在特定总线上选择性挂起所需的任何 Irp。 例如，USB 网络适配器的微型端口驱动程序在选择性挂起期间发出特定于总线的 USB 空闲请求 IRP （[**IOCTL\_内部\_usb\_向 USB 总线驱动程序提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)）运作.

NDIS 和微型端口驱动程序通过以下方式参与 NDIS 选择性挂起：

1.  如果微型端口驱动程序已注册其对 NDIS 选择性挂起的支持，NDIS 会监视网络适配器的 i/o 活动。 I/o 活动包括接收数据包指示、发送数据包完成和由微型端口驱动程序处理的 OID 请求。

2.  如果网络适配器处于非活动状态的时间超过指定的空闲超时期限，NDIS 会将网络适配器视为空闲。 发生这种情况时，NDIS 会通过向微型端口驱动程序发出空闲通知来启动选择性挂起操作，以便将网络适配器转换为低功耗状态。

    > [!NOTE]
    > 空闲超时期限的长度由 **\*SSIdleTimeout**标准化 INF 关键字的值指定。 有关此关键字的详细信息，请参阅[用于 NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。     

    有关 NDIS 如何确定网络适配器处于空闲状态的详细信息，请参阅[Ndis 如何检测空闲网络适配器](how-ndis-detects-idle-network-adapters.md)。

3.  NDIS 通过调用驱动程序的[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数，向微型端口驱动程序发出空闲通知。 调用此函数时，微型端口驱动程序确定网络适配器是否可以转换为低功耗状态。 微型端口驱动程序以特定于总线的方式执行此确定。

    例如，USB 微型端口驱动程序通过发出 USB 空闲请求 IRP （[**IOCTL\_内部\_usb\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)），确定网络适配器是否可以过渡到低功耗状态。基础 USB 总线驱动程序。 这会通知总线驱动程序网络适配器处于空闲状态，并确认适配器是否可以转换为低功耗状态。
    
    > [!NOTE]
    > 微型端口驱动程序必须为 USB 空闲请求 IRP 指定回调和完成例程。
    
    有关微型端口驱动程序如何处理空闲通知的详细信息，请参阅[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

4.  当微型端口驱动程序确认网络适配器可以转换到低功耗状态后，它将调用[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)。 在此调用中，微型端口驱动程序指定网络适配器可以转换到的最低电源状态。

5.  调用[**NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)时，NDIS 会向微型端口驱动程序发出 OID 请求，以便准备适配器，以便过渡到低功耗状态。 NDIS 还向底层总线驱动程序颁发 Irp，以将适配器设置为低功耗状态。

6.  挂起网络适配器后，它将保持低功耗状态，直到取消未完成的空闲通知。

    NDIS 通过调用微型端口驱动程序的[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)处理程序函数来取消未完成的空闲通知。 如果满足以下一个或多个条件，NDIS 将调用此处理程序函数：

    -   NDIS 检测向过量协议或筛选器驱动程序颁发给微型端口驱动程序的发送数据包请求或 OID 请求。

    -   网络适配器发出唤醒事件信号。 当适配器接收到数据包或检测到其媒体连接状态发生更改时，就会发生这种情况。

    挂起网络适配器后，微型端口驱动程序还可以完成空闲通知，以便将适配器恢复到完全电源状态。 执行此操作的原因特定于驱动程序和适配器的设计和要求。

    有关 NDIS 如何取消空闲通知的详细信息，请参阅[取消 Ndis 选择性挂起空闲通知](canceling-the-ndis-selective-suspend-idle-notification.md)。

    有关微型端口驱动程序如何完成空闲通知的详细信息，请参阅[完成 NDIS 选择性挂起空闲通知](completing-the-ndis-selective-suspend-idle-notification.md)。

7.  调用[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)处理程序函数时，微型端口驱动程序将确定网络适配器是否可以恢复到全电源状态。 驱动程序还会取消它以前为空闲通知发出的任何特定于总线的 Irp。

    确定网络适配器是否可以过渡到完全电源状态是特定于总线的。 例如，当调用[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)时，usb 微型端口必须取消以前颁发的 usb 空闲请求 IRP。 USB 驱动程序取消了 IRP 后，它将调用 IRP 的完成例程以确认 IRP 已取消，并且网络适配器可以恢复到全电源状态。 在完成例程的上下文中，微型端口驱动程序调用[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)。

    当微型端口确定网络适配器可以恢复到全功能状态时，它将调用[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)。 此调用会通知 NDIS 空闲通知已完成。 然后，NDIS 通过将网络适配器转换为完全电源状态，继续完成选择性挂起操作。

8.  调用[**NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)时，NDIS 会向微型端口驱动程序发出 OID 请求，以便准备适配器，以便转换为完全电源状态。 NDIS 还向底层总线驱动程序颁发 Irp，以将适配器设置为完全电源状态。

9.  当网络适配器恢复到完全电源状态时，将完成选择性挂起操作。 NDIS 继续监视网络适配器的 i/o 活动。 如果适配器在另一个空闲超时期限后变为非活动状态，NDIS 将向微型端口驱动程序发出空闲通知，以便挂起网络适配器。