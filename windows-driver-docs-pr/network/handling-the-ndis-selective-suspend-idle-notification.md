---
title: 处理 NDIS 选择性挂起空闲通知
description: 处理 NDIS 选择性挂起空闲通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 941aeb0c5a8fb97e01cfd016e71794dd7b7b14b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833415"
---
# <a name="handling-the-ndis-selective-suspend-idle-notification"></a>处理 NDIS 选择性挂起空闲通知


如果发生以下事件之一，NDIS 将启动选择性挂起操作：

-   网络适配器处于非活动状态的时间超过了空闲超时期限。 此超时期限的持续时间由 **\* SSIDLETIMEOUT** 标准化 INF 关键字的值指定。 有关此关键字的详细信息，请参阅 [用于 NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

    有关 NDIS 如何确定网络适配器处于空闲状态的详细信息，请参阅 [Ndis 如何检测空闲网络适配器](how-ndis-detects-idle-network-adapters.md)。

-   符合 Always On 始终连接 (AOAC) 技术的系统正在转换为连接待机状态。

通过选择性挂起操作，网络适配器会转换为低功耗状态。 NDIS 通过调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 处理程序函数向微型端口驱动程序发出空闲通知来开始此操作。

小型端口驱动程序在处理空闲通知时可能需要执行与总线相关的操作。 下图显示了通过 USB 网络适配器的微型端口驱动程序处理空闲通知所涉及的步骤。

![显示空闲通知操作的关系图](images/ndis-ss-idle-notification.png)

本主题包括有关如何处理 NDIS 选择性挂起空闲通知的以下信息：

[处理对 *MiniportIdleNotification* 的调用的准则](#guidelines-for-handling-the-call-to-miniportidlenotification)

[调用 **NdisMIdleNotificationConfirm** 的准则](#guidelines-for-the-call-to-ndismidlenotificationconfirm)

[取消并完成 NDIS 选择性挂起空闲通知](#canceling-and-completing-an-ndis-selective-suspend-idle-notification)

## <a name="guidelines-for-handling-the-call-to-miniportidlenotification"></a>处理对 *MiniportIdleNotification* 的调用的准则

Ndis 和微型端口驱动程序在 NDIS 调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)时执行以下步骤：

1.  NDIS 调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 处理程序函数来通知驱动程序，基础网络适配器似乎处于空闲状态。 NDIS 将 *MiniportIdleNotification* 处理函数的 *ForceIdle* 参数设置为以下值之一：

    -   当网络适配器处于非活动状态的时间超过空闲超时期限时，NDIS 会将 *ForceIdle* 参数设置为 **FALSE** 。

    -   如果符合 Always On 始终连接 (AOAC) 技术的系统正在转换为连接待机状态，NDIS 会将 *ForceIdle* 参数设置为 **TRUE** 。

2.  调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 时，微型端口驱动程序可以通过返回 NDIS 状态 "忙碌" 来拒绝空闲通知和选择性挂起操作 \_ \_ 。 例如，如果驱动程序在网络适配器上检测到活动，则驱动程序可能会拒绝空闲通知。

    如果微型端口驱动程序 vetoes 空闲通知，NDIS 将在网络适配器上重新启动活动的监视器。 如果适配器在空闲超时期限内再次变为非活动状态，NDIS 将调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)。

    **注意**  如果 *ForceIdle* 参数设置为 **TRUE**，微型端口驱动程序不得否决空闲通知。 在这种情况下，驱动程序必须继续进行选择性挂起操作。

3.  如果微型端口驱动程序未拒绝空闲通知，则它必须执行任何特定于总线的操作，以便为选择性挂起操作准备网络适配器。 例如，USB 网络适配器的微型端口驱动程序执行以下步骤，以确定网络适配器是否可以转换为低功耗状态：

    1.  微型端口驱动程序调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，以发出 (IRP) USB 空闲请求的 i/o 请求， ([**IOCTL \_ 内部 \_ usb \_ \_ \_**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification) 向底层 usb 总线驱动程序提供) 。 在此 IRP 中，微型端口驱动程序必须指定回调和完成例程。

        USB 总线驱动程序不会立即完成 IRP。 IRP 通过低功耗转换保持处于挂起状态。 如果发生以下任何事件，则总线驱动程序会在以后完成 IRP：

        -   微型端口驱动程序会取消 IRP。

        -   需要系统电源状态更改。

        -   设备已从 USB 集线器中删除。

    2.  USB 总线驱动程序确定可以将网络适配器置于低功耗状态之后，会调用微型端口驱动程序的 IRP 回调例程。 此调用可确认网络适配器可以转换为低功耗状态。

        有关如何为 USB 空闲请求 IRP 编写回调例程的指导，请参阅 [实现 Usb 空闲请求 Irp 回调例程](implementing-a-usb-idle-request-irp-callback-routine.md)。

4.  当微型端口驱动程序完成网络适配器的准备以进行选择性挂起操作后，它将调用 [**NdisMIdleNotificationConfirm**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)。 在此调用中，微型端口驱动程序指定网络适配器可以转换到的最低电源状态。

    根据选择性挂起操作的总线要求，微型端口驱动程序会在调用 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)或在 *MiniportIdleNotification* 返回之后以异步方式调用 [**NdisMIdleNotificationConfirm**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm) 。 例如，USB 网络适配器的微型端口驱动程序在 USB 空闲请求的回调例程的上下文中调用 **NdisMIdleNotificationConfirm** 。 USB 总线驱动程序在对 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 的调用的上下文中以同步方式调用回调例程，或在 *MiniportIdleNotification* 返回后异步调用。

5.  如果网络适配器可以转换为低功耗状态，微型端口驱动程序将 \_ 从对 MiniportIdleNotification 的调用返回 NDIS 状态 " \_ 挂起 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)"。

    **注意**  微型端口驱动程序返回 NDIS \_ 状态 \_ "挂起"，因为在驱动程序调用 [**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)之前不会完成空闲通知。 微型端口驱动程序不得 \_ \_ 从 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)返回 NDIS 状态成功。



