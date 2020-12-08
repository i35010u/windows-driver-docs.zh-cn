---
title: WDI_TLV_BAND_INFO
description: WDI_TLV_BAND_INFO 是包含带区信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BAND_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f929c4c0a6d9288ccb8e1c995eaccd7e615d1253
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817059"
---
# <a name="wdi_tlv_band_info"></a>WDI \_ TLV \_ 波段 \_ 信息


WDI \_ tlv \_ 波段 \_ 信息是包含带区信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x27

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                 | 允许多个 TLV 实例 | 可选 | 说明                                   |
|----------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI \_ TLV \_ 波段 \_ 功能**](wdi-tlv-band-capabilities.md)    |                                |          | 带区的功能。                 |
| [**WDI \_ TLV \_ PHY \_ 类型 \_ 列表**](wdi-tlv-phy-type-list.md)           |                                |          | 此带区中有效的 PHY 类型的列表。       |
| [**WDI \_ TLV \_ 通道 \_ 列表**](wdi-tlv-channel-list.md)              |                                |          | 此带区中的有效通道号列表。 |
| [**WDI \_ TLV \_ 通道 \_ 宽度 \_ 列表**](wdi-tlv-channel-width-list.md) |                                |          | 通道宽度的列表（以 MHz 为单位）               |

 

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

 

 




