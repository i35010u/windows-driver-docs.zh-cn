---
title: NDIS MUX 中间驱动程序
description: NDIS MUX 中间驱动程序
keywords:
- MUX 中间驱动程序 WDK
- NDIS MUX 中间驱动程序 WDK
- 单对 n MUX 中间驱动程序配置 WDK
- n 对一 MUX 中间驱动程序配置 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 474120f93e689e917c28f827f52841d5a4b3420b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825067"
---
# <a name="ndis-mux-intermediate-drivers"></a>NDIS MUX 中间驱动程序





MUX 中间驱动程序公开的虚拟微型端口数可能不同于绑定到该驱动程序的较低物理适配器的数目。 MUX 中间驱动程序在一对 *n*、 *n* 对一，甚至是与基础适配器的 *m* 到 *n* 关系中公开虚拟微型端口。 这种不同产生了复杂的内部绑定和数据路径。

在 *一对一配置中* ，单个 MUX 中间驱动程序可以绑定到下面的多个物理适配器。 传输驱动程序绑定到 MUX 中间驱动程序的虚拟小型端口，其方式与它们绑定到非虚拟微型端口的方式相同。 MUX 中间驱动程序重新打包，并向下传递所有请求并发送提交给特定连接的中间驱动程序的数据包。  (LBFO) 驱动程序的负载均衡故障转移是此类型 MUX 中间驱动程序的一个示例。

下图说明了单对 *n* MUX 中间驱动程序配置。

![说明一对一 mux 中间驱动程序配置的示意图](images/1tonmux.png)

在 *n* 对一配置中，MUX 中间驱动程序可以为以下单个物理适配器公开多个虚拟微型端口。 过量协议驱动程序绑定到 MUX 中间驱动程序的这些虚拟微型端口，其方式与它们绑定到非虚拟微型端口的方式相同。 MUX 中间驱动程序处理在每个虚拟小型端口上提交到特定连接的驱动程序的请求和发送。 驱动程序重新打包并传输这些请求，并将其发送到绑定的物理适配器的 NDIS 微型端口驱动程序。

下图说明了一个 *n* 对一 MUX 中间驱动程序配置。

![说明 n 对一 mux 中间驱动程序配置的示意图](images/nto1mux.png)

MUX 中间驱动程序需要通知对象 DLL。 初始化 MUX 中间驱动程序时，其绑定由其通知对象 DLL 建立的配置决定。 有关安装 MUX 中间驱动程序的详细信息，请参阅 [Mux 中间驱动程序安装](mux-intermediate-driver-installation.md)。

以下列表描述了 *n* 对 1 MUX 中间驱动程序的示例：

-   802和专用虚拟 Lan 是可作为与 MUX 示例类似的中间驱动程序实现的技术。

-   MUX 中间驱动程序示例是一个多元 MUX 中间驱动程序。 MUX 在单个基础微型端口适配器之上创建多个虚拟微型端口。

 

 





