---
title: 取消 NDIS 选择性挂起空闲通知
description: 取消 NDIS 选择性挂起空闲通知
ms.assetid: 14C19F15-9D0E-4F37-942C-7F7AFE1EBA0B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 887127920a4a04574994d82744b50570db3c1a4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351977"
---
# <a name="canceling-the-ndis-selective-suspend-idle-notification"></a>取消 NDIS 选择性挂起空闲通知


如果空闲超时时间变为非活动状态的网络适配器，NDIS 启动选择性挂起操作。 通过此操作，网络适配器转换为低功耗状态。 NDIS 开始此操作通过向微型端口驱动程序发出的空闲通知。 有关此操作的详细信息，请参阅[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

NDIS 调用[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)处理程序函数，以通知似乎处于空闲状态的基础网络适配器的驱动程序。 发出的空闲通知后，NDIS 取消挂起空闲通知，如果一个或多个以下条件成立：

-   基础协议或筛选器驱动程序会发出发送数据包请求或对象标识符 (OID) 请求到微型端口驱动程序。

    有关如何 NDIS 取消这种情况下的空闲通知的详细信息，请参阅[取消由于过量驱动程序活动的空闲通知](#canceling-the-idle-notification-because-of-overlying-driver-activity)。

-   基础适配器发出信号唤醒事件，如接收数据包，或在其媒体连接状态中检测更改。

    有关如何 NDIS 取消这种情况下的空闲通知的详细信息，请参阅[发生唤醒事件取消空闲通知](#canceling-the-idle-notification-because-of-wake-up-events)。

NDIS 取消通过调用发出的空闲通知[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)基础微型端口驱动程序的处理程序函数。 当调用此函数时，微型端口驱动程序必须完成恢复全功率状态到适配器的空闲通知。 此过程的指导原则，请参阅[完成 NDIS 选择性挂起空闲通知](completing-the-ndis-selective-suspend-idle-notification.md)。

有关如何实现详细信息[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)处理程序函数，请参阅[实现*MiniportCancelIdleNotification*处理程序函数](implementing-a-miniportcancelidlenotification-handler-function.md)。

## <a name="canceling-the-idle-notification-because-of-overlying-driver-activity"></a>取消由于过量驱动程序活动的空闲通知


NDIS 监视器发送请求并 OID 请求，颁发给其网络适配器已挂起并处于低功耗状态的微型端口驱动程序。 在此情况下，NDIS 取消未完成的空闲通知，以便网络适配器可以恢复到全功率状态。

NDIS 和微型端口驱动程序发出的空闲通知被取消时执行以下步骤：

1.  NDIS 调用[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)要取消未完成的空闲通知处理程序函数。 当调用此处理程序函数时，微型端口驱动程序必须取消它可能会对空闲通知之前发出任何特定于总线的 I/O 请求数据包 (Irp)。

    例如，当[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)调用时，微型端口用于 USB 网络适配器将执行以下步骤：

    1.  微型端口驱动程序取消挂起的 USB 空闲请求 ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) IRP。 微型端口驱动程序之前颁发此 IRP 到基础 USB 总线驱动程序时 NDIS 称为驱动程序的[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)函数。 微型端口驱动程序通过调用取消此 IRP [ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)。

    2.  当总线驱动程序取消 USB 空闲请求 IRP 时，它为 IRP 调用微型端口驱动程序的完成例程。 此调用通知完成 IRP 和网络适配器可以转换为全功率状态的驱动程序。 从环境中完成例程，该驱动程序调用[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)通知 NDIS 网络适配器可以转换为全功率状态。

    **请注意**具体取决于正在取消特定于总线的空闲状态请求的依赖关系，微型端口驱动程序调用[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)以同步方式中的上下文调用到[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)或后，将异步*MiniportCancelIdleNotification*返回。

    有关如何实现 USB 空闲请求 IRP 完成例程的详细信息，请参阅[实现 USB 空闲请求 IRP 完成例程](implementing-a-usb-idle-request-irp-completion-routine.md)。

2.  微型端口驱动程序取消空闲通知任何特定于总线的 Irp 后，它会调用[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)。 此调用通知 NDIS 空闲通知已完成。 NDIS 然后完成选择性挂起操作通过转换为全功率状态的网络适配器。

    当[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)是调用，NDIS 执行以下步骤：

    1.  NDIS 问题[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)到基础总线驱动程序。 此 IRP 请求要设置的网络适配器的电源状态为 PowerDeviceD0 的总线驱动程序。

    2.  NDIS 颁发的 OID 集请求[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)微型端口驱动程序。 在此 OID 请求中，NDIS 指定网络适配器现在转换到 NdisDeviceStateD0 全功率状态。

        当它处理此 OID 集请求时，该驱动程序为全功率工作准备适配器。 这包括还原接收和发送到相同的状态转换到低功耗状态前它们所在的引擎。 该驱动程序然后完成 OID 请求使用 NDIS\_状态\_成功。

下图显示了当 NDIS 取消对 USB 网络适配器的微型端口驱动程序发出的空闲通知时所涉及的步骤。

![显示空闲通知恢复过程的关系图](images/ndis-ss-idle-notification-resume.png)

## <a name="canceling-the-idle-notification-because-of-wake-up-events"></a>发生唤醒事件取消的空闲通知


NDIS 网络适配器转换为低功耗状态之前，发出的 OID 集请求[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)到网络适配器。 此 OID 请求指定的适配器可以发出信号，以恢复全功率状态唤醒事件的类型。 NDIS 选择性挂起，有关适配器已配置为发出信号的任何以下唤醒事件：

-   与以前通过 OID 配置筛选器匹配的数据包的接收设置的请求[OID\_PM\_添加\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569764)或[OID\_GEN\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)。

-   在适配器上的媒体连接状态中的更改。

NDIS 和微型端口驱动程序时 NDIS 取消的空闲通知由于唤醒信号生成的网络适配器的遵循以下步骤：

1.  总线驱动程序完成[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)转换到低功耗状态适配器之前的 NDIS 颁发。 通过完成 IRP，总线驱动程序通知 NDIS 网络适配器已生成唤醒信号。

2.  NDIS 调用[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)处理程序函数以启动取消空闲通知的操作。 在此操作中涉及的步骤都相同中所述[取消由于过量驱动程序活动的空闲通知](#cancel-due-to-driver-activity)。

例如下, 图显示了当 NDIS 取消的空闲通知由于通过 USB 网络适配器来发出信号的唤醒事件时所涉及的步骤。

![显示空闲通知唤醒过程的关系图](images/ndis-ss-idle-notification-resume-wake.png)









