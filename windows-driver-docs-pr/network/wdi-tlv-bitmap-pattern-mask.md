---
title: WDI_TLV_BITMAP_PATTERN_MASK
description: WDI_TLV_BITMAP_PATTERN_MASK 是包含位图模式掩码 TLV。
ms.assetid: 251B3496-04CE-419B-BE5E-C46265F50B7A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BITMAP_PATTERN_MASK 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 87b79c86464e4cead65e6a7267b9a5dc5e76ce9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523117"
---
# <a name="wditlvbitmappatternmask"></a>WDI\_TLV\_BITMAP\_PATTERN\_MASK


WDI\_TLV\_位图\_模式\_掩码是包含位图模式掩码 TLV。

## <a name="tlv-type"></a>TLV 类型


0xE4

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                                                                              |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素数组，包含模式掩码的字节数组。 掩码必须具有每个模式字节的 1 位，因此掩码长度应等于 （模式长度 + 7） / 8。 |

 

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

 

 




