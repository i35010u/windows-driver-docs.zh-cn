---
title: OID_WWAN_NETWORK_BLACKLIST
description: OID_WWAN_NETWORK_BLACKLIST 获取或设置有关移动宽带 (MBB) 设备的网络黑名单的信息。
ms.assetid: CD5F0913-73E4-4A04-BB56-76A59D886FF1
ms.date: 08/21/2018
keywords: -从 Windows Vista 开始 OID_WWAN_NETWORK_BLACKLIST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c8a406adf09eb3e1000322f29694f4070856a49c
ms.sourcegitcommit: 29c2e6dd8a3de3c11822d990adf1edd774f8a136
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91230007"
---
# <a name="oid_wwan_network_blacklist"></a>OID_WWAN_NETWORK_BLACKLIST

> [!IMPORTANT]
> ### <a name="bias-free-communication"></a>无偏差通信
>
> Microsoft 支持各种不同的环境。 本文介绍了 Microsoft [风格的无偏差通信的 Microsoft 风格指南](/style-guide/bias-free-communication) 的术语参考。 本文中使用的词或短语的一致性是因为它当前出现在软件中。 当软件更新为删除语言时，本文将更新为对齐。

OID_WWAN_NETWORK_BLACKLIST 获取或设置有关移动宽带 (MBB) 设备的网络黑名单的信息。

微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送 [NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md) 状态通知，其中包含描述当前网络黑名单的 [**NDIS_WWAN_NETWORK_BLACKLIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist) 结构。

对于 Set 请求，此 OID 的负载包含一个 [**NDIS_WWAN_SET_NETWORK_BLACKLIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist) 结构，该结构指定了调制解调器应忽略的 MNC/MCC 组合的列表。

## <a name="remarks"></a>备注

完成每个查询或设置请求后，微型端口驱动程序应返回 [**NDIS_WWAN_NETWORK_BLACKLIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist) 结构，其中包含有关当前网络黑名单信息的信息。

有关使用此 OID 的详细信息，请参阅 [MBIM_CID_MS_NETWORK_BLACKLIST](./mb-network-blacklist-operations.md#mbim_cid_ms_network_blacklist)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[MB 网络阻止列表操作](./mb-network-blacklist-operations.md)

[NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)

[**NDIS_WWAN_SET_NETWORK_BLACKLIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist)