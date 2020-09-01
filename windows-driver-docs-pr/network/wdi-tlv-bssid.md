---
title: WDI_TLV_BSSID
description: WDI_TLV_BSSID 是包含 BSS BSSID 的 TLV。
ms.assetid: 0B3AB317-D1E7-4E61-9F6E-C3134B5A3984
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSSID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ab79a721f5cd0e75f4a637d1fdc2f1c0eaa42d92
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208517"
---
# <a name="wdi_tlv_bssid"></a>WDI \_ TLV \_ BSSID


WDI \_ tlv \_ bssid 是包含 BSS BSSID 的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x2

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型                                              | 说明                                 |
|---------------------------------------------------|---------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定 BSSID 的 Wi-fi MAC 地址。 |

 

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

 

