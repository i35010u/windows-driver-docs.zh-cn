---
title: WDI_TLV_P2P_DEVICE_ADDRESS
description: WDI_TLV_P2P_DEVICE_ADDRESS 为 TLV，其中包含组所有者的设备地址。
ms.assetid: EAC1972E-3D9B-4248-BAC3-3C2EB15D6817
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 774a766312a6f8a91644144dd07c9152772ab320
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208489"
---
# <a name="wdi_tlv_p2p_device_address"></a>WDI \_ TLV \_ P2P \_ 设备 \_ 地址


WDI \_ tlv \_ P2P \_ 设备 \_ 地址是一种 Tlv，其中包含组所有者的设备地址。

## <a name="tlv-type"></a>TLV 类型


0x91

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型                                              | 说明                            |
|---------------------------------------------------|----------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 组所有者的设备地址。 |

 

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

 

