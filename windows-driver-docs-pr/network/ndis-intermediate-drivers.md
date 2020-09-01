---
title: 中间驱动程序
description: 中间驱动程序
ms.assetid: 0c0516b0-1fc4-43b5-8c7c-58255c72a4e7
keywords:
- 中间驱动程序 WDK 网络，体系结构
- NDIS 中间驱动程序 WDK，体系结构
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 954df9ac5b164fbbb1c90c4a97cbbb6f0057d889
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207461"
---
# <a name="intermediate-drivers"></a>中间驱动程序

如下图所示，中间驱动程序通常在微型端口驱动程序和传输协议驱动程序之间进行分层。

![说明小型端口驱动程序和传输驱动程序之间的中间驱动程序的示意图](images/id-1.png)

> [!NOTE]
> 有关 NDIS 驱动程序堆栈的详细信息以及显示所有四个 NDIS 驱动程序类型之间关系的关系图，请参阅 [NDIS 驱动程序堆栈](ndis-driver-stack.md)。

由于其在驱动程序层次结构中的中间位置，中间驱动程序必须与过量协议驱动程序和基础微型端口驱动程序通信，才能公开：

-   协议入口点。

    在其下边缘，NDIS 调用 *ProtocolXxx* 函数，以从基础微型端口驱动程序传递请求。 中间驱动程序看起来像是基础微型端口驱动程序的协议驱动程序。

-   微型端口驱动程序入口点。

    在其上边缘，NDIS 调用 *MiniportXxx* 函数，以便与一个或多个过量协议驱动程序的请求进行通信。 中间驱动程序看起来像是过量协议驱动程序的微型端口驱动程序。

中间驱动程序将 *MiniportXxx* 函数的子集导出到其上边缘。 它还会导出过量协议驱动程序可以绑定到的一个或多个虚拟适配器。 对于协议驱动程序，中间驱动程序导出的虚拟适配器似乎是物理 NIC。 当协议驱动程序将数据包或请求发送到虚拟适配器时，中间驱动程序会将这些数据包和请求传播到基础微型端口驱动程序。 当基础微型端口驱动程序指示收到的数据包时，响应协议驱动程序的信息请求，或指示状态，中间驱动程序将此类数据包、响应和状态传播到绑定到虚拟适配器的协议驱动程序。

可以使用中间驱动程序执行以下操作：

-   在不同的网络媒体之间转换。

-   跨多个 NIC 平衡数据包传输。 负载平衡驱动程序将一个虚拟适配器公开给过量传输协议，并在多个 NIC 之间分发发送数据包。

## <a name="related-topics"></a>相关主题

[NDIS 中间驱动程序](ndis-intermediate-drivers2.md)

[NDIS 中间驱动程序参考](/windows-hardware/drivers/ddi/_netvista/)