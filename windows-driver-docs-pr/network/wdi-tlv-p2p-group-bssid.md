---
title: WDI_TLV_P2P_GROUP_BSSID
description: WDI_TLV_P2P_GROUP_BSSID 是包含本地 Wi-fi Direct 中转的组 BSSID 的 TLV。
ms.assetid: C9BC2209-DF72-4775-A3B5-EC37D404CFED
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GROUP_BSSID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6e7209753e3e4e62ffe6c4e1d7cd8e7b23a50efe
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209567"
---
# <a name="wdi_tlv_p2p_group_bssid"></a>WDI \_ TLV \_ P2P \_ 组 \_ BSSID


WDI \_ tlv \_ P2P \_ 组 \_ BSSID 是包含本地 Wi-fi DIRECT 中转的组 BSSID 的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x73

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型                                              | 说明                                          |
|---------------------------------------------------|------------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 为本地 Wi-fi Direct 中转指定组 BSSID。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

