---
title: OID_WWAN_NETWORK_BLACKLIST
description: OID_WWAN_NETWORK_BLACKLIST 获取或设置有关移动宽带（MBB）设备的网络黑名单的信息。
ms.assetid: CD5F0913-73E4-4A04-BB56-76A59D886FF1
ms.date: 08/21/2018
keywords: -从 Windows Vista 开始 OID_WWAN_NETWORK_BLACKLIST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 48948ab939ec6c18e26eea4035f4e1224454290f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916876"
---
# <a name="oid_wwan_network_blacklist"></a>OID_WWAN_NETWORK_BLACKLIST

OID_WWAN_NETWORK_BLACKLIST 获取或设置有关移动宽带（MBB）设备的网络黑名单的信息。

微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送[NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md)状态通知，其中包含描述当前网络黑名单的[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)结构。

对于 Set 请求，此 OID 的负载包含一个[**NDIS_WWAN_SET_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist)结构，该结构指定了调制解调器应忽略的 MNC/MCC 组合的列表。

## <a name="remarks"></a>备注

完成每个查询或设置请求后，微型端口驱动程序应返回[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)结构，其中包含有关当前网络黑名单信息的信息。

有关使用此 OID 的详细信息，请参阅[MBIM_CID_MS_NETWORK_BLACKLIST](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations#mbimcidmsnetworkblacklist)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703**头**： Ntddndis （包括 Ndis .h）

## <a name="see-also"></a>另请参阅

[MB 网络阻止列表操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)

[NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)

[**NDIS_WWAN_SET_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist)
