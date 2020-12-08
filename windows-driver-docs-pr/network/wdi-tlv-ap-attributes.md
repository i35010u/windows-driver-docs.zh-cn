---
title: WDI_TLV_AP_ATTRIBUTES
description: WDI_TLV_AP_ATTRIBUTES 为 TLV，其中包含访问点的属性。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_AP_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c0ff8a9ce0395531a2aad1f6a1b92b3ec1458f2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840887"
---
# <a name="wdi_tlv_ap_attributes"></a>WDI \_ TLV \_ AP \_ 属性


WDI \_ tlv \_ AP \_ 属性是包含访问点属性的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x23

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                        | 允许多个 TLV 实例 | 可选 | 说明                              |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------|
| [**WDI \_ TLV \_ AP \_ 功能**](wdi-tlv-ap-capabilities.md)                               |                                |          | 访问点功能。           |
| [**WDI \_ TLV \_ 单播 \_ 算法 \_ 列表**](wdi-tlv-unicast-algorithm-list.md)                |                                |          | 支持的单播算法。        |
| [**WDI \_ TLV \_ 多播 \_ 数据 \_ 算法 \_ 列表**](wdi-tlv-multicast-data-algorithm-list.md) |                                |          | 支持的多播数据算法。 |

 

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

 

 




