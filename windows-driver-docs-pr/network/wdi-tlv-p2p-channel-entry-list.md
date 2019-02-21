---
title: WDI_TLV_P2P_CHANNEL_ENTRY_LIST
description: WDI_TLV_P2P_CHANNEL_ENTRY_LIST 是包含通道编号列表 TLV。
ms.assetid: 10739684-C00C-4AE7-A3B2-D4A6F1E9829B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CHANNEL_ENTRY_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dd4a9ad8ba318cf8023aed75c3faab14b4a1aac1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519039"
---
# <a name="wditlvp2pchannelentrylist"></a>WDI\_TLV\_P2P\_通道\_条目\_列表


WDI\_TLV\_P2P\_通道\_条目\_列表是包含通道编号列表 TLV。

## <a name="tlv-type"></a>TLV 类型


0xF9

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                               | 允许多个 TLV 实例 | 可选 | 描述                          |
|--------------------------------------------------------------------|--------------------------------|----------|--------------------------------------|
| [**WDI\_TLV\_OPERATING\_类**](wdi-tlv-operating-class.md)      |                                |          | 表示通道的频率带区。 |
| [**WDI\_TLV\_CHANNEL\_INFO\_LIST**](wdi-tlv-channel-info-list.md) |                                |          | 通道编号列表。             |

 

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

 

 




