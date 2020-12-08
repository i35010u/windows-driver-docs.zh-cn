---
title: WDI_TLV_BITMAP_PATTERN
description: WDI_TLV_BITMAP_PATTERN 是包含模式的字节数组的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BITMAP_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 44780a7078dfd2d51caa98784abe0007088bb7bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818805"
---
# <a name="wdi_tlv_bitmap_pattern"></a>WDI \_ TLV \_ 位图 \_ 模式


WDI \_ tlv \_ 位图 \_ 模式是包含模式的字节数组的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x68

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 包含模式的字节数组的 UINT8 元素的数组。 Length = (模式长度 + 7) /8。 |

 

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

 

 




