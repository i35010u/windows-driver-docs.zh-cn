---
title: NDIS 网络接口服务
description: NDIS 网络接口服务
keywords:
- NDIS 网络接口 WDK，服务
- 网络接口 WDK，服务
- 服务 WDK 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56f9125cb8c76560fe02a71f03101e95437ff47b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801569"
---
# <a name="ndis-network-interface-services"></a>NDIS 网络接口服务





NDIS 网络接口编程接口提供以下服务：

-   为每个接口 ( [**NET \_ LUID**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh)) 生成本地唯一标识符。 NET \_ LUID 值：
    -   计算机重新启动时必须保留。 \_即使关联的接口不是永久性的，接口提供程序也必须使 NET luid 持久。 例如，如果存在计算机电源故障，则此永久性允许接口提供程序释放 NET \_ LUID 索引。
    -   必须与 RFC 2863) 中 ( *IfType* 的接口类型相关联。
    -   在本地计算机上必须唯一。
    -   由于 NET \_ LUID 等效于 RFC 2863) 中 (*ifName* 的接口名称，因此可转换为文本表示形式。
-    (一个24位值生成本地唯一接口索引，每个接口也称为 *IfIndex* ) 。 *IfIndex* 值具有以下属性：
    -   优先级较低。 例如，NDIS 重用最低可用的接口索引。
    -   计算机重新启动时， *IfIndex* 值不会持久保存。
    -   [**NET \_ LUID**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh)值与 *IfIndex* 值之间存在一对一的对应关系。
-   接口索引、NET \_ LUID 值和 "友好名称" 之间的映射 (例如，) 的 "网络连接" 文件夹中显示的友好名称。

-   定义驱动程序堆栈中接口的分层顺序。

-   查询并设置 NDIS 驱动程序管理的接口属性和表，以及 Rfc 2863 和2864指定的表。

 

