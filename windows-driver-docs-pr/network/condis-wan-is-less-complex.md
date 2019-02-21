---
title: WAN 的 CoNDIS 是不太复杂
description: WAN 的 CoNDIS 是不太复杂
ms.assetid: 750f321a-72c9-4d90-b02e-cbe5177dc2af
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络权益
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15d060329cdcc7d3166b6196f7c62cada81f8ea8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542758"
---
# <a name="condis-wan-is-less-complex"></a>WAN 的 CoNDIS 是不太复杂





CoNDIS 到每个连接中涉及的逻辑实体定义相对应的对象。 这些实体包括地址系列 (AFs)、 虚拟连接 (VCs)、 服务访问点 (SAPs) 和参与方。

在的 CoNDIS 环境中，系统将处理的许多复杂的 TAPI 要求。 因此，CoNDIS WAN 微型端口驱动程序或 MCM 无需处理任意数量的 TAPI Oid 为 NDIS WAN 的微型端口驱动程序。 此外，CoNDIS WAN 微型端口驱动程序或 MCM 不需要处理以下状态指示：

-   NDIS\_状态\_TAPI\_指示

-   NDIS\_状态\_WAN\_行\_向上

-   NDIS\_状态\_WAN\_行\_下

呼叫管理器和微型端口驱动程序函数的分离，可实现两个简单的驱动程序。 简化驱动程序应易于维护和调试比一个大型和复杂的驱动程序。

 

 





