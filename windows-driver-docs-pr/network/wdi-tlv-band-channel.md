---
title: WDI_TLV_BAND_CHANNEL
description: WDI_TLV_BAND_CHANNEL 是一种 TLV，其中包含要扫描指定波段的通道。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BAND_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0f78277903af35b5c5e72dbeff814f96b2e88f8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818309"
---
# <a name="wdi_tlv_band_channel"></a>WDI \_ TLV \_ 波段 \_ 通道


WDI \_ tlv \_ 波段 \_ 通道是一个 tlv，其中包含要扫描指定波段的通道。

## <a name="tlv-type"></a>TLV 类型


0x2C

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                               | 允许多个 TLV 实例 | 可选 | 说明                                                                                     |
|--------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ BANDID**](wdi-tlv-bandid.md)                         |                                |          | 指定带区的标识符。                                                          |
| [**WDI \_ TLV \_ 通道 \_ 信息 \_ 列表**](wdi-tlv-channel-info-list.md) |                                |          | 指定要扫描的通道的列表。 如果列表为空，则该端口必须扫描所有通道。 |

 

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

 

 




