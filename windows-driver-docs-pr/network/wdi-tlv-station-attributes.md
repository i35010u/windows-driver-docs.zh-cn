---
title: WDI_TLV_STATION_ATTRIBUTES
description: WDI_TLV_STATION_ATTRIBUTES 是包含工作站属性的 TLV。
ms.date: 02/14/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_STATION_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: edaacef09803a50bb33b1a70a54c491fe4572169
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834149"
---
# <a name="wdi_tlv_station_attributes"></a>WDI \_ TLV \_ 工作站 \_ 属性


WDI \_ tlv \_ 工作站 \_ 属性是包含工作站属性的 tlv。

## <a name="tlv-type"></a>TLV 类型

0x22

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
|--- | --- | --- | --- |
| [**WDI \_ TLV \_ 工作站 \_ 功能**](wdi-tlv-station-capabilities.md) |   |   | 工作站功能。 |
| [**WDI \_ TLV \_ 单播 \_ 算法 \_ 列表**](wdi-tlv-unicast-algorithm-list.md) |   | X | 支持的单播算法。 |
| [**WDI \_ TLV \_ 多播 \_ 数据 \_ 算法 \_ 列表**](wdi-tlv-multicast-data-algorithm-list.md) |   | X  | 支持的多播数据算法。 |
| [**WDI \_ TLV \_ 多播 \_ 管理 \_ 算法 \_ 列表**](wdi-tlv-multicast-mgmt-algorithm-list.md) |   | X  | 支持的多播管理算法。 |

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

 

 




