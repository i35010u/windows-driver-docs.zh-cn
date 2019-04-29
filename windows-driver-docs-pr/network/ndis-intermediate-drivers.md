---
title: 中间驱动程序
description: 中间驱动程序
ms.assetid: 0c0516b0-1fc4-43b5-8c7c-58255c72a4e7
keywords:
- 中间驱动程序 WDK 网络体系结构
- NDIS 中间层驱动程序 WDK，体系结构
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9097dfcd64af18584b8668d855724b579683821f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378431"
---
# <a name="intermediate-drivers"></a>中间驱动程序

下图所示，中间驱动程序微型端口驱动程序之间通常分层和传输协议驱动程序。

![说明分层微型端口驱动程序和传输驱动程序之间的中间驱动程序的关系图](images/id-1.png)

> [!NOTE]
> 有关 NDIS 驱动程序堆栈和一个显示所有四个的 NDIS 驱动程序类型之间的关系图的详细信息，请参阅[NDIS 驱动程序堆栈](ndis-driver-stack.md)。

由于在驱动程序层次结构中的中间位置，而中间驱动程序都必须与基础协议驱动程序和基础微型端口驱动程序以便公开通信：

-   协议的入口点。

    在其下边缘调用 NDIS *ProtocolXxx*函数进行通信来自基础微型端口驱动程序的请求。 中间驱动程序看起来像协议驱动程序为基础的微型端口驱动程序。

-   微型端口驱动程序入口点。

    在其上边缘调用 NDIS *MiniportXxx*函数进行通信的一个或多个基础协议驱动程序的请求。 中间驱动程序看起来像微型端口驱动程序与某个基础协议驱动程序。

中间的驱动程序将导出的子集*MiniportXxx*函数在其上边缘。 它还将导出一个或多个虚拟适配器，可以绑定到基础协议驱动程序。 到协议驱动程序，由中间驱动程序导出的虚拟适配器显示为物理 nic。 当协议驱动程序将数据包或请求发送到的虚拟适配器时，中间驱动程序将传播这些数据包并请求到基础微型端口驱动程序。 此类数据包、 响应和最多绑定到的协议驱动程序的状态时的基础的微型端口驱动程序指示接收到的数据包、 响应的协议驱动程序的请求的信息，或指示状态，传播中间驱动程序虚拟适配器。

可以使用中间的驱动程序：

-   不同的网络媒体之间进行转换。

-   平衡数据包传输跨多个 nic。 负载平衡驱动程序公开到过量的传输协议的一个虚拟适配器和发送数据包分布多个 nic。

## <a name="related-topics"></a>相关主题

[中间的 NDIS 驱动程序](ndis-intermediate-drivers2.md)

[NDIS 中间驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff565782)