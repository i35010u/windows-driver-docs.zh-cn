---
title: WDI_TLV_P2P_CHANNEL_ENTRY_LIST
description: WDI_TLV_P2P_CHANNEL_ENTRY_LIST 是包含通道号列表的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CHANNEL_ENTRY_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 10aea3335bf1ded10f54e0ec84a04b101eb76c92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823744"
---
# <a name="wdi_tlv_p2p_channel_entry_list"></a>WDI \_ TLV \_ P2P \_ 信道 \_ 条目 \_ 列表


WDI \_ tlv \_ P2P \_ 通道 \_ 条目 \_ 列表是包含通道号列表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xF9

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                               | 允许多个 TLV 实例 | 可选 | 说明                          |
|--------------------------------------------------------------------|--------------------------------|----------|--------------------------------------|
| [**WDI \_ TLV \_ 操作 \_ 类**](wdi-tlv-operating-class.md)      |                                |          | 通道的频带。 |
| [**WDI \_ TLV \_ 通道 \_ 信息 \_ 列表**](wdi-tlv-channel-info-list.md) |                                |          | 频道号列表。             |

 

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

 

 




