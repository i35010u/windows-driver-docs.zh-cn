---
title: NDIS 选择性挂起概述
description: NDIS 选择性挂起概述
ms.assetid: D23E103E-893E-4B42-8EFD-0524846EF45F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ba167fbc75c94f95acd8a69f467429af69f5e9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382653"
---
# <a name="overview-of-ndis-selective-suspend"></a>NDIS 选择性挂起概述


从开始 NDIS 6.30，NDIS 选择性挂起接口允许通过转换到低功耗状态适配器挂起空闲的网络适配器的 NDIS。 这使系统可以减少 CPU 和功耗开销的适配器。

NDIS 选择性挂起特别适合用于基于 USB v1.1 和 v2.0 接口的网络适配器。 这些适配器收到的数据包而不考虑它们是否活动或空闲持续轮询。 通过停用空闲的 USB 适配器，CPU 开销可以减少 10%。

NDIS 选择性挂起基于[USB 选择性挂起](../usbcon/usb-selective-suspend.md)技术。 但是，NDIS 选择性挂起旨在作为总线无关。 在这种方式，独立于总线的 I/O 请求数据包 (Irp) 的选择性挂起颁发的 NDIS。 这使得微型端口驱动程序负责颁发所需的任何 Irp 选择性挂起特定的总线上。 例如，微型端口驱动程序用于 USB 网络适配器发出空闲的总线特定于 USB 请求 IRP ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 到 USB 总线驱动程序在选择性挂起操作。

NDIS 和微型端口驱动程序参与 NDIS 选择性挂起如下所示：

1.  如果微型端口驱动程序已注册其支持 NDIS 选择性挂起，NDIS 监视的网络适配器的 I/O 活动。 I/O 活动包括接收数据包的指示，发送数据包完成和 OID 处理的请求的微型端口驱动程序。

2.  NDIS 将视为处于空闲状态，如果它已处于非活动状态的时间超过指定的空闲超时期限的网络适配器。 在此情况下，选择性 NDIS 启动挂起操作，以便转换到低功耗状态的网络适配器到微型端口驱动程序发出的空闲通知。

    > [!NOTE]
    > 值指定空闲超时期限的长度 **\*SSIdleTimeout**标准化 INF 关键字。 有关此关键字的详细信息，请参阅[NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。     

    NDIS 如何确定网络适配器处于空闲状态的详细信息，请参阅[如何 NDIS 检测到空闲的网络适配器](how-ndis-detects-idle-network-adapters.md)。

3.  NDIS 颁发给微型端口驱动程序通过调用在驱动程序的空闲通知[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)处理程序函数。 当调用此函数时，微型端口驱动程序确定网络适配器是否可以转换到低功耗状态。 微型端口驱动程序执行的特定于总线的方式确定。

    例如，USB 微型端口驱动程序确定是否将网络适配器可以过渡到低功耗状态通过发出 USB 空闲请求 IRP ([**IOCTL\_内部\_USB\_提交\_IDLE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 为基础的 USB 总线驱动程序。 这会通知总线驱动程序的网络适配器处于空闲状态，并确认该适配器是否可以转换为低功耗状态。
    
    > [!NOTE]
    > 微型端口驱动程序必须指定 USB 空闲请求 IRP 的回调和完成例程。
    
    有关如何微型端口驱动程序处理的空闲通知的详细信息，请参阅[处理 NDIS 挂起空闲选择性通知](handling-the-ndis-selective-suspend-idle-notification.md)。

4.  微型端口驱动程序确定网络适配器可以过渡到低功耗状态后，它会调用[ **NdisMIdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)。 在此调用中，微型端口驱动程序指定的网络适配器可以转换到的最低电源状态。

5.  当[ **NdisMIdleNotificationConfirm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationconfirm)是调用，NDIS 对要转换到低功耗状态为准备该适配器的微型端口驱动程序中发出 OID 请求。 NDIS 也会发出 Irp 到基础总线驱动程序将适配器设置为低功耗状态。

6.  已挂起的网络适配器后，它仍处于低功耗状态，直到取消未完成的空闲通知。

    NDIS 取消通过调用微型端口驱动程序的未完成的空闲通知[ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)处理程序函数。 NDIS 调用此处理程序函数，如果一个或多个以下条件成立：

    -   NDIS 检测到的数据包发送请求或 OID 请求的过量协议或筛选器驱动程序从颁发给微型端口驱动程序。

    -   网络适配器向唤醒事件发出信号。 接收适配器接收的数据包，或在其媒体连接状态中检测到更改时，这可能发生。

    已挂起的网络适配器后，微型端口驱动程序还可以完成空闲通知才能恢复全功率状态到适配器。 执行此操作的原因是特定于设计和驱动程序和适配器的要求。

    有关如何 NDIS 取消空闲通知的详细信息，请参阅[取消 NDIS 挂起空闲选择性通知](canceling-the-ndis-selective-suspend-idle-notification.md)。

    有关如何微型端口驱动程序完成空闲通知的详细信息，请参阅[完成 NDIS 挂起空闲选择性通知](completing-the-ndis-selective-suspend-idle-notification.md)。

7.  当[ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)调用处理程序函数，该微型端口驱动程序确定网络适配器是否可以恢复全功率状态。 该驱动程序也将取消任何特定于总线的 Irp，它可能以前颁发的空闲通知。

    网络适配器可以转换为全功率状态决定是总线特定的。 例如，当[ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)调用时，USB 微型端口必须取消以前颁发的 USB 空闲请求 IRP。 一旦 USB 驱动程序已取消 IRP，它将调用 IRP 的完成例程，以确认取消 IRP 和网络适配器可以恢复到全功率状态。 在上下文中完成例程，微型端口驱动程序调用[ **NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)。

    当微型端口确定网络适配器可以恢复到全功率状态时，它将调用[ **NdisMIdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)。 此调用通知 NDIS 空闲通知已完成。 NDIS 然后继续进行完成选择性挂起操作通过转换为全功率状态的网络适配器。

8.  当[ **NdisMIdleNotificationComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismidlenotificationcomplete)是调用，NDIS 对要转换到全功率状态为准备该适配器的微型端口驱动程序中发出 OID 请求。 NDIS 也会发出 Irp 到基础总线驱动程序将适配器设置为全功率状态。

9.  如果为全功率状态恢复的网络适配器，选择性挂起操作完成。 NDIS 恢复监视的网络适配器的 I/O 活动。 如果适配器在另一个空闲超时期限后变为非活动状态，NDIS 空闲通知向发出微型端口驱动程序以挂起的网络适配器。