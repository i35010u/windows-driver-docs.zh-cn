---
title: 微型端口驱动程序的适配器状态
description: 微型端口驱动程序的适配器状态
ms.assetid: 3ca03511-a912-4ee3-bd9f-1bd8e6996c48
keywords:
- NDIS 微型端口驱动程序 WDK，适配器状态
- 适配器状态 WDK 网络
- 微型端口适配器 WDK 网络，状态
- 微型端口驱动程序 WDK 网络，微型端口适配器
- NDIS 微型端口驱动程序 WDK、微型端口适配器
- 暂停状态 WDK 网络
- S
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e63439bf71ba0ab49378b9804f5d645f68f78962
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215280"
---
# <a name="adapter-states-of-a-miniport-driver"></a>微型端口驱动程序的适配器状态





对于它管理的每个微型端口适配器， [NDIS 微型端口驱动程序](ndis-miniport-drivers2.md) 必须支持以下操作状态集：

-   中断

-   Shutdown

-   正在初始化

-   已暂停

-   重新启动

-   正在运行

-   正在暂停

下图显示了这些状态之间的相互关系。

![说明微型端口适配器状态图的关系图](images/miniportstate.png)

**注意**   Reset 操作不会影响微型端口适配器操作状态。 此外，当重置操作正在进行时，适配器的状态可能会发生更改。 例如，当正在进行重置操作时，NDIS 可能会调用驱动程序的暂停处理程序。 在这种情况下，驱动程序可以按任意顺序完成重置或暂停操作，同时满足每个操作的一般要求。 对于 reset 操作，驱动程序可能会导致传输请求数据包失败，或者可以将它们保留在队列中，稍后再完成。 但是，你应注意，如果某个过量驱动程序的传输数据包处于挂起状态，则无法完成暂停操作。

 

下面定义了适配器状态：

<a href="" id="halted"></a>中断  
*暂停* 是所有微型端口适配器的初始状态。 当微型端口适配器处于 "已停止" 状态，并且 NDIS 调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数以初始化微型端口适配器时，微型端口适配器将进入 "正在初始化" 状态。 如果 *MiniportInitializeEx* 失败，微型端口适配器将返回到 "已停止" 状态。 当微型端口适配器处于暂停状态并且 NDIS 调用 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数时，微型端口适配器将返回到 "已停止" 状态。

<a href="" id="shutdown"></a>立即  
在关闭并重新启动系统之前，不能使用处于 *关闭* 状态的微型端口适配器。 当微型端口适配器处于暂停、重新启动、正在运行或暂停状态，并且 NDIS 调用微型端口驱动程序的 [*MiniportShutdownEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown) 函数时，微型端口适配器将进入关闭状态。

<a href="" id="initializing"></a>出错  
在 " *正在初始化* " 状态下，微型端口驱动程序完成初始化微型端口适配器所需的任何操作。 当微型端口适配器处于暂停状态，并且 NDIS 调用微型端口驱动程序的 *MiniportInitializeEx* 函数时，微型端口适配器将进入 "正在初始化" 状态。 如果 *MiniportInitializeEx* 成功，微型端口适配器将进入暂停状态。 如果 *MiniportInitializeEx* 失败，微型端口适配器将返回到 "已停止" 状态。

<a href="" id="paused"></a>悬停  
当微型端口适配器处于 *暂停* 状态时，微型端口驱动程序不会指示接收的网络数据或接受发送请求。 当微型端口适配器处于暂停状态并且暂停操作完成后，微型端口适配器将进入暂停状态。 当微型端口适配器处于 "正在初始化" 状态且 *MiniportInitializeEx* 为 "成功" 时，微型端口适配器将进入暂停状态。 当 NDIS 调用微型端口驱动程序的 [**MiniportRestart**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart) 函数时，微型端口适配器将从 "已暂停" 状态转换为 "正在重新启动" 状态。 当 NDIS 调用微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数时，微型端口适配器将从 "已暂停" 状态转换为 "已暂停" 状态。

<a href="" id="restarting"></a>重新启动  
在 *重新启动* 状态下，微型端口驱动程序完成为微型端口适配器重新启动发送和接收操作所需的任何操作。 当微型端口适配器处于暂停状态，并且 NDIS 调用驱动程序的 *MiniportRestart* 函数时，微型端口适配器将进入重新启动状态。 如果重启失败，微型端口适配器将恢复到暂停状态。 如果重新启动成功，微型端口适配器将进入 "正在运行" 状态。

<a href="" id="running"></a>耗尽  
在 " *正在运行* " 状态下，微型端口驱动程序为微型端口适配器执行发送和接收处理的常规处理。 当微型端口适配器处于重启状态并且驱动程序已准备好执行发送和接收操作时，微型端口适配器将进入 "正在运行" 状态。

<a href="" id="pausing"></a>暂停  
在 *暂停* 状态下，微型端口驱动程序完成停止端口适配器的发送和接收操作所需的任何操作。 驱动程序必须等待 NDIS 返回所有未完成的接收指示。 当微型端口适配器处于 "正在运行" 状态，并且 NDIS 调用驱动程序的 [*MiniportPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause) 函数时，微型端口适配器将进入暂停状态。 小型端口驱动程序不能使暂停操作失败。 暂停操作完成后，微型端口适配器将进入暂停状态。

## <a name="related-topics"></a>相关主题


[驱动程序堆栈管理](driver-stack-management.md)

[NDIS 微型端口驱动程序](ndis-miniport-drivers2.md)

 

