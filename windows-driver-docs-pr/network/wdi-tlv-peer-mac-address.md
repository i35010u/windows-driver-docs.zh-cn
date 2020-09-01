---
title: WDI_TLV_PEER_MAC_ADDRESS
description: WDI_TLV_PEER_MAC_ADDRESS 是包含对等方的 MAC 地址的 TLV。
ms.assetid: A936BAA6-96AD-4187-9933-FA02CCFED2AE
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PEER_MAC_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 26e07960b9128b070fe5fe965810ad3baf112ca6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210035"
---
# <a name="wdi_tlv_peer_mac_address"></a>WDI \_ TLV \_ 对等 \_ MAC \_ 地址


WDI \_ tlv \_ 对等 \_ MAC \_ 地址是包含对等节点的 MAC 地址的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x4C

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型                                              | 说明                                  |
|---------------------------------------------------|----------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定对等节点的 Wi-fi MAC 地址。 |

 

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

 

