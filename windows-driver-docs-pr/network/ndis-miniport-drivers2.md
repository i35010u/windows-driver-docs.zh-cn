---
title: 微型端口驱动程序
description: 微型端口驱动程序
ms.assetid: d0b8f143-2966-4338-9d2f-96e7e9216b3a
keywords:
- 微型端口驱动程序 WDK 网络体系结构
- NDIS 微型端口驱动程序 WDK，体系结构
- 无连接驱动程序 WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: b215f5c34c376d90b9dbd3ae969e97a87ffdc192
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378307"
---
# <a name="miniport-drivers"></a>微型端口驱动程序

*NDIS 微型端口驱动程序*有两种基本功能：

-   管理网络接口卡 (NIC)，包括发送和接收数据通过 nic。

-   与更高级别的驱动程序，例如筛选器驱动程序、 中间驱动程序和协议驱动程序进行交互。

具有其 Nic 和与的 NDIS 库通过更高级别的驱动程序进行通信的微型端口驱动程序。 NDIS 库导出一套完整的函数 (**NdisM * Xxx*** 和其他**Ndis * Xxx*** 函数)，它封装所有微型端口驱动程序必须调用的操作系统函数。 微型端口驱动程序，反过来，必须导出一组的入口点 (*MiniportXxx*函数) 的 NDIS 调用其自身的用途，或代表更高级别的驱动程序，以访问微型端口驱动程序。

> [!NOTE]
> 有关 NDIS 驱动程序堆栈和一个显示所有四个的 NDIS 驱动程序类型之间的关系图的详细信息，请参阅[NDIS 驱动程序堆栈](ndis-driver-stack.md)。

以下发送和接收操作演示了使用 NDIS 和更高级别的驱动程序微型端口驱动程序的交互：

- 当传输驱动程序包含要传输的数据包时，它将调用**Ndis * Xxx*** 函数导出由 NDIS 库。 NDIS 然后将传递该数据包给微型端口驱动程序通过调用适当*MiniportXxx*微型端口驱动程序导出的函数。 微型端口驱动程序然后将数据包转发到传输的 NIC，通过调用适当**Ndis * Xxx*** 函数。

- 当 NIC 接收到其自身的数据包时，它可以发送由 NDIS 或 NIC 的微型端口驱动程序处理的硬件中断。 NDIS 通知 NIC 的微型端口驱动程序通过调用适当*MiniportXxx*函数。 微型端口驱动程序从 NIC 将数据传输的设置，然后指示接收到的数据包绑定通过调用适当的更高级别的驱动程序存在**Ndis * Xxx*** 函数。

## <a name="connectionless-and-connection-oriented-miniport-drivers"></a>无连接和面向连接的微型端口驱动程序

NDIS 支持无连接的环境和面向连接的环境的微型端口驱动程序。

*无连接的微型端口驱动程序*控制无连接网络媒体，例如以太网的 Nic。 无连接的微型端口驱动程序进一步分为反序列化和序列化驱动程序：

**请注意**  所有 NDIS 6.0 和更高版本的驱动程序反序列化。 

-   *反序列化的驱动程序*序列化其自己的操作*MiniportXxx*函数和内部的所有传入的队列发送数据包。 这会导致全双工性能明显优于，前提是驱动程序的关键部分 （只有一个线程一次可以运行的代码） 显示小。

-   *序列化的驱动程序*依赖于 NDIS 以序列化到调用其*MiniportXxx*函数以及管理其发送队列。

*面向连接的微型端口驱动程序*控制对于面向连接的网络媒体，例如 ISDN 的 Nic。 面向连接的微型端口驱动程序始终反序列化-它们始终序列化其自己的操作*MiniportXxx*函数和内部所有传入的队列发送数据包。

NDIS 微型端口驱动程序可以有非 NDIS 下边缘 （请参阅下图）。

![非 ndis 下边缘与的 ndis 微型端口驱动程序](images/nonndslo.png)

通过非 NDIS 下边缘，微型端口驱动程序使用的总线，如通用串行总线 (USB) 来控制设备上的总线类接口。 微型端口驱动程序与设备通信，发送到总线或直接向远程连接到总线的设备的 I/O 请求数据包 (Irp)。 在其上边缘的微型端口驱动程序公开标准的 NDIS 微型端口驱动程序接口，可与过量的 NDIS 驱动程序进行通信的微型端口驱动程序。

## <a name="related-topics"></a>相关主题

[NDIS 微型端口驱动程序](ndis-miniport-drivers.md)

[NDIS 微型端口驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff565969)