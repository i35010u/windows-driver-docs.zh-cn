---
title: NDIS 网络接口服务
description: NDIS 网络接口服务
ms.assetid: c37d9b7e-bc56-41e6-b41f-92a6df890e8e
keywords:
- NDIS 网络接口 WDK，服务
- 网络接口 WDK，服务
- 服务 WDK 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e26685fab844eff6166a4884f9ae3bdf07f2d29d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568671"
---
# <a name="ndis-network-interface-services"></a>NDIS 网络接口服务





NDIS 网络的接口的编程接口提供的服务：

-   生成的本地唯一标识符 ( [ **NET\_LUID**](https://msdn.microsoft.com/library/windows/hardware/ff568747)) 为每个接口。 NET\_LUID 值：
    -   必须保留在计算机重新启动时。 接口提供程序必须进行 NET\_持久，即使关联的接口不是永久的 Luid。 例如，此持久性可让接口提供程序，以释放 NET\_LUID 索引计算机电源故障时。
    -   必须与接口类型相关联 ( *IfType*在 RFC 2863)。
    -   必须是本地计算机上唯一的。
    -   可以将转换为文本表示形式，因为 NET\_LUID 相当于接口名称 (*ifName*在 RFC 2863)。
-   生成的本地唯一的接口索引 (一个 24 位值，也称为*IfIndex* ) 为每个接口。 *IfIndex*值具有以下属性：
    -   较低的数值是首选。 例如，NDIS 重复使用的最小可用接口索引。
    -   *IfIndex*计算机重新启动时不会保留值。
    -   没有之间的一一对应关系[ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)值和一个*IfIndex*值。
-   接口索引，NET 之间的映射\_LUID 值和"友好名称"（例如，为显示网络连接文件夹中的友好名称）。

-   在驱动程序堆栈中定义接口的分层顺序。

-   查询和设置接口属性和 NDIS 驱动程序管理，并且该 Rfc 2863 和 2864年指定表。

 

 





