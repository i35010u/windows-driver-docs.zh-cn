---
title: NDIS_STATUS_WWAN_NETWORK_BLACKLIST
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_NETWORK_BLACKLIST 通知来通知移动宽带（MB）服务完成了上一个 OID_WWAN_NETWORK_BLACKLIST 查询或设置请求。
ms.assetid: 38ED7C51-D352-4B48-BF80-433A7C4642AB
ms.date: 08/21/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_NETWORK_BLACKLIST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b326d8c5e592843399b316b67f6982dc4928c8c7
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916656"
---
# <a name="ndis_status_wwan_network_blacklist"></a>NDIS_STATUS_WWAN_NETWORK_BLACKLIST

微型端口驱动程序使用**NDIS_STATUS_WWAN_NETWORK_BLACKLIST**通知来通知移动宽带（MB）服务完成了上一个[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)查询或设置请求。

如果任何黑名单状态已从 "开始" 改为 "未开始"，则发送未经请求的事件，反之亦然。 例如，如果插入的 SIM 与 SIM 提供程序黑名单匹配，则为。

此通知使用[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703**头**： Ntddndis （包括 Ndis .h）

## <a name="see-also"></a>另请参阅

[MB 网络阻止列表操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)

[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)
