---
title: 微型端口驱动程序
description: 微型端口驱动程序
ms.assetid: d0b8f143-2966-4338-9d2f-96e7e9216b3a
keywords:
- 微型端口驱动程序 WDK 网络，体系结构
- NDIS 微型端口驱动程序 WDK、体系结构
- 无连接驱动程序 WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae2096701724fbdfb1f14d908c5eef850b54dc1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844366"
---
# <a name="miniport-drivers"></a>微型端口驱动程序

*NDIS 微型端口驱动程序*有两个基本功能：

-   管理网络接口卡（NIC），包括通过 NIC 发送和接收数据。

-   与较高级别的驱动程序交互，如筛选器驱动程序、中间驱动程序和协议驱动程序。

微型端口驱动程序通过 NDIS 库与其 Nic 和更高级别的驱动程序通信。 NDIS 库导出一组完整的函数（**NdisM * xxx*** 和其他**NDIS * xxx*** 函数），该函数封装了微型端口驱动程序必须调用的所有操作系统函数。 然后，微型端口驱动程序必须导出一组入口点（*MiniportXxx*函数），NDIS 将其用于自己的目的，或代表更高级别的驱动程序来访问微型端口驱动程序。

> [!NOTE]
> 有关 NDIS 驱动程序堆栈的详细信息以及显示所有四个 NDIS 驱动程序类型之间关系的关系图，请参阅[NDIS 驱动程序堆栈](ndis-driver-stack.md)。

以下发送和接收操作演示了与 NDIS 驱动程序和更高级别的驱动程序的交互：

- 当传输驱动程序有要传输的数据包时，它将调用 NDIS 库导出的**ndis * Xxx*** 函数。 然后，NDIS 会通过调用微型端口驱动程序导出的相应*MiniportXxx*函数，将数据包传递到微型端口驱动程序。 然后，微型端口驱动程序通过调用相应的**Ndis * Xxx*** 函数将数据包转发到 NIC 进行传输。

- 当 NIC 接收到其自身寻址的数据包时，它可以发布由 NDIS 或 NIC 的微型端口驱动程序处理的硬件中断。 NDIS 通过调用相应的*MiniportXxx*函数通知 NIC 的微型端口驱动程序。 微型端口驱动程序设置从 NIC 传输数据，然后通过调用相应的**Ndis * Xxx*** 函数指示接收到的数据包是否存在。

## <a name="connectionless-and-connection-oriented-miniport-drivers"></a>无连接和面向连接的微型端口驱动程序

NDIS 支持无连接环境和面向连接的环境的微型端口驱动程序。

*无连接微型端口驱动程序*控制无连接网络媒体（如以太网）的 nic。 无连接微型端口驱动程序进一步分为反序列化和序列化驱动程序：

**请注意**  所有 NDIS 6.0 和更高版本的驱动程序都已反序列化。 

-   *反序列化的驱动程序*序列化其自己的*MiniportXxx*函数的操作，并在内部将所有传入的发送数据包排队。 如果驱动程序的关键部分（一次只能运行一个线程的代码）保持较小，这就会显著提高全双工性能。

-   *序列化驱动程序*依赖于 NDIS 来序列化对其*MiniportXxx*函数的调用，并管理其发送队列。

*面向连接的微型端口驱动程序*控制面向连接的网络媒体（如 ISDN）的 nic。 面向连接的微型端口驱动程序始终是反序列化的，它们始终会序列化其自己的*MiniportXxx*函数的操作，并在内部将所有传入的发送数据包排队。

NDIS 微型端口驱动程序可以具有非 NDIS 下边缘（见下图）。

![具有非 ndis 下边缘的 ndis 微型端口驱动程序](images/nonndslo.png)

通过其非 NDIS 下边缘，微型端口驱动程序使用总线的类接口，如通用串行总线（USB）来控制总线上的设备。 微型端口驱动程序通过将 i/o 请求数据包（Irp）发送到总线或直接发送到连接到总线的远程设备与设备通信。 在其上边缘，微型端口驱动程序公开了标准的 NDIS 微型端口驱动程序接口，该接口使微型端口驱动程序能够与过量 NDIS 驱动程序通信。

## <a name="related-topics"></a>相关主题

[NDIS 微型端口驱动程序](ndis-miniport-drivers.md)

[NDIS 微型端口驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)