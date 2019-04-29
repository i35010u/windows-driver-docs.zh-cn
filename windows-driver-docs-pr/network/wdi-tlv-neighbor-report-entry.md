---
title: WDI_TLV_NEIGHBOR_REPORT_ENTRY
description: WDI_TLV_NEIGHBOR_REPORT_ENTRY 是包含相邻报表 TLV。
ms.assetid: 23A0AA84-3EDA-4D6F-9140-2361C0CF55AA
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_NEIGHBOR_REPORT_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0ee93407c51e05707e3828f91ab3f77f378bc650
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392277"
---
# <a name="wditlvneighborreportentry"></a>WDI\_TLV\_邻居\_报表\_条目


WDI\_TLV\_邻居\_报表\_项是包含相邻报表 TLV。

## <a name="tlv-type"></a>TLV 类型


0x123

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                          | 允许多个 TLV 实例 | 可选 | 描述                                                         |
|---------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                      |                                |          | AP 邻居报表中的 BSSID。                         |
| [**WDI\_TLV\_BSSID\_INFO**](wdi-tlv-bssid-info.md)           |                                |          | AP BSSID 信息。                                    |
| [**WDI\_TLV\_OPERATING\_类**](wdi-tlv-operating-class.md) |                                |          | 指示此 BSSID AP 操作类。              |
| [**WDI\_TLV\_CHANNEL\_NUMBER**](wdi-tlv-channel-number.md)   |                                |          | 最后一个已知的操作通道的指示此 BSSID AP。 |
| [**WDI\_TLV\_PHY\_TYPE**](wdi-tlv-phy-type.md)               |                                |          | 指示此 BSSID AP 物理类型。                     |

 

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

 

 




