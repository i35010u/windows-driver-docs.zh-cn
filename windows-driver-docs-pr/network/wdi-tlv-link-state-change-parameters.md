---
title: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS
description: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS 是一个 TLV，其中包含 NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 的链接状态更改参数。
ms.assetid: 808C2E69-B713-41A3-AFB9-7441D2A96867
ms.date: 07/18/2017
keywords:
- WDI_TLV_LINK_STATE_CHANGE_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0867d99ccc6fdd2269860eab892061460d63a0c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845058"
---
# <a name="wdi_tlv_link_state_change_parameters"></a>WDI\_TLV\_LINK\_状态\_更改\_参数


WDI\_TLV\_LINK\_状态\_更改\_参数是一个 TLV，其中包含 NDIS\_状态的链接状态更改参数\_WDI\_\_\_[状态的链接\_更改](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-link-state-change)。

## <a name="tlv-type"></a>TLV 类型


0x56

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定远程对等方的 MAC 地址。                                                                                                                                   |
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
<td><p>Windows 10</p></td>
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

 

 




