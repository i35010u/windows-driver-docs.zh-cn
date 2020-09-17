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
ms.openlocfilehash: 7e115970c478ce4d618da46fc303658fb9b3bad3
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716322"
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
    -   计算机重新启动时， *IfIndex*值不会持久保存。
    -   [**NET \_ LUID**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh)值与*IfIndex*值之间存在一对一的对应关系。
-   接口索引、NET \_ LUID 值和 "友好名称" 之间的映射 (例如，) 的 "网络连接" 文件夹中显示的友好名称。

-   定义驱动程序堆栈中接口的分层顺序。

-   查询并设置 NDIS 驱动程序管理的接口属性和表，以及 Rfc 2863 和2864指定的表。

 

