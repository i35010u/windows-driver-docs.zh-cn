---
title: NDIS_STATUS_WWAN_NETWORK_BLACKLIST
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_NETWORK_BLACKLIST 通知来通知关于完成的上一个 OID_WWAN_NETWORK_BLACKLIST 查询或一组请求的移动宽带 (MB) 服务。
ms.assetid: 38ED7C51-D352-4B48-BF80-433A7C4642AB
ms.date: 08/21/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_NETWORK_BLACKLIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c1b00724a44e8af2514d54a4d8d9c0104a51771f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555941"
---
# <a name="ndisstatuswwannetworkblacklist"></a>NDIS_STATUS_WWAN_NETWORK_BLACKLIST

微型端口驱动程序使用**NDIS_STATUS_WWAN_NETWORK_BLACKLIST**通知来通知关于完成的上一次移动宽带 (MB) 服务[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)查询或设置请求。

如果任何方块列表状态已更改从启动以不启动、 发送未经请求的事件，反之亦然。 例如，如果 SIM 将插入的提供程序与 SIM 提供程序方块列表匹配。

使用此通知[ **NDIS_WWAN_NETWORK_BLACKLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1703 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>另请参阅

[MB 网络方块列表操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)

[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)
