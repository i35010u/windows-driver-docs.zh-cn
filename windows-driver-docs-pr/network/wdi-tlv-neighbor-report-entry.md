---
title: WDI_TLV_NEIGHBOR_REPORT_ENTRY
description: WDI_TLV_NEIGHBOR_REPORT_ENTRY 是包含邻居报表的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_NEIGHBOR_REPORT_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 11dea97d8a5baaf06dac926f2a5b85d0ba3a348c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788259"
---
# <a name="wdi_tlv_neighbor_report_entry"></a>WDI \_ TLV \_ 邻居 \_ 报表 \_ 条目


WDI \_ tlv \_ 邻居 \_ 报表 \_ 项是包含邻居报表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x123

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                          | 允许多个 TLV 实例 | 可选 | 说明                                                         |
|---------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------|
| [**WDI \_ TLV \_ BSSID**](wdi-tlv-bssid.md)                      |                                |          | 邻居报表中的 AP 的 BSSID。                         |
| [**WDI \_ TLV \_ BSSID \_ 信息**](wdi-tlv-bssid-info.md)           |                                |          | AP 的 BSSID 信息。                                    |
| [**WDI \_ TLV \_ 操作 \_ 类**](wdi-tlv-operating-class.md) |                                |          | 此 BSSID 指示的 AP 的操作类。              |
| [**WDI \_ TLV \_ 通道 \_ 号**](wdi-tlv-channel-number.md)   |                                |          | 此 BSSID 指示的 AP 的最后一个已知操作通道。 |
| [**WDI \_ TLV \_ PHY \_ 类型**](wdi-tlv-phy-type.md)               |                                |          | 此 BSSID 指示的 AP 的 PHY 类型。                     |

 

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

 

 




