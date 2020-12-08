---
title: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS
description: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS 是包含 NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 的链接状态更改参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LINK_STATE_CHANGE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2283b9ff4d2aadf1b1d27e70eca6e836ef5a0d46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839215"
---
# <a name="wdi_tlv_link_state_change_parameters"></a>WDI \_ TLV \_ 链接 \_ 状态 \_ 更改 \_ 参数


WDI \_ tlv \_ 链接 \_ 状态 \_ 更改 \_ 参数是一个 TLV，其中包含 NDIS 状态的链接状态更改参数 [ \_ \_ WDI \_ 指示 \_ 链接 \_ 状态 \_ 更改](./ndis-status-wdi-indication-link-state-change.md)。

## <a name="tlv-type"></a>TLV 类型


0x56

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 描述                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定远程对等方的 MAC 地址。                                                                                                                                   |
| UINT32                                            | 指定当前的 TX 链接速度。 这是一个值（以千比特/秒为单位），这是此虚拟化端口的当前 TX 链接速度。 转换为 1 kbps = 1000 bps。 |
| UINT32                                            | 指定当前的 RX 链接速度。 这是一个值（以千比特/秒为单位），这是此虚拟化端口的当前 RX 链接速度。 转换为 1 kbps = 1000 bps。 |
| UINT8                                             | 指定当前链接质量。 这是一个介于0到100之间的值，它是此虚拟化端口的当前链接质量。                                               |

 

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

 

