---
title: 取消 NDIS 选择性挂起空闲通知
description: 取消 NDIS 选择性挂起空闲通知
ms.assetid: 14C19F15-9D0E-4F37-942C-7F7AFE1EBA0B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b9396ebc74e8116f601b8ab209bc95c3fcaf092
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218479"
---
# <a name="canceling-the-ndis-selective-suspend-idle-notification"></a>取消 NDIS 选择性挂起空闲通知


如果网络适配器处于空闲超时期限内处于非活动状态，NDIS 将启动选择性挂起操作。 完成此操作后，网络适配器会转换为低功耗状态。 NDIS 通过向微型端口驱动程序发出空闲通知来开始此操作。 有关此操作的详细信息，请参阅 [处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

NDIS 调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 处理程序函数来通知驱动程序，基础网络适配器似乎处于空闲状态。 发出空闲通知后，如果满足以下一个或多个条件，NDIS 将取消挂起的空闲通知：

-   过量协议或筛选器驱动程序发出发送数据包请求或对象标识符 (OID) 请求到微型端口驱动程序。

    有关 NDIS 如何为此方案取消空闲通知的详细信息，请参阅 [由于过量驱动程序活动而取消空闲通知](#canceling-the-idle-notification-because-of-overlying-driver-activity)。

-   基础适配器发出唤醒事件，例如接收数据包或检测其媒体连接状态的更改。

    有关 NDIS 如何为此方案取消空闲通知的详细信息，请参阅 [取消空闲通知，因为出现了唤醒事件](#canceling-the-idle-notification-because-of-wake-up-events)。

NDIS 通过调用基础微型端口驱动程序的 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 处理程序函数来取消空闲通知。 调用此函数时，微型端口驱动程序必须完成空闲通知，才能将适配器恢复到完全电源状态。 有关此过程的指导原则，请参阅 [完成 NDIS 选择性挂起空闲通知](completing-the-ndis-selective-suspend-idle-notification.md)。

有关如何实现 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 处理程序函数的详细信息，请参阅 [实现 *MiniportCancelIdleNotification* 处理程序函数](implementing-a-miniportcancelidlenotification-handler-function.md)。

## <a name="canceling-the-idle-notification-because-of-overlying-driver-activity"></a>由于过量驱动程序活动而取消空闲通知


NDIS 监视颁发给微型端口驱动程序的发送请求和 OID 请求，其网络适配器已挂起并且处于低功耗状态。 发生这种情况时，NDIS 会取消未完成的空闲通知，以便网络适配器可以恢复到全电源状态。

当取消空闲通知时，NDIS 和微型端口驱动程序会执行以下步骤：

1.  NDIS 调用 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 处理程序函数以取消未完成的空闲通知。 调用此处理程序函数时，微型端口驱动程序必须取消 (Irp 的任何特定于总线的 i/o 请求包，) 可能之前为空闲通知发出此包。

    例如，当调用 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 时，USB 网络适配器的微型端口会执行以下步骤：

    1.  小型端口驱动程序将取消挂起的 USB 空闲请求 ([**IOCTL \_ 内部 \_ usb \_ 提交 \_ 空闲 \_ 通知**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) IRP。 当 NDIS 调用驱动程序的 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 函数时，小型端口驱动程序先前将此 IRP 颁发给基础 USB 总线驱动程序。 微型端口驱动程序通过调用 [**IoCancelIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)来取消此 IRP。

    2.  当总线驱动程序取消 USB 空闲请求 IRP 后，它将调用 IRP 的微型端口驱动程序的完成例程。 此调用会通知驱动程序 IRP 已完成，并且网络适配器可以转换为完全电源状态。 从完成例程的上下文中，驱动程序调用 [**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete) 来通知 NDIS，网络适配器可以转换为完全电源状态。

    **注意** 根据取消特定于总线的空闲请求的依赖项，微型端口驱动程序会在调用[*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)或在*MiniportCancelIdleNotification*返回后以异步方式调用[**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete) 。

    有关如何实现 USB 空闲请求 IRP 完成例程的详细信息，请参阅 [实现 Usb 空闲请求 Irp 完成例程](implementing-a-usb-idle-request-irp-completion-routine.md)。

2.  在微型端口驱动程序为空闲通知取消任何特定于总线的 Irp 后，它将调用 [**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)。 此调用会通知 NDIS 空闲通知已完成。 然后，NDIS 通过将网络适配器转换为完全电源状态来完成选择性挂起操作。

    调用 [**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete) 时，NDIS 执行以下步骤：

    1.  NDIS 问题 IRP MN 为基础总线驱动程序 [** \_ \_ 设置 \_ 电源**](../kernel/irp-mn-set-power.md) 。 此 IRP 请求总线驱动程序将网络适配器的电源状态设置为 PowerDeviceD0。

    2.  NDIS 向微型端口驱动程序发出 [oid \_ PNP \_ 设置 \_ 功能](./oid-pnp-set-power.md) 的 oid 设置请求。 在此 OID 请求中，NDIS 指定网络适配器现在正在转换为 NdisDeviceStateD0 的完全电源状态。

        当它处理此 OID 集请求时，驱动程序会准备适配器以实现完全电源操作。 这包括将接收和发送引擎还原到在转换到低功耗状态之前所处的状态。 然后，该驱动程序将完成 OID 请求，并获得 NDIS \_ 状态 \_ SUCCESS。

下图显示了 NDIS 取消颁发给 USB 网络适配器的微型端口驱动程序的空闲通知时所涉及的步骤。

![显示空闲通知恢复过程的示意图](images/ndis-ss-idle-notification-resume.png)

## <a name="canceling-the-idle-notification-because-of-wake-up-events"></a>由于唤醒事件而取消空闲通知


在将网络适配器转换为低功耗状态之前，NDIS 会向网络适配器发出 oid [ \_ PM \_ 参数](./oid-pm-parameters.md) 的 oid 设置请求。 此 OID 请求指定唤醒事件的类型，适配器可以通过该类型发出信号以恢复到完全电源状态。 对于 NDIS 选择性挂起，适配器配置为发出以下任何唤醒事件的信号：

-   接收到的数据包与先前通过 OID 集的 oid 集请求配置的筛选器的接收 [ \_ \_ 添加 \_ WOL \_ 模式](./oid-pm-add-wol-pattern.md) 或 oid 生成 [ \_ \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md)。

-   适配器上媒体连接状态的更改。

Ndis 和微型端口驱动程序在 NDIS 由于网络适配器生成的唤醒信号而取消空闲通知时，请按照以下步骤操作：

1.  总线驱动程序完成 NDIS 发出的 [**IRP \_ MN \_ 等待 \_ 唤醒**](../kernel/irp-mn-wait-wake.md) ，然后将适配器转换为低功耗状态。 通过完成 IRP，总线驱动程序会通知 NDIS 网络适配器已生成唤醒信号。

2.  NDIS 调用 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 处理程序函数来启动取消空闲通知的操作。 此操作所涉及的步骤与 [由于过量驱动程序活动而取消空闲通知](#canceling-the-idle-notification-because-of-overlying-driver-activity)中所述的步骤相同。

例如，下图显示由于 USB 网络适配器发出的唤醒事件，NDIS 取消空闲通知时所涉及的步骤。

![显示空闲通知唤醒过程的关系图](images/ndis-ss-idle-notification-resume-wake.png)