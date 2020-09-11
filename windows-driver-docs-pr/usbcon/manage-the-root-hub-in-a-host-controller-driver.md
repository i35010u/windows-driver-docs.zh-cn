---
description: UCX 执行根集线器管理。
title: USB 主控制器驱动程序的根集线器回调函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 525d07b4754440d844ef90a421d46a316a3b3678
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010617"
---
# <a name="root-hub-callback-functions-of-a-usb-host-controller-driver"></a>USB 主控制器驱动程序的根集线器回调函数


UCX 执行根集线器管理。 它模拟并管理虚拟控制和中断端点。 当主机控制器驱动程序创建根中心对象时，UCX 将创建这些虚拟终结点。

USB 集线器驱动程序与根集线器交互的方式与与常规集线器设备交互的方式相同。 但是，主机控制器驱动程序不必直接处理发送到控件和中断终结点的根集线器的请求。 UCX 处理这些请求。 UCX 调用由主机控制器驱动程序实现的回调函数，以便它可以返回有关主机控制器端口的当前状态的相关信息。 完成这些回调函数后，将完成基础 UCX 请求，并将其返回给集线器驱动程序。

接收到根集线器的中断传输后，UCX 会将请求设置为 "挂起"。 当在其中一个根集线器端口上检测到更改时，主机控制器驱动程序将调用 [**UcxRootHubPortChanged**](/windows-hardware/drivers/ddi/ucxroothub/nf-ucxroothub-ucxroothubportchanged)。 然后，UCX 调用驱动程序的 [*.Evt \_ UCX \_ ROOTHUB \_ 中断 \_ TX*](/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_interrupt_tx) 回拨，驱动程序指示已更改的端口。 此时，UCX 完成挂起的请求并返回到集线器驱动程序。 集线器驱动程序向根集线器发送控件传输，以获取发出更改的端口的端口状态。 用于控制将请求传输到挂起的 UCX 集，并调用驱动程序的 [*.Evt \_ UCX \_ ROOTHUB \_ control \_ URB*](/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_control_urb) 回调函数。 在实现中，将返回根集线器端口的当前状态，包括设备已连接的指示。 UCX 完成对集线器驱动程序的控制传输请求，设备枚举将继续。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)