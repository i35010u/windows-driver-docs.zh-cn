---
title: NDIS 6.1 中的直接 OID 请求接口
description: NDIS 6.1 中的直接 OID 请求接口
ms.assetid: 1a24dec6-f16a-45f5-857b-c6e0df4ce261
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f2a58bc5e86c1c361cabc4f940208fe273f5070
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217646"
---
# <a name="direct-oid-request-interface-in-ndis-61"></a>NDIS 6.1 中的直接 OID 请求接口





NDIS 为 NDIS 6.1 和更高版本的驱动程序提供直接 OID 请求接口。 *直接 OID 请求路径*支持经常查询或设置的 OID 请求。 例如，IPsec 卸载版本 2 (IPsecOV2) 接口为 [OID \_ TCP \_ 任务 \_ IPsec \_ 卸载 \_ V2 \_ 添加 \_ ](./oid-tcp-task-ipsec-offload-v2-add-sa.md) 了用于直接 OID 请求的 SA OID。

直接 OID 请求接口对于 NDIS 驱动程序是可选的。 为了支持直接 OID 路径，驱动程序提供入口点，NDIS 为协议、筛选器和微型端口驱动程序提供 **ndis * Xxx*** 函数。

**注意**   NDIS 支持用于直接 OID 请求接口的特定 Oid。 若要确定驱动程序是否可以在直接 Oid 接口中使用 OID，请参阅 "OID 引用" 页中的说明。

 

对于 NDIS 6.1，使用直接 OID 请求接口的唯一接口为 IPsecOV2。 有关 IPsecOV2 的详细信息，请参阅 [NDIS 6.1 中的 IPsec 任务卸载版本 2](ipsec-task-offload-version-2-in-ndis-6-1.md)。

对于带有 Service Pack 1 (SP1) 操作系统的 Windows Server 2008 和 Windows Vista 中的 NDIS 6.1 驱动程序，只能在直接 OID 请求接口中使用以下 Oid：

-   [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA](./oid-tcp-task-ipsec-offload-v2-add-sa.md)

-   [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ DELETE \_ SA](./oid-tcp-task-ipsec-offload-v2-delete-sa.md)

-   [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 更新 \_ SA](./oid-tcp-task-ipsec-offload-v2-update-sa.md)

微型端口驱动程序和筛选器驱动程序必须能够处理未序列化的直接 OID 请求。 与标准 OID 请求接口不同，NDIS 不会将直接 OID 请求与通过直接 OID 接口或标准 OID 请求接口发送的其他请求进行序列化。 此外，微型端口驱动程序和筛选器驱动程序必须能够以 IRQL = 调度级别处理直接 OID 请求 &lt; \_ 。

有关如何在驱动程序中实现直接 OID 接口的详细信息，请参阅以下主题：

-   [微型端口适配器 OID 请求](miniport-adapter-oid-requests.md)

-   [协议驱动程序 OID 请求](protocol-driver-oid-requests.md)

-   [筛选器模块 OID 请求](filter-module-oid-requests.md)

 

