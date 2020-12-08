---
title: WDI_TLV_P2P_CHANNEL_LIST_ATTRIBUTE
description: WDI_TLV_P2P_CHANNEL_LIST_ATTRIBUTE 是包含通道列表属性的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CHANNEL_LIST_ATTRIBUTE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cc12091c1dde751a120b897979bd3843d3f72f9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823745"
---
# <a name="wdi_tlv_p2p_channel_list_attribute"></a>WDI \_ TLV \_ P2P \_ 通道 \_ 列表 \_ 属性


WDI \_ tlv \_ P2P \_ 通道 \_ 列表 \_ 属性是包含通道列表属性的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xD5

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                                          | 允许多个 TLV 实例 | 可选 | 说明              |
|-------------------------------------------------------------------------------|--------------------------------|----------|--------------------------|
| [**WDI \_ TLV \_ 国家/地区 \_ \_ 列表**](wdi-tlv-country-region-list.md)        |                                |          | 国家/地区列表。 |
| [**WDI \_ TLV \_ P2P \_ 信道 \_ 条目 \_ 列表**](wdi-tlv-p2p-channel-entry-list.md) | X                              |          | 通道的列表。    |

 

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

 

 




