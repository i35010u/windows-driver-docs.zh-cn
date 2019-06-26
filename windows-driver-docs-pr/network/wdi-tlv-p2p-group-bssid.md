---
title: WDI_TLV_P2P_GROUP_BSSID
description: WDI_TLV_P2P_GROUP_BSSID 是针对本地 Wi-Fi Direct GO 包含组 BSSID TLV。
ms.assetid: C9BC2209-DF72-4775-A3B5-EC37D404CFED
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GROUP_BSSID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 845a106737fb3ec322b9365ee2b5226e98437f82
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374673"
---
# <a name="wditlvp2pgroupbssid"></a>WDI\_TLV\_P2P\_GROUP\_BSSID


WDI\_TLV\_P2P\_组\_BSSID 是针对本地 Wi-Fi Direct GO 包含组 BSSID TLV。

## <a name="tlv-type"></a>TLV 类型


0x73

## <a name="length"></a>长度


大小 （以字节为单位） [ **WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                          |
|---------------------------------------------------|------------------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定组 BSSID 本地 Wi-Fi Direct 转。 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




