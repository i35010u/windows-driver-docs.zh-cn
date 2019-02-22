---
title: 绑定协议驱动程序的状态
description: 绑定协议驱动程序的状态
ms.assetid: 15bc6217-e258-4e07-abc8-6c46fd01d85b
keywords:
- 协议驱动程序 WDK 网络，绑定状态
- NDIS 协议驱动程序 WDK，绑定状态
- 绑定状态 WDK 网络
- 协议绑定 WDK 网络
- 协议驱动程序 WDK 网络协议绑定
- NDIS 协议驱动程序 WDK，协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7840780652dcfd1f45b9611485648fb53f24fb2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554165"
---
# <a name="binding-states-of-a-protocol-driver"></a>绑定协议驱动程序的状态





[NDIS 协议驱动程序](ndis-protocol-drivers2.md)驱动程序管理每个绑定必须支持以下操作状态：

-   未绑定

-   打开

-   正在运行

-   关闭

-   暂停

-   已暂停

-   重新启动

以下各图显示了这些状态之间的关系。

![说明如何绑定状态关系图的图](images/protocolstate.png)

下面定义了绑定状态的协议驱动程序：

<a href="" id="unbound"></a>未绑定  
*未绑定*状态是绑定的初始状态。 在此状态下，协议驱动程序等待调用的 NDIS [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数。 在 NDIS 后调用*ProtocolBindAdapterEx*，绑定将进入打开状态。 后取消绑定操作已完成，绑定到未绑定状态从返回正在关闭状态。

<a href="" id="opening"></a>打开  
在中*打开*状态下，协议驱动程序绑定分配资源，尝试打开微型端口适配器。 NDIS 调用驱动程序的后*ProtocolBindAdapterEx*函数，该绑定将进入打开状态。 如果协议驱动程序无法将绑定到微型端口适配器，绑定将返回到未绑定状态。 如果成功，驱动程序将绑定到的微型端口适配器，绑定将进入暂停状态。

<a href="" id="running"></a>运行  
在中*运行*状态中时，协议驱动程序执行正常发送和接收处理的绑定。 如果绑定处于正在重新启动状态，该驱动程序已准备好执行发送和接收操作，绑定将进入运行状态。

<a href="" id="closing"></a>关闭  
在中*关闭*状态下，协议驱动程序关闭到微型端口适配器的绑定，然后在释放该绑定的资源。 NDIS 调用协议驱动程序的后[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)函数，该绑定会进入关闭状态。 协议驱动程序完成取消绑定操作后，该绑定将进入未绑定状态。

<a href="" id="pausing"></a>暂停  
在中*暂停*状态中时，协议驱动程序完成停止发送和接收操作的绑定所需的任何操作。 如果绑定处于运行状态，NDIS 发送协议驱动程序 PnP 暂停通知绑定将进入暂停状态。 协议驱动程序必须等待其的所有未完成发送请求，才能完成。 协议驱动程序不能故障暂停操作。 暂停操作完成后，该绑定将进入暂停状态。

<a href="" id="paused"></a>已暂停  
在中*已暂停*状态，则协议驱动程序不会执行发送或接收操作的绑定。 如果绑定处于暂停状态，完成暂停操作后，绑定将进入暂停状态。 如果绑定处于打开状态，打开操作成功完成，绑定将进入暂停状态。 如果 NDIS 发送协议驱动程序绑定的即插即用重启通知，该绑定将进入正在重新启动状态。 如果 NDIS 调用驱动程序的[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)函数，该绑定会进入关闭状态。

<a href="" id="restarting"></a>重新启动  
在中*正在重新启动*状态中时，协议驱动程序完成重启发送和接收操作的绑定所需的任何操作。 当绑定处于已暂停状态，NDIS 发送协议驱动程序即插即用的重新启动通知时，绑定将进入正在重新启动状态。 如果重新启动将失败，该绑定将返回到暂停状态。 如果在重新启动成功，绑定将进入运行状态。

## <a name="related-topics"></a>相关主题


[驱动程序堆栈管理](driver-stack-management.md)

[协议的 NDIS 驱动程序](ndis-protocol-drivers2.md)

 

 






