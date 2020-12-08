---
title: 协议驱动程序
description: 协议驱动程序
keywords:
- 协议驱动程序 WDK 网络，体系结构
- NDIS 协议驱动程序 WDK、体系结构
- 传输协议驱动程序 WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: d79592761f719b60f754ff15db28c0ef66ea4cde
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821281"
---
# <a name="protocol-drivers"></a>协议驱动程序

网络协议是在驱动程序的 NDIS 层次结构中最高的驱动程序，通常用作实现传输协议堆栈（如 TCP/IP 堆栈）的传输驱动程序中的最低级别驱动程序。 *传输协议驱动程序* 分配数据包，将数据从发送应用程序复制到数据包，并通过调用 NDIS 函数将数据包发送到较低级别的驱动程序。 协议驱动程序还提供了一个协议接口，用于接收来自下一个较低级别驱动程序的传入数据包。 传输协议驱动程序将接收的数据传输到适当的客户端应用程序。

在其下边缘，使用中间网络驱动程序和微型端口驱动程序的协议驱动程序接口。 协议驱动程序调用 **Ndis * Xxx*** 函数发送数据包、读取和设置由较低级别的驱动程序维护的信息，以及使用操作系统服务。 协议驱动程序还会导出 (*ProtocolXxx* 函数的一组入口点) NDIS 调用其自身的目的，或代表较低级别的驱动程序来指示最大的接收数据包，指示较低级别的驱动程序的状态，并以其他方式与协议驱动程序通信。

在其上边缘，传输协议驱动程序具有指向协议堆栈中较高级别的驱动程序的专用接口。

> [!NOTE]
> 有关 NDIS 驱动程序堆栈的详细信息以及显示所有四个 NDIS 驱动程序类型之间关系的关系图，请参阅 [NDIS 驱动程序堆栈](ndis-driver-stack.md)。

## <a name="related-topics"></a>相关主题

[NDIS 协议驱动程序](./roadmap-for-developing-ndis-protocol-drivers.md)

[NDIS 协议驱动程序参考](/windows-hardware/drivers/ddi/_netvista/)
