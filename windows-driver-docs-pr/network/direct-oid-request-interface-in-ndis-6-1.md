---
title: NDIS 6.1 中的直接 OID 请求接口
description: NDIS 6.1 中的直接 OID 请求接口
ms.assetid: 1a24dec6-f16a-45f5-857b-c6e0df4ce261
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 925ce2225b19e0b3c22d72ebf992bf19da9a4804
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379574"
---
# <a name="direct-oid-request-interface-in-ndis-61"></a>NDIS 6.1 中的直接 OID 请求接口





NDIS NDIS 6.1 和更高版本的驱动程序提供直接的 OID 请求接口。 *直接 OID 请求路径*支持查询或频繁设置的 OID 请求。 例如，IPsec 卸载版本 2 (IPsecOV2) 接口提供了[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812)直接 OID 请求的 OID。

直接 OID 请求接口是可选的 NDIS 驱动程序。 若要支持直接的 OID 路径，驱动程序提供入口点，并提供 NDIS **Ndis * Xxx*** 的协议、 筛选和微型端口驱动程序函数。

**请注意**  NDIS 支持特定 Oid 与 direct 的 OID 请求接口一起使用。 若要确定您的驱动程序是否可以直接 Oid 界面中使用 OID，请参阅 OID 引用页中的说明。

 

对于 NDIS 6.1，使用直接的 OID 请求接口的唯一接口是 IPsecOV2。 有关 IPsecOV2 详细信息，请参阅[IPsec 任务卸载版本 2 中 NDIS 6.1](ipsec-task-offload-version-2-in-ndis-6-1.md)。

有关 NDIS 6.1 驱动程序中的 Windows Server 2008 和 Windows Vista Service Pack 1 (SP1) 操作系统，可以使用与直接 OID 请求接口仅以下 Oid:

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569813)

-   [OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_UPDATE\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569814)

微型端口驱动程序和筛选器驱动程序必须能够处理不会序列化的直接 OID 请求。 与标准的 OID 请求接口，不同 NDIS 不序列化与使用直接的 OID 接口或使用标准的 OID 请求接口发送其他请求直接 OID 请求。 此外，微型端口驱动程序和筛选器驱动程序必须能够处理直接 OID 请求在 IRQL &lt;= 调度\_级别。

有关如何在驱动程序中实现直接 OID 接口的详细信息，请参阅以下主题：

-   [微型端口适配器 OID 请求](miniport-adapter-oid-requests.md)

-   [协议驱动程序 OID 请求](protocol-driver-oid-requests.md)

-   [筛选模块 OID 请求](filter-module-oid-requests.md)

 

 





