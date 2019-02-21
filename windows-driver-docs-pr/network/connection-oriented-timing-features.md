---
title: 面向连接的计时功能
description: 面向连接的计时功能
ms.assetid: 73b005c2-39bd-4931-89cd-7ea3db9068ca
keywords:
- 面向连接的 NDIS WDK，计时功能
- CoNDIS WDK 连接网络、 计时功能
- 计时功能 WDK 的 CoNDIS
- 时钟
- 本地时钟 WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47ac08445814538a95675b783e2926b0fb9fc9e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519454"
---
# <a name="connection-oriented-timing-features"></a>面向连接的计时功能





面向连接的 NDIS 支持使用 NIC 的本地时间来安排数据包的传输以及时间戳发送和接收数据包。

**请注意**  这些面向连接的计时功能是可选的。 所有的 CoNDIS Nic 不支持这些功能。

 

面向连接的协议驱动程序可以调用[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)若要查询的面向连接的微型端口驱动程序或与 MCM 驱动程序的本地计时功能[OID\_GEN\_CO\_获取\_时间\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569451)。 此类查询响应，微型端口驱动程序或 MCM 驱动程序将返回有关信息：

-   NIC 是否存在可读的时钟

-   是否 NIC 派生自其时间的网络连接。

-   本地时钟的精度。

-   NIC 是否可以时间戳收到数据包的其本地时间。

-   是否 NIC 可以计划按照其本地时间的传输发送数据包。

-   NIC 是否可以时间戳传输数据包的其本地时间。

若要获取 NIC 的本地时间，面向连接的协议可以调用**NdisCoOidRequest**若要查询的面向连接的微型端口驱动程序或与 MCM 驱动程序[OID\_常规\_CO\_获取\_网卡\_时间](https://msdn.microsoft.com/library/windows/hardware/ff569450)。 面向连接的微型端口驱动程序或 MCM 驱动程序以同步方式返回其本地时间，然后可以使用面向连接的协议计划数据包的传输。

计时信息对要发送或接收数据包的带外 (OOB) 数据中包含的数据包。 有关详细信息，请参阅[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)。

 

 





