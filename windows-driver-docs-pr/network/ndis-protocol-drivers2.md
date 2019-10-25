---
title: 协议驱动程序
description: 协议驱动程序
ms.assetid: e144f9a6-97fc-46ac-82f8-4a1745d280c7
keywords:
- 协议驱动程序 WDK 网络，体系结构
- NDIS 协议驱动程序 WDK、体系结构
- 传输协议驱动程序 WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9aa935b6340b811255230932fdde781f62a90da4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842171"
---
# <a name="protocol-drivers"></a>协议驱动程序

网络协议是在驱动程序的 NDIS 层次结构中最高的驱动程序，通常用作实现传输协议堆栈（如 TCP/IP 堆栈）的传输驱动程序中的最低级别驱动程序。 *传输协议驱动程序*分配数据包，将数据从发送应用程序复制到数据包，并通过调用 NDIS 函数将数据包发送到较低级别的驱动程序。 协议驱动程序还提供了一个协议接口，用于接收来自下一个较低级别驱动程序的传入数据包。 传输协议驱动程序将接收的数据传输到适当的客户端应用程序。

在其下边缘，使用中间网络驱动程序和微型端口驱动程序的协议驱动程序接口。 协议驱动程序调用**Ndis * Xxx*** 函数发送数据包、读取和设置由较低级别的驱动程序维护的信息，以及使用操作系统服务。 协议驱动程序还会导出一组入口点（*ProtocolXxx*函数），NDIS 会自行调用这些入口点或代表较低级别的驱动程序来指明接收数据包，指出较低级别的驱动程序的状态，以及其他与协议驱动程序通信。

在其上边缘，传输协议驱动程序具有指向协议堆栈中较高级别的驱动程序的专用接口。

> [!NOTE]
> 有关 NDIS 驱动程序堆栈的详细信息以及显示所有四个 NDIS 驱动程序类型之间关系的关系图，请参阅[NDIS 驱动程序堆栈](ndis-driver-stack.md)。

## <a name="related-topics"></a>相关主题

[NDIS 协议驱动程序](ndis-protocol-drivers.md)

[NDIS 协议驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)