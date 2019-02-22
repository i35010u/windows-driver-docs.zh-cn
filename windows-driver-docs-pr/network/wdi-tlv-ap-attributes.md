---
title: WDI_TLV_AP_ATTRIBUTES
description: WDI_TLV_AP_ATTRIBUTES 是 TLV，其中包含访问点的特性。
ms.assetid: FD6F635C-85FF-4668-AA17-12677A61F84D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_AP_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6630d830c214be4460dfc8fb7261ca3102f6286a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523099"
---
# <a name="wditlvapattributes"></a>WDI\_TLV\_AP\_ATTRIBUTES


WDI\_TLV\_AP\_属性是包含属性的访问点 TLV。

## <a name="tlv-type"></a>TLV 类型


0x23

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                        | 允许多个 TLV 实例 | 可选 | 描述                              |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------|
| [**WDI\_TLV\_AP\_CAPABILITIES**](wdi-tlv-ap-capabilities.md)                               |                                |          | 访问点功能。           |
| [**WDI\_TLV\_UNICAST\_ALGORITHM\_LIST**](wdi-tlv-unicast-algorithm-list.md)                |                                |          | 支持的单播算法中。        |
| [**WDI\_TLV\_MULTICAST\_DATA\_ALGORITHM\_LIST**](wdi-tlv-multicast-data-algorithm-list.md) |                                |          | 支持多播的数据的算法。 |

 

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

 

 




