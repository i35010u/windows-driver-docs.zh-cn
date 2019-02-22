---
title: NDIS MUX 中间驱动程序
description: NDIS MUX 中间驱动程序
ms.assetid: 2c2e0af8-aa33-47fb-8605-26eae184ea22
keywords:
- MUX 中间驱动程序 WDK
- NDIS MUX 中间驱动程序 WDK
- 一个 n MUX 中间驱动程序配置 WDK
- n 对一 MUX 中间驱动程序配置 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2538c3552d783d85c0712100af6eafee97e3d58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547672"
---
# <a name="ndis-mux-intermediate-drivers"></a>NDIS MUX 中间驱动程序





公开的 MUX 中间驱动程序的虚拟微型端口数可为不同于绑定到该驱动程序的较低物理适配器的数量。 MUX 中间驱动程序显示在一个虚拟微型端口-到-*n*， *n*-到-一个，或甚至*m*到*n*与关系适配器的基础。 这样的多样性会导致复杂的内部绑定和数据路径。

在一个-到-*n*配置中，单个 MUX 中间驱动程序可以绑定到下面的许多物理适配器。 传输驱动程序将绑定到 MUX 中间驱动程序的虚拟微型端口一样，它们将绑定到非虚拟微型端口。 MUX 中间驱动程序会重新打包和向下的所有请求将传递，将提交的数据包发送到中间驱动程序特定的连接。 负载平衡故障转移 (LBFO) 驱动程序是这种类型的 MUX 中间驱动程序的示例。

下图演示了一个-到-*n* MUX 中间驱动程序配置。

![说明一个 n mux 中间驱动程序配置的关系图](images/1tonmux.png)

在中*n*-到-一种配置 MUX 中间驱动程序可以公开为下面的单个物理适配器的许多虚拟微型端口。 基础协议驱动程序绑定到 MUX 中间驱动程序这些虚拟微型端口中其绑定到非虚拟微型端口的相同方法。 MUX 中间驱动程序处理请求，并将发送到的特定连接在每个虚拟微型端口驱动程序提交。 该驱动程序会重新打包并传输这些请求和向下发送到绑定的物理适配器的 NDIS 微型端口驱动程序。

下图演示了*n*-到-MUX 中间驱动程序的一种配置。

![说明 n 对一 mux 中间驱动程序配置的关系图](images/nto1mux.png)

MUX 中间驱动程序需要通知对象 DLL。 初始化 MUX 中间驱动程序时，其绑定由其通知对象 DLL 所建立的配置决定。 有关安装 MUX 中间驱动程序的详细信息，请参阅[MUX 中间驱动程序安装](mux-intermediate-driver-installation.md)。

以下列表描述了的示例*n*-到-一个 MUX 中间驱动程序：

-   802 和专有的虚拟 Lan 是就可以实现为中间驱动程序的 MUX 示例类似的技术。

-   MUX 中间驱动程序示例是 n 对一 MUX 中间驱动程序。 MUX 创建多个虚拟微型端口上的单个基础的微型端口适配器分层。

 

 