小型端口驱动程序应执行以下操作，直到网络适配器挂起并转换为低功耗状态：

-   微型端口驱动程序应处理收到的数据包，并通过调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)将其指示到 NDIS。

-   微型端口驱动程序应处理已完成的发送数据包，并通过调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)将其指示到 NDIS。

    **注意** 如果 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)返回 NDIS 状态 "挂起"，NDIS 不会调用驱动程序的 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数来发送数据包 \_ \_ 。



## <a name="guidelines-for-the-call-to-ndismidlenotificationconfirm"></a>调用 **NdisMIdleNotificationConfirm** 的准则


当微型端口驱动程序调用 [**NdisMIdleNotificationConfirm**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)时，NDIS 和微型端口驱动程序请按照以下步骤操作：

1.  NDIS 问题 [**IRP \_ MN \_ 等待 \_ 唤醒**](../kernel/irp-mn-wait-wake.md) 到基础总线驱动程序。 此 IRP 使总线驱动程序可以唤醒网络适配器，以响应外部唤醒信号。

2.  NDIS (OID 发出对象标识符) 将 [oid \_ PM \_ 参数](./oid-pm-parameters.md) 的请求设置为微型端口驱动程序。 此 OID 请求与 [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters) 结构关联，后者指定网络适配器生成唤醒事件时所用的设置。

    当微型端口驱动程序处理 [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters) 结构的成员时，必须遵循以下准则：

    -   如果 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数的 *ForceIdle* 参数设置为 FALSE，则 ndis 只 \_ \_ \_ \_ 在 [**NDIS \_ pm \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的 **WakeUpFlags** 成员中设置 ndis pm 选择性挂起已启用标志。 在这种情况下，当发生以下事件之一时，网络适配器可以发出唤醒事件信号：

        -   网络适配器接收与接收数据包筛选器匹配的数据包。 适配器配置为使用这些筛选器，通过 OID 设置 [oid \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md)的请求。

        -   网络适配器检测需要由网络驱动程序堆栈处理的其他外部事件，例如当链接状态更改为 "媒体断开连接" 或 "媒体已连接" 时。

    -   如果 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数的 *ForceIdle* 参数设置为 **TRUE**，ndis 不会在 \_ \_ \_ \_ [**ndis \_ pm \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的 **WakeUpFlags** 成员中设置 ndis pm 选择性挂起已启用标志。 在这种情况下，NDIS 会将 **ndis \_ PM \_ 参数** 结构中的其他成员设置为与 ndis 选择性挂起无关的唤醒事件。

        **注意**  仅当符合 Always On 始终连接 (AOAC) 技术的系统正在转换为连接待机状态时，NDIS 才将 *ForceIdle* 参数设置为 **TRUE** 。

        驱动程序完成 OID 请求，其 NDIS \_ 状态为 \_ 成功。

        **注意** 如果 NDIS \_ \_ \_ \_ 在 [**Ndis \_ pm \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的 **WakeUpFlags** 成员中设置 ndis pm 选择性挂起已启用标志，则它会直接向微型端口驱动程序发出 [oid \_ pm \_ 参数](./oid-pm-parameters.md)的 oid 设置请求。 这允许 NDIS 通过网络驱动程序堆栈中的筛选器驱动程序绕过处理。

3.  在 oid 的 OID 设置请求成功完成后，NDIS 将向微型端口驱动程序发出 OID 集请求[oid \_ PNP \_ 设置 \_ 电源](./oid-pnp-set-power.md)。 [ \_ \_ ](./oid-pm-parameters.md)

    当它处理此 OID 集请求时，驱动程序会准备网络适配器，以转换为在 OID 请求中指定的低功耗状态。 驱动程序必须通过以下方式完成所有挂起的操作：

    -   微型端口驱动程序等待所有先前指示的接收数据包通过对 [*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)的调用返回。

    -   微型端口驱动程序等待硬件处理的发送请求完成。 请求完成后，微型端口驱动程序必须调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)。

    -   微型端口驱动程序通过调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)完成所有挂起的发送请求。

    -   微型端口驱动程序必须取消所有挂起的 NDIS 计时器和工作项。 在这些操作取消后，驱动程序必须等待这些计时器和工作项完成。

    -   微型端口驱动程序必须使网络适配器处于静止状态。 例如，驱动程序必须取消所有硬件计时器。

    微型端口驱动程序将基础网络适配器配置为启用以前在 [oid \_ \_ 参数 oid 参数](./oid-pm-parameters.md)中指定的指定唤醒事件。 为网络适配器准备低功耗转换后，微型端口驱动程序将完成 [oid \_ PNP \_ 集 \_ 功能](./oid-pnp-set-power.md) 的 oid 设置请求，NDIS 状态为 " \_ \_ 成功"。

4.  NDIS 向底层总线驱动程序发出 [**IRP \_ MN \_ 设置 \_ 电源**](../kernel/irp-mn-set-power.md) 。 此 IRP 请求将网络适配器转换为低功耗状态。

    **注意**  在选择性挂起操作期间，网络适配器将转换为对 [**NdisMIdleNotificationConfirm**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)的调用中指定的设备电源状态。 微型端口驱动程序在此函数的 *IdlePowerState* 参数中指定此设备电源状态。

完成 IRP 后，NDIS 返回对 [**NdisMIdleNotificationConfirm**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationconfirm)的调用。

## <a name="canceling-and-completing-an-ndis-selective-suspend-idle-notification"></a>取消并完成 NDIS 选择性挂起空闲通知

发出空闲通知后，可以通过以下方式取消和完成该通知：

-   如果满足以下条件，NDIS 可以取消未完成的空闲通知：

    -   过量协议或筛选器驱动程序发出向微型端口驱动程序发送数据包请求或 OID 请求的问题。

    -   基础适配器发出唤醒事件，例如，接收与 LAN 唤醒 (的数据包) 模式，或检测其媒体连接状态的更改。

    NDIS 通过调用 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)来取消空闲通知。 调用此处理程序函数时，微型端口驱动程序会取消以前为空闲通知发出的任何特定于总线的 Irp。 最后，微型端口驱动程序调用 [**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete) 来完成空闲通知。

    有关 NDIS 如何取消空闲通知的详细信息，请参阅 [取消 Ndis 选择性挂起空闲通知](canceling-the-ndis-selective-suspend-idle-notification.md)。

-   网络适配器处于低功耗状态后，微型端口驱动程序可以完成空闲通知本身，以将适配器恢复到完全电源状态。 执行此操作的原因特定于驱动程序和适配器的设计和要求。 微型端口驱动程序通过调用 [**NdisMIdleNotificationComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismidlenotificationcomplete)完成空闲通知。

    有关微型端口驱动程序如何完成空闲通知的详细信息，请参阅 [完成 NDIS 选择性挂起空闲通知](completing-the-ndis-selective-suspend-idle-notification.md)。
