---
title: 协议驱动程序
description: 协议驱动程序
ms.assetid: e144f9a6-97fc-46ac-82f8-4a1745d280c7
keywords:
- 协议驱动程序 WDK 网络体系结构
- NDIS 协议驱动程序 WDK，体系结构
- 传输协议驱动程序 WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 407ec7bbab7c8c72979949578e3b6b782c8288da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378271"
---
# <a name="protocol-drivers"></a>协议驱动程序

一种网络协议，它是驱动程序在 NDIS 层次结构中的最高驱动程序，通常用作实现传输协议堆栈，如 TCP/IP 堆栈的传输驱动程序中的最低级别驱动程序。 一个*传输协议驱动程序*分配数据包，将数据从发送应用程序到数据包，复制并通过调用 NDIS 函数将数据包发送至较低级别驱动程序。 协议驱动程序还提供一个协议界面，用于接收传入的数据包中的下一步的较低级驱动程序。 传输协议驱动程序将接收到的数据传输到相应的客户端应用程序。

在其下边缘，协议驱动程序与中间网络驱动程序和微型端口驱动程序的接口。 协议驱动程序调用**Ndis * Xxx*** 函数能够发送数据包，读取和设置的较低级驱动程序维护的信息和使用操作系统服务。 协议驱动程序也会导出一组的入口点 (*ProtocolXxx*函数) NDIS 呼叫，为其自身的用途或代表较低级别的驱动程序设置指示接收数据包，指示状态的较低级驱动程序，并否则与协议驱动程序进行通信。

在其上边缘传输协议驱动程序包含对协议堆栈中的更高级别的驱动程序的专用接口。

> [!NOTE]
> 有关 NDIS 驱动程序堆栈和一个显示所有四个的 NDIS 驱动程序类型之间的关系图的详细信息，请参阅[NDIS 驱动程序堆栈](ndis-driver-stack.md)。

## <a name="related-topics"></a>相关主题

[协议的 NDIS 驱动程序](ndis-protocol-drivers.md)

[NDIS 协议驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff566829)