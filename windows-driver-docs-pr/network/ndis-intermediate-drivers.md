---
title: 中间驱动程序
description: 中间驱动程序
ms.assetid: 0c0516b0-1fc4-43b5-8c7c-58255c72a4e7
keywords:
- 中间驱动程序 WDK 网络，体系结构
- NDIS 中间驱动程序 WDK，体系结构
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7a563b1acb7f9ce635d63cd633483f4b9845c0a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843544"
---
# <a name="intermediate-drivers"></a>中间驱动程序

如下图所示，中间驱动程序通常在微型端口驱动程序和传输协议驱动程序之间进行分层。

![说明小型端口驱动程序和传输驱动程序之间的中间驱动程序的示意图](images/id-1.png)

> [!NOTE]
> 有关 NDIS 驱动程序堆栈的详细信息以及显示所有四个 NDIS 驱动程序类型之间关系的关系图，请参阅[NDIS 驱动程序堆栈](ndis-driver-stack.md)。

由于其在驱动程序层次结构中的中间位置，中间驱动程序必须与过量协议驱动程序和基础微型端口驱动程序通信，才能公开：

-   协议入口点。

    在其下边缘，NDIS 调用*ProtocolXxx*函数，以从基础微型端口驱动程序传递请求。 中间驱动程序看起来像是基础微型端口驱动程序的协议驱动程序。

-   微型端口驱动程序入口点。

    在其上边缘，NDIS 调用*MiniportXxx*函数，以便与一个或多个过量协议驱动程序的请求进行通信。 中间驱动程序看起来像是过量协议驱动程序的微型端口驱动程序。

中间驱动程序将*MiniportXxx*函数的子集导出到其上边缘。 它还会导出过量协议驱动程序可以绑定到的一个或多个虚拟适配器。 对于协议驱动程序，中间驱动程序导出的虚拟适配器似乎是物理 NIC。 当协议驱动程序将数据包或请求发送到虚拟适配器时，中间驱动程序会将这些数据包和请求传播到基础微型端口驱动程序。 当基础微型端口驱动程序指示收到的数据包时，会响应协议驱动程序的信息请求，或指示状态，中间驱动程序将此类数据包、响应和状态传播到绑定到的协议驱动程序虚拟适配器。

可以使用中间驱动程序执行以下操作：

-   在不同的网络媒体之间转换。

-   跨多个 NIC 平衡数据包传输。 负载平衡驱动程序将一个虚拟适配器公开给过量传输协议，并在多个 NIC 之间分发发送数据包。

## <a name="related-topics"></a>相关主题

[NDIS 中间驱动程序](ndis-intermediate-drivers2.md)

[NDIS 中间驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)