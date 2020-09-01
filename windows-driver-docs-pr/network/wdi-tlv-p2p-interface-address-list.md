---
title: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST
description: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST 是一种 TLV，其中包含 Wi-fi Direct 接口的地址列表。
ms.assetid: B7FCB047-28D2-43E2-B4D6-B24E7BC74D47
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INTERFACE_ADDRESS_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 03c0e167d6deecc00ce0c9df0522f7aa806fe2ea
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212687"
---
# <a name="wdi_tlv_p2p_interface_address_list"></a>WDI \_ TLV \_ P2P \_ INTERFACE \_ ADDRESS \_ LIST


WDI \_ tlv \_ P2P \_ INTERFACE \_ ADDRESS \_ list 是一个 Tlv，其中包含 wi-fi Direct 接口的地址列表。

## <a name="tlv-type"></a>TLV 类型


0x18

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 类型                                                  | 说明                      |
|-------------------------------------------------------|----------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | Wi-fi MAC 地址的数组。 |

 

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

 

