---
title: 协议驱动程序 OID 请求
description: 协议驱动程序 OID 请求
ms.assetid: ab664e75-d17d-4664-8c37-91fd651d23c2
keywords:
- 协议驱动程序 WDK 网络、 OID 请求
- Oid WDK 网络协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e43b2816eec28b6d76b9ad9cbb3feca4fcd1d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384222"
---
# <a name="protocol-driver-oid-requests"></a>协议驱动程序 OID 请求





NDIS 定义用于标识适配器参数包括操作参数，如设备特征、 可配置的设置和统计信息的对象标识符 (OID) 值。 有关 Oid 的详细信息，请参阅[NDIS Oid](https://msdn.microsoft.com/library/windows/hardware/ff566707)。

协议驱动程序可使用查询或设置操作参数的基础驱动程序。

此外提供了 NDIS [NDIS 6.1 的直接 OID 请求接口](direct-oid-request-interface-in-ndis-6-1.md)和更高版本的协议驱动程序。 *直接 OID 请求路径*支持查询或频繁设置的 OID 请求。 例如，IPsec 卸载版本 2 (IPsecv2) 接口提供了[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812)直接 OID 请求的 OID。 直接 OID 请求接口是可选的 NDIS 驱动程序。

以下主题提供有关协议驱动程序 OID 请求的详细信息：

[正在从 NDIS 协议驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-protocol-driver.md)

[协议驱动程序直接 OID 请求](protocol-driver-direct-oid-requests.md)

[协议驱动程序同步 OID 请求](protocol-driver-synchronous-oid-requests.md)

 

 





