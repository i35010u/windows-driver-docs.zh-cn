---
title: 将 NDIS 6.20 更新到 NDIS 6.1 的功能
description: 将 NDIS 6.20 更新到 NDIS 6.1 的功能
ms.assetid: b57af71b-2718-4a52-888b-b378b3e6097f
keywords:
- NDIS 6.20 WDK，对 NDIS 6.1 功能的更新
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c064c59190ac02018ec63192c3932a072aea22cc
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716709"
---
# <a name="ndis-620-updates-to-ndis-61-features"></a>将 NDIS 6.20 更新到 NDIS 6.1 的功能





NDIS 6.1 将以下接口添加到 NDIS 6.0：

[标头数据拆分](header-data-split-in-ndis-6-1.md)

[直接 OID 请求](direct-oid-request-interface-in-ndis-6-1.md)

[IPsec 任务卸载版本2](ipsec-task-offload-version-2-in-ndis-6-1.md)

[NetDMA 1.1 和2。0](netdma-updates-in-ndis-6-1.md)

有关 NDIS 6.1 的详细信息，请参阅 [ndis 6.1 简介](introduction-to-ndis-6-1.md)。

NDIS 6.1 还包括用于支持用于接收方缩放 (RSS) 的 MSI X 动态配置的更新。 有关 RSS 中的 NDIS 6.1 更改的详细信息，请参阅 [NDIS MSI-X](ndis-msi-x.md)。 在 NDIS 6.20 中更新 RSS，为超过64个处理器提供支持。

[直接 OID 请求接口](direct-oid-request-interface-in-ndis-6-1.md)对于 ndis 6.1 驱动程序是可选的，但对于 ndis 6.20 微型端口驱动程序是必需的。

将不支持 NDIS 6.20 [IPsec 任务卸载版本 1](background-reading-on-ipsec.md) 。 应更新支持 IPsec 任务卸载的所有驱动程序，以支持 [ipsec 任务卸载版本 2](./introduction-to-ipsec-offload-version-2.md)。

NetDMA 1.1 和2.0 随 NDIS 6.1 一起引入。 NetDMA 2.1 与 NDIS 6.20 一起引入，为超过64个处理器提供支持。

 

