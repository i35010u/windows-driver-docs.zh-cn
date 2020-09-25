---
title: NDIS_STATUS_WWAN_NETWORK_BLACKLIST
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_NETWORK_BLACKLIST 通知来通知移动宽带 (MB) 服务与先前 OID_WWAN_NETWORK_BLACKLIST 查询或设置请求的完成有关。
ms.assetid: 38ED7C51-D352-4B48-BF80-433A7C4642AB
ms.date: 08/21/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_NETWORK_BLACKLIST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0389ceb502c5b1ed6a577c35d72ef394b2cb379e
ms.sourcegitcommit: 29c2e6dd8a3de3c11822d990adf1edd774f8a136
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91230019"
---
# <a name="ndis_status_wwan_network_blacklist"></a>NDIS_STATUS_WWAN_NETWORK_BLACKLIST

> [!IMPORTANT]
> ### <a name="bias-free-communication"></a>无偏差通信
>
> Microsoft 支持各种不同的环境。 本文介绍了 Microsoft [风格的无偏差通信的 Microsoft 风格指南](/style-guide/bias-free-communication) 的术语参考。 本文中使用的词或短语的一致性是因为它当前出现在软件中。 当软件更新为删除语言时，本文将更新为对齐。

微型端口驱动程序使用 **NDIS_STATUS_WWAN_NETWORK_BLACKLIST** 通知来通知移动宽带 (MB) 服务与先前 [OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md) 查询或设置请求的完成有关。

如果任何黑名单状态已从 "开始" 改为 "未开始"，则发送未经请求的事件，反之亦然。 例如，如果插入的 SIM 与 SIM 提供程序黑名单匹配，则为。

此通知使用 [**NDIS_WWAN_NETWORK_BLACKLIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[MB 网络阻止列表操作](./mb-network-blacklist-operations.md)

[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)