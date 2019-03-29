---
title: WDI_TLV_FT_MDE
description: WDI_TLV_FT_MDE 是包含的 BSS 条目 MDIE TLV。
ms.assetid: 2D075487-9B1E-4DEE-B3C3-3208C1CBAB64
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FT_MDE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5ad29a8f82b24f87822ef529fa3cea473b2f0122
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566817"
---
# <a name="wditlvftmde"></a>WDI\_TLV\_FT\_MDE


WDI\_TLV\_FT\_MDE 是包含的 BSS 条目 MDIE TLV。

## <a name="tlv-type"></a>TLV 类型


0x10D

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述              |
|-----------|--------------------------|
| UINT8\[\] | BSS 条目的 MDIE。 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




