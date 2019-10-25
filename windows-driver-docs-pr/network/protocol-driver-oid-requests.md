---
title: 协议驱动程序 OID 请求
description: 协议驱动程序 OID 请求
ms.assetid: ab664e75-d17d-4664-8c37-91fd651d23c2
keywords:
- 协议驱动程序 WDK 网络，OID 请求
- Oid WDK 网络，协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc74ad8034123b3c7a52378eaf073b17f624b27e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844912"
---
# <a name="protocol-driver-oid-requests"></a>协议驱动程序 OID 请求





NDIS 定义对象标识符（OID）值以标识包含操作参数的适配器参数，如设备特征、可配置的设置和统计信息。 有关 Oid 的详细信息，请参阅[NDIS oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

协议驱动程序可以查询或设置基础驱动程序的操作参数。

NDIS 还为 NDIS 6.1 和更高版本的协议驱动程序提供[直接 OID 请求接口](direct-oid-request-interface-in-ndis-6-1.md)。 *直接 OID 请求路径*支持经常查询或设置的 OID 请求。 例如，IPsec 卸载版本2（IPsecv2）接口提供[OID\_TCP\_任务\_IPsec\_卸载\_V2\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)为直接 OID 请求添加\_SA OID。 直接 OID 请求接口对于 NDIS 驱动程序是可选的。

以下主题提供了有关协议驱动程序 OID 请求的详细信息：

[从 NDIS 协议驱动程序生成 OID 请求](generating-oid-requests-from-an-ndis-protocol-driver.md)

[协议驱动程序直接 OID 请求](protocol-driver-direct-oid-requests.md)

[协议驱动程序同步 OID 请求](protocol-driver-synchronous-oid-requests.md)

 

 





