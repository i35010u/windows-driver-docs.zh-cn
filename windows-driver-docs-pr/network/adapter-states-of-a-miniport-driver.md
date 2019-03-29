---
title: 微型端口驱动程序的适配器状态
description: 微型端口驱动程序的适配器状态
ms.assetid: 3ca03511-a912-4ee3-bd9f-1bd8e6996c48
keywords:
- NDIS 微型端口驱动程序 WDK，适配器状态
- 适配器状态 WDK 网络
- 微型端口适配器 WDK 网络状态
- 微型端口驱动程序 WDK 网络，微型端口适配器
- NDIS 微型端口驱动程序 WDK，微型端口适配器
- 非暂停的状态下 WDK 网络
- S
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3637d82b4f8566da3451f60552ac77f5c4f80ca6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576219"
---
# <a name="adapter-states-of-a-miniport-driver"></a>微型端口驱动程序的适配器状态





为管理，每个微型端口适配器[NDIS 微型端口驱动程序](ndis-miniport-drivers2.md)必须支持以下一组操作状态：

-   暂停

-   关机

-   初始化

-   已暂停

-   重新启动

-   正在运行

-   暂停

下图显示了这些状态之间的相互关系。

![说明微型端口适配器状态图的关系图](images/miniportstate.png)

**请注意**  重置操作不会影响微型端口适配器操作状态。 此外，重置操作正在进行时，可能会更改该适配器的状态。 例如，NDIS 可能会重置操作正在进行中的时调用的驱动程序暂停处理程序。 在这种情况下，该驱动程序可以完成重置或暂停操作，按任意顺序遵循每个操作的常规要求。 对于重置操作，该驱动程序可能会传输请求数据包失败或它可以使它们保持排队和完成这些更高版本。 但是，您应该注意基础驱动程序无法完成暂停操作时其传输数据包处于挂起状态。

 

以下定义的适配器状态：

<a href="" id="halted"></a>暂停  
*暂停*是所有微型端口适配器的初始状态。 当微型端口适配器处于暂停状态，并 NDIS 调用驱动程序的[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数初始化的微型端口适配器，微型端口适配器进入正在初始化状态。 如果*MiniportInitializeEx*失败，微型端口适配器返回到暂停状态。 调用时的微型端口适配器处于已暂停状态，NDIS [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数，微型端口适配器返回到暂停状态。

<a href="" id="shutdown"></a>关闭  
中的微型端口适配器*关闭*状态不能使用，直到系统关闭并重新启动。 当微型端口适配器处于已暂停，重新启动、 正在运行或暂停状态和 NDIS 调用微型端口驱动程序[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)函数，微型端口适配器进入关闭状态。

<a href="" id="initializing"></a>正在初始化  
在中*正在初始化*状态中时，微型端口驱动程序完成初始化的微型端口适配器所需的任何操作。 当微型端口适配器处于暂停状态，NDIS 调用微型端口驱动程序*MiniportInitializeEx*函数，微型端口适配器进入正在初始化状态。 如果*MiniportInitializeEx*成功，微型端口适配器进入暂停状态。 如果*MiniportInitializeEx*失败，微型端口适配器返回到暂停状态。

<a href="" id="paused"></a>已暂停  
当微型端口适配器处于*已暂停*状态时，微型端口驱动程序不会指示接收的网络数据或接受发送请求。 如果暂停操作已完成的微型端口适配器处于暂停状态，微型端口适配器进入暂停状态。 微型端口适配器处于 Initializing 状态时， *MiniportInitializeEx*是成功，微型端口适配器进入暂停状态。 当 NDIS 调用微型端口驱动程序[ **MiniportRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff559435)函数，从暂停状态的微型端口适配器转换到正在重新启动状态。 当 NDIS 调用微型端口驱动程序[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数，从暂停状态的微型端口适配器转换为暂停状态。

<a href="" id="restarting"></a>重新启动  
在中*正在重新启动*状态中时，微型端口驱动程序完成重启发送和接收操作的微型端口适配器所需的任何操作。 当微型端口适配器处于已暂停状态，NDIS 调用驱动程序的*MiniportRestart*函数，微型端口适配器进入正在重新启动状态。 如果重新启动将失败，微型端口适配器返回到暂停状态。 如果在重新启动成功，微型端口适配器将进入运行状态。

<a href="" id="running"></a>运行  
在中*运行*状态、 微型端口驱动程序执行正常发送和接收的微型端口适配器处理。 当微型端口适配器处于正在重新启动状态，该驱动程序已准备好执行发送和接收操作时，微型端口适配器进入运行状态。

<a href="" id="pausing"></a>暂停  
在中*暂停*状态中时，微型端口驱动程序完成停止发送和接收操作的微型端口适配器所需的任何操作。 该驱动程序必须等待 NDIS 以返回所有未完成接收的指示。 当微型端口适配器处于运行状态，NDIS 调用驱动程序的[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)函数，微型端口适配器进入暂停状态。 微型端口驱动程序不能故障暂停操作。 暂停操作完成后，微型端口适配器进入暂停状态。

## <a name="related-topics"></a>相关主题


[驱动程序堆栈管理](driver-stack-management.md)

[NDIS 微型端口驱动程序](ndis-miniport-drivers2.md)

 

 






