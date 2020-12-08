---
title: CoNDIS WAN 更简单
description: CoNDIS WAN 更简单
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，优点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc4e483389fcfe46dae734e171f58a30c8a55df3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840663"
---
# <a name="condis-wan-is-less-complex"></a>CoNDIS WAN 更简单





CoNDIS 定义与连接中所涉及的每个逻辑实体对应的对象。 这些实体包括 (AFs) 的地址系列、 (VCs) 的虚拟连接、服务访问点 (Sap) 和参与方。

在 CoNDIS 环境中，系统会处理许多复杂的 TAPI 需求。 因此，CoNDIS WAN 微型端口驱动程序或 MCM 无需处理任意数量的 TAPI Oid 作为 NDIS WAN 微型端口驱动程序。 此外，CoNDIS WAN 微型端口驱动程序或 MCM 不需要处理以下状态指示：

-   NDIS \_ 状态 \_ TAPI \_ 指示

-   NDIS \_ 状态 \_ WAN \_ \_ 向上排列

-   NDIS \_ 状态 \_ 广域网 \_ 行 \_

通过分离调用管理器和微型端口驱动程序功能，您可以实现两个简单的驱动程序。 简化的驱动程序应比一个大型和复杂的驱动程序更容易维护和调试。

 

 





