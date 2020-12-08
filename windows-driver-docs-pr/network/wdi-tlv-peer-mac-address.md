---
title: WDI_TLV_PEER_MAC_ADDRESS
description: WDI_TLV_PEER_MAC_ADDRESS 是包含对等方的 MAC 地址的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PEER_MAC_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 37dbb35fb43ea2c929c1b0b83320dbdceb3dd4e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818107"
---
# <a name="wdi_tlv_peer_mac_address"></a>WDI \_ TLV \_ 对等 \_ MAC \_ 地址


WDI \_ tlv \_ 对等 \_ MAC \_ 地址是包含对等节点的 MAC 地址的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x4C

## <a name="length"></a>长度


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型                                              | 描述                                  |
|---------------------------------------------------|----------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定对等方的 Wi-Fi MAC 地址。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

