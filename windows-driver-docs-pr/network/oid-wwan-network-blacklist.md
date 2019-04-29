---
title: OID_WWAN_NETWORK_BLACKLIST
description: OID_WWAN_NETWORK_BLACKLIST 获取或设置用于移动宽带 (MBB) 设备的网络阻止列表有关的信息。
ms.assetid: CD5F0913-73E4-4A04-BB56-76A59D886FF1
ms.date: 08/21/2018
keywords: -从 Windows Vista 开始 OID_WWAN_NETWORK_BLACKLIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9ae817b68faf7a4366dd3c49f97bf88ef21ed171
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353715"
---
# <a name="oidwwannetworkblacklist"></a>OID_WWAN_NETWORK_BLACKLIST

OID_WWAN_NETWORK_BLACKLIST 获取或设置用于移动宽带 (MBB) 设备的网络阻止列表有关的信息。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS_STATUS_INDICATION_REQUIRED 到原始请求更高版本发送前[NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md)状态通知包含[ **NDIS_WWAN_NETWORK_BLACKLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)结构，描述当前网络阻止列表。

对于组的请求，此 OID 负载包含[ **NDIS_WWAN_SET_NETWORK_BLACKLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist)结构，它指定应忽略调制解调器的 mnc 是否/MCC 组合的列表。

## <a name="remarks"></a>备注

每个查询或一组请求后，微型端口驱动程序应返回[ **NDIS_WWAN_NETWORK_BLACKLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)结构，其中包含有关当前网络方块列表信息的信息。

有关此 OID 的使用情况的详细信息，请参阅[MBIM_CID_MS_NETWORK_BLACKLIST](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations#mbimcidmsnetworkblacklist)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10 版本 1703 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB 网络方块列表操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)

[NDIS_STATUS_WWAN_NETWORK_BLACKLIST](ndis-status-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)

[**NDIS_WWAN_SET_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_network_blacklist)
