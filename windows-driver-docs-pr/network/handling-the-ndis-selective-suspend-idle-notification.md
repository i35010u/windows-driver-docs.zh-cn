---
title: 处理 NDIS 选择性挂起空闲通知
description: 处理 NDIS 选择性挂起空闲通知
ms.assetid: 02D13260-5816-4621-8527-E1E79C9AE975
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7905c1fa5c2751be4d5bef961aac0c55fe2a1d00
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342646"
---
# <a name="handling-the-ndis-selective-suspend-idle-notification"></a>处理 NDIS 选择性挂起空闲通知


NDIS 启动选择性挂起操作，如果发生以下事件之一：

-   网络适配器已处于非活动状态的时间超过空闲超时期限。 此超时期限的持续时间指定的值 **\*SSIdleTimeout**标准化 INF 关键字。 有关此关键字的详细信息，请参阅[NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

    NDIS 如何确定网络适配器处于空闲状态的详细信息，请参阅[如何 NDIS 检测到空闲的网络适配器](how-ndis-detects-idle-network-adapters.md)。

-   符合始终上始终连接 (AOAC) 技术的系统正在过渡到连接待机状态。

通过选择性挂起操作、 网络适配器转换为低功耗状态。 NDIS 开始此操作，通过调用[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)要向微型端口驱动程序发出的空闲通知处理程序函数。

微型端口驱动程序可能需要处理空闲通知时，执行依赖于总线的操作。 下图显示了通过 USB 网络适配器的微型端口驱动程序处理的空闲通知涉及的步骤。

![显示空闲通知操作的关系图](images/ndis-ss-idle-notification.png)

本主题包括以下信息有关如何处理 NDIS 选择性挂起空闲通知：

[处理对调用指导原则*MiniportIdleNotification*](#guidelines-for-handling-the-call-to-miniportidlenotification)

[为调用的指导原则**NdisMIdleNotificationConfirm**](#guidelines-for-the-call-to-ndismidlenotificationconfirm)

[取消和完成 NDIS 选择性挂起空闲通知](#canceling-and-completing-an-ndis-selective-suspend-idle-notification)

## <a name="guidelines-for-handling-the-call-to-miniportidlenotification"></a>处理对调用指导原则*MiniportIdleNotification*

NDIS 和微型端口驱动程序按照以下步骤，当调用 NDIS [ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092):

1.  NDIS 调用[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)处理程序函数，以通知似乎处于空闲状态的基础网络适配器的驱动程序。 NDIS 集*ForceIdle*的参数*MiniportIdleNotification*处理程序函数，为以下值之一：

    -   NDIS 集*ForceIdle*参数**FALSE**网络适配器已处于非活动状态的时间超过空闲超时期限。

    -   NDIS 集*ForceIdle*参数**TRUE**时符合始终上始终连接 (AOAC) 技术的系统正在过渡到连接待机状态。

2.  当[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)调用时，微型端口驱动程序可以禁止空闲通知和选择性通过返回 NDIS 挂起操作\_状态\_忙。 例如，驱动程序无法否决空闲通知，如果该驱动程序检测到网络适配器上的活动。

    如果微型端口驱动程序 vetoes 空闲通知，NDIS 重新启动网络适配器上的活动的监视器。 如果适配器空闲超时时间内再次变为非活动状态，调用 NDIS [ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)。

    **请注意**微型端口驱动程序如果不能阻止空闲通知*ForceIdle*参数设置为**TRUE**。 在这种情况下，该驱动程序必须继续使用选择性挂起操作。

3.  如果微型端口驱动程序不能阻止空闲通知，它必须执行任何特定于总线的操作，用于准备的网络适配器以选择性挂起操作。 例如，USB 网络适配器的微型端口驱动程序将执行以下步骤来确定网络适配器是否可以转换到低功耗状态：

    1.  微型端口驱动程序调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)发出 USB 空闲状态请求的 I/O 请求数据包 (IRP) ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) 为基础的 USB 总线驱动程序。 在此 IRP 微型端口驱动程序必须指定一个回调和完成例程。

        USB 总线驱动程序不会立即完成 IRP。 IRP 处于挂起状态通过低电源转变。 总线驱动程序完成 IRP 更高版本时出现任何以下事件：

        -   微型端口驱动程序取消 IRP。

        -   系统电源状态更改是必需的。

        -   从 USB 集线器中删除设备。

    2.  USB 总线驱动程序确定，它可以将网络适配器放在低功耗状态后，它会调用微型端口驱动程序的 IRP 的回调例程。 此调用确定的网络适配器可以过渡到低功耗状态。

        有关如何编写 USB 空闲请求 IRP 的回调例程的指南，请参阅[实现一个 USB 空闲请求 IRP 的回调例程](implementing-a-usb-idle-request-irp-callback-routine.md)。

4.  微型端口驱动程序的选择性挂起操作完成的网络适配器的准备后，它会调用[ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492)。 在此调用中，微型端口驱动程序指定的网络适配器可以转换到的最低电源状态。

    具体取决于的总线要求选择性挂起操作，微型端口驱动程序调用[ **NdisMIdleNotificationConfirm** ](https://msdn.microsoft.com/library/windows/hardware/hh451492)到调用的上下文中以同步方式[*MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)或后，将异步*MiniportIdleNotification*返回。 例如，USB 的微型端口驱动程序的网络适配器调用**NdisMIdleNotificationConfirm** USB 空闲状态请求的回调例程的上下文中。 USB 总线驱动程序调用回调例程的调用上下文中以同步方式[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)或后，将异步*MiniportIdleNotification*返回。

5.  如果网络适配器可以转换为低功耗状态，微型端口驱动程序将返回 NDIS\_状态\_调用 PENDING [ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)。

    **请注意**微型端口驱动程序返回 NDIS\_状态\_PENDING 因为直到驱动程序调用未完成的空闲通知[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491). 微型端口驱动程序不能返回 NDIS\_状态\_从成功[ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)。



挂起的网络适配器并将其转换为低功耗状态之前，微型端口驱动程序应执行以下操作：

-   微型端口驱动程序应处理接收到的数据包，并指示它们到 NDIS 通过调用[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)。

-   微型端口驱动程序应处理已完成的发送数据包，并指示它们到 NDIS 通过调用[ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)。

    **请注意**NDIS 将不会调用驱动程序的[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)函数来发送数据包，如果[ *MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)返回 NDIS\_状态\_PENDING。



## <a name="guidelines-for-the-call-to-ndismidlenotificationconfirm"></a>为调用的指导原则**NdisMIdleNotificationConfirm**


NDIS 和微型端口驱动程序微型端口驱动程序调用时执行以下步骤[ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492):

1.  NDIS 问题[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)到基础总线驱动程序。 此 IRP，总线驱动程序以响应外部唤醒信号中的网络适配器中唤醒。

2.  NDIS 问题的对象标识符 (OID) 设置的请求[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)微型端口驱动程序。 此 OID 请求相关联[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构，它指定在其下的网络适配器生成唤醒事件的设置。

    微型端口驱动程序必须处理的成员时请遵循以下准则[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构：

    -   如果*ForceIdle*的参数[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)处理程序函数已设置为 FALSE，NDIS 仅设置 NDIS\_PM\_选择性\_挂起\_中的已启用标志**WakeUpFlags**的成员[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。 在这种情况下，网络适配器可以发出信号的唤醒事件时出现以下事件之一：

        -   网络适配器接收的数据包，与接收数据包筛选器匹配。 适配器配置为使用这些筛选器通过 OID 的集请求[OID\_代\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)。

        -   网络适配器检测到的网络驱动程序堆栈，如当链接状态更改为媒体断开连接或连接的媒体需要处理其他外部事件。

    -   如果*ForceIdle*的参数[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)处理程序函数已设置为**TRUE**，NDIS 未设置 NDIS\_PM\_选择性\_挂起\_中的已启用标志**WakeUpFlags**隶属[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。 NDIS 在这种情况下，设置中的其他成员**NDIS\_PM\_参数**结构唤醒事件不相关到 NDIS 选择性挂起。

        **请注意**NDIS 集*ForceIdle*参数**TRUE**仅符合始终上始终连接 (AOAC) 技术的系统正在过渡到连接待机状态时。

        该驱动程序完成 OID 请求使用 NDIS\_状态\_成功。

        **请注意**如果 NDIS 设置 NDIS\_PM\_选择性\_挂起\_中的已启用标志**WakeUpFlags**隶属[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构，它会发出的 OID 集请求[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)直接向微型端口驱动程序。 这允许 NDIS 以网络驱动程序堆栈中的筛选器驱动程序的跳过处理。

3.  OID 设置的请求后[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)是已成功完成，NDIS 发出一个 OID 集请求[OID\_PNP\_设置\_电源](https://msdn.microsoft.com/library/windows/hardware/ff569780)微型端口驱动程序。

    当它处理此 OID 集请求时，该驱动程序准备转换为 OID 请求中指定了低功耗状态的网络适配器。 该驱动程序必须按以下方式完成所有挂起的操作：

    -   所有以前所指示的微型端口驱动程序等待接收数据包，以通过调用返回[ *MiniportReturnNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559437)。

    -   微型端口驱动程序将等待发送请求处理的硬件来完成。 请求完成后，必须调用微型端口驱动程序[ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)。

    -   微型端口驱动程序通过调用来完成所有挂起的发送请求[ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)。

    -   微型端口驱动程序必须取消所有挂起的 NDIS 计时器和工作项。 这些取消后，该驱动程序必须等待这些计时器完成和工作项。

    -   微型端口驱动程序必须将网络适配器放处于静止状态。 例如，驱动程序必须取消所有硬件计时器。

    微型端口驱动程序配置基础的网络适配器，若要启用以前指定的 OID 集请求中的指定的唤醒事件[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)。 微型端口驱动程序的网络适配器已准备好进行低功耗转换后，完成的 OID 集请求[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)使用 NDIS\_状态\_成功。

4.  NDIS 问题[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)到基础总线驱动程序。 此 IRP 请求的网络适配器将转换为低功耗状态。

    **请注意**在选择性挂起操作，但网络适配器将转换为对的调用中指定的设备电源状态[ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492)。 微型端口驱动程序指定在此设备电源状态*IdlePowerState*此函数的参数。

NDIS IRP 完成后，返回通过调用[ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492)。

## <a name="canceling-and-completing-an-ndis-selective-suspend-idle-notification"></a>取消和完成 NDIS 选择性挂起空闲通知

发出的空闲通知后，它可以取消并按以下方式完成：

-   NDIS 可以取消未完成的空闲通知，如果满足以下条件：

    -   基础协议或筛选器驱动程序会发出发送数据包请求或 OID 请求到微型端口驱动程序。

    -   基础适配器发出信号唤醒事件，如接收的数据包，与 LAN 唤醒 (WOL) 模式匹配或在其媒体连接状态中检测更改。

    NDIS 取消通过调用发出的空闲通知[ *MiniportCancelIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464088)。 调用此处理程序函数时，微型端口驱动程序将取消任何特定于总线的 Irp，它可能以前颁发的空闲通知。 最后，微型端口驱动程序调用[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451491)完成空闲通知。

    有关如何 NDIS 取消空闲通知的详细信息，请参阅[取消 NDIS 挂起空闲选择性通知](canceling-the-ndis-selective-suspend-idle-notification.md)。

-   网络适配器低功耗状态后，微型端口驱动程序可以完成的空闲通知本身来恢复全功率状态到适配器。 执行此操作的原因是特定于设计和驱动程序和适配器的要求。 微型端口驱动程序将通过调用完成空闲通知[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)。

    有关如何微型端口驱动程序完成空闲通知的详细信息，请参阅[完成 NDIS 挂起空闲选择性通知](completing-the-ndis-selective-suspend-idle-notification.md)。