---
title: NDIS 6.20 到 NDIS 6.1 功能更新
description: NDIS 6.20 到 NDIS 6.1 功能更新
ms.assetid: b57af71b-2718-4a52-888b-b378b3e6097f
keywords:
- NDIS 6.20 WDK、 NDIS 6.1 功能更新
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d123910b9c304c406e794049209f299c4bab072
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548067"
---
# <a name="ndis-620-updates-to-ndis-61-features"></a>NDIS 6.20 到 NDIS 6.1 功能更新





NDIS 6.1 添加到 NDIS 6.0 以下接口：

[标头数据拆分](header-data-split-in-ndis-6-1.md)

[直接 OID 请求](direct-oid-request-interface-in-ndis-6-1.md)

[IPsec 任务卸载版本 2](ipsec-task-offload-version-2-in-ndis-6-1.md)

[NetDMA 1.1 和 2.0](netdma-updates-in-ndis-6-1.md)

有关 NDIS 6.1 的详细信息，请参阅[简介 NDIS 6.1](introduction-to-ndis-6-1.md)。

NDIS 6.1 还包括更新以支持 MSI X 动态配置的接收方缩放 (RSS)。 有关 RSS 的 NDIS 6.1 更改的详细信息，请参阅[NDIS MSI-X](ndis-msi-x.md)。 RSS NDIS 6.20 提供支持多个 64 位处理器中更新。

[直接 OID 请求接口](direct-oid-request-interface-in-ndis-6-1.md)是可选的 NDIS 6.1 驱动程序，但它是必需的 NDIS 6.20 微型端口驱动程序。

在 NDIS 6.20 [IPsec 任务卸载版本 1](ipsec-offload-version-1.md)不受支持。 支持 IPsec 任务卸载的所有驱动程序应更新为支持[IPsec 任务卸载版本 2](ipsec-offload-version-2.md)。

NetDMA 1.1 和 2.0 引入了 NDIS 6.1。 NetDMA 2.1 引入了 NDIS 6.20 为 64 个以上处理器提供支持。

 

 





