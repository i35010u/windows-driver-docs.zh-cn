---
title: WDI_TLV_BITMAP_PATTERN_MASK
description: WDI_TLV_BITMAP_PATTERN_MASK 是包含位图模式掩码的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BITMAP_PATTERN_MASK 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 38fba24e4faef0b0dc0d15f94664d01ba00ddc54
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822003"
---
# <a name="wdi_tlv_bitmap_pattern_mask"></a>WDI \_ TLV \_ 位图 \_ 模式 \_ 掩码


WDI \_ tlv \_ 位图 \_ 模式 \_ 掩码是包含位图模式掩码的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xE4

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                                                                                                              |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素的数组，其中包含模式掩码的字节数组。 掩码的每个模式字节必须有1位，因此掩码长度应等于 (模式长度 + 7) /8。 |

 

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

 

 




