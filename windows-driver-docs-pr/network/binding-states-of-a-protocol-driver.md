---
title: 协议驱动程序的绑定状态
description: 协议驱动程序的绑定状态
ms.assetid: 15bc6217-e258-4e07-abc8-6c46fd01d85b
keywords:
- 协议驱动程序 WDK 网络，绑定状态
- NDIS 协议驱动程序 WDK，绑定状态
- 绑定状态 WDK 网络
- 协议绑定 WDK 网络
- 协议驱动程序 WDK 网络，协议绑定
- NDIS 协议驱动程序 WDK，协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8e47cfc9c543c58d7049c191918d44dd1c3f829
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838220"
---
# <a name="binding-states-of-a-protocol-driver"></a>协议驱动程序的绑定状态





对于驱动程序管理的每个绑定， [NDIS 协议驱动程序](ndis-protocol-drivers2.md)必须支持以下操作状态：

-   未绑定

-   结

-   Running

-   结束语

-   暂停

-   暂停

-   重新

下图显示了这些状态之间的关系。

![阐释绑定状态图的图](images/protocolstate.png)

下面定义了协议驱动程序绑定状态：

<a href="" id="unbound"></a>未绑定  
*未绑定*状态是绑定的初始状态。 在此状态下，协议驱动程序将等待 NDIS 调用[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数。 在 NDIS 调用*ProtocolBindAdapterEx*后，绑定进入 "正在打开" 状态。 解除绑定操作完成后，绑定将从关闭状态返回到未绑定状态。

<a href="" id="opening"></a>结  
在 "*正在打开*" 状态下，协议驱动程序为绑定分配资源，并尝试打开微型端口适配器。 在 NDIS 调用驱动程序的*ProtocolBindAdapterEx*函数后，绑定将进入打开状态。 如果协议驱动程序未能绑定到微型端口适配器，则绑定将返回到未绑定状态。 如果驱动程序成功绑定到微型端口适配器，则绑定进入暂停状态。

<a href="" id="running"></a>耗尽  
在 "*正在运行*" 状态下，协议驱动程序为绑定执行发送和接收处理的常规处理。 当绑定处于重启状态并且驱动程序已准备好执行发送和接收操作时，绑定将进入正在运行状态。

<a href="" id="closing"></a>结束语  
在*关闭*状态下，协议驱动程序会关闭到微型端口适配器的绑定，然后释放绑定的资源。 在 NDIS 调用了协议驱动程序的[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数后，绑定将进入关闭状态。 协议驱动程序完成解除绑定操作后，绑定将进入未绑定状态。

<a href="" id="pausing"></a>暂停  
在*暂停*状态下，协议驱动程序完成为绑定停止发送和接收操作所需的任何操作。 当绑定处于 "正在运行" 状态并且 NDIS 向协议驱动程序发送 PnP 暂停通知时，绑定将进入暂停状态。 协议驱动程序必须等待所有未完成的发送请求完成。 协议驱动程序不能使暂停操作失败。 暂停操作完成后，绑定进入暂停状态。

<a href="" id="paused"></a>悬停  
在*暂停*状态下，协议驱动程序不会对绑定执行发送或接收操作。 绑定处于暂停状态并且暂停操作完成后，绑定进入暂停状态。 当绑定处于打开状态并且打开操作成功完成时，绑定进入暂停状态。 如果 NDIS 发送了协议驱动程序，则绑定的 PnP 重启通知将进入重新启动状态。 如果 NDIS 调用驱动程序的[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数，则绑定进入关闭状态。

<a href="" id="restarting"></a>重新  
在*重新启动*状态下，协议驱动程序将完成为绑定重新启动发送和接收操作所需的任何操作。 当绑定处于暂停状态，并且 NDIS 向协议驱动程序发送 PnP 重启通知时，绑定将进入重新启动状态。 如果重启失败，绑定将恢复到暂停状态。 如果重新启动成功，绑定将进入 "正在运行" 状态。

## <a name="related-topics"></a>相关主题


[驱动程序堆栈管理](driver-stack-management.md)

[NDIS 协议驱动程序](ndis-protocol-drivers2.md)

 

 






