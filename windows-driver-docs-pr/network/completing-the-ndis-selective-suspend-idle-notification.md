---
title: 完成 NDIS 选择性挂起空闲通知
description: 完成 NDIS 选择性挂起空闲通知
ms.assetid: 2330A8EE-DC8B-4244-935C-DEF20A6EB5E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd9d3acdc1cb0c2d065c84afdb4c66647b91a9d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344257"
---
# <a name="completing-the-ndis-selective-suspend-idle-notification"></a>完成 NDIS 选择性挂起空闲通知


NDIS 调用[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)处理程序函数，以通知似乎处于空闲状态的基础网络适配器的驱动程序。 有关此操作的详细信息，请参阅[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

微型端口驱动程序发出的空闲通知后，完成 NDIS 选择性挂起在以下情况下发出的空闲通知：

-   NDIS 取消通过调用发出的空闲通知[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)基础微型端口驱动程序的处理程序函数。

-   微型端口驱动程序完成的空闲通知本身。 执行此操作的原因是特定于设计和驱动程序和适配器的要求。 例如，如果它检测到接收活动上的网络适配器驱动程序无法完成空闲通知。

**请注意**  微型端口驱动程序不能显式取消空闲通知。 当 NDIS 取消空闲通知时，微型端口驱动程序必须完成通知，如本主题中所述。 有关详细信息，请参阅[取消 NDIS 选择性挂起空闲通知](canceling-the-ndis-selective-suspend-idle-notification.md)。

 

在任一情况下，微型端口驱动程序必须完成恢复全功率状态到适配器的空闲通知。 若要完成的空闲通知，微型端口驱动程序必须取消它可能会对空闲通知之前发出任何特定于总线的 I/O 请求数据包 (Irp)。 最后，该驱动程序调用[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)通知 NDIS 网络适配器可以转换为全功率状态。

例如，USB 网络适配器的微型端口驱动程序完成的空闲通知通过执行以下步骤：

1.  微型端口驱动程序取消挂起的 USB 空闲请求 ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) IRP。 微型端口驱动程序之前颁发此 IRP 到基础 USB 总线驱动程序时 NDIS 称为驱动程序的[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)函数。 微型端口驱动程序通过调用取消此 IRP [ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)。

2.  当总线驱动程序取消 USB 空闲请求 IRP 时，它为 IRP 调用微型端口驱动程序的完成例程。 此调用通知完成 IRP 和网络适配器可以转换为全功率状态的驱动程序。 从环境中完成例程，该驱动程序调用[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)通知 NDIS 网络适配器可以转换为全功率状态。

    有关如何实现 USB 空闲请求 IRP 完成例程的详细信息，请参阅[实现 USB 空闲请求 IRP 完成例程](implementing-a-usb-idle-request-irp-completion-routine.md)。

**请注意**  具体取决于正在取消特定于总线的空闲状态请求的依赖关系，微型端口驱动程序调用[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)任一以同步方式在调用上下文中[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)或后，将异步*MiniportCancelIdleNotification*返回。

 

微型端口驱动程序取消空闲通知任何特定于总线的 Irp 后，它会调用[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)。 此调用通知 NDIS 空闲通知已完成。 NDIS 然后完成选择性挂起操作通过转换为全功率状态的网络适配器。

当[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)是调用，NDIS 执行以下步骤：

1.  NDIS 问题[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)到基础总线驱动程序。 此 IRP 请求要设置的网络适配器的电源状态为 PowerDeviceD0 的总线驱动程序。

2.  NDIS 问题的对象标识符 (OID) 设置的请求[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)微型端口驱动程序。 在此 OID 请求中，NDIS 指定网络适配器现在转换到 NdisDeviceStateD0 全功率状态。

    当它处理此 OID 集请求时，该驱动程序为全功率工作准备适配器。 这包括还原接收和发送到相同的状态转换到低功耗状态前它们所在的引擎。 该驱动程序然后完成 OID 请求使用 NDIS\_状态\_成功。

下图显示了微型端口驱动程序完成 USB 网络适配器的空闲通知时所涉及的步骤。

![显示空闲通知恢复过程的关系图](images/ndis-ss-idle-notification-complete.png)

**请注意**  微型端口驱动程序完成后的空闲通知，它必须调用[ **NdisMIdleNotificationConfirm** ](https://msdn.microsoft.com/library/windows/hardware/hh451492)为之前的空闲通知通过调用已完成[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)。

 

 

 





