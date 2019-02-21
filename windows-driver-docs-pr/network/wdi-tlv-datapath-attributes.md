---
title: WDI_TLV_DATAPATH_ATTRIBUTES
description: WDI_TLV_DATAPATH_ATTRIBUTES 是 TLV，其中包含数据路径特性。
ms.assetid: 3477054B-01CE-4D08-8A58-49FD8840B237
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DATAPATH_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d4befa0556667dc4f28dd36f338243483680ee74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543804"
---
# <a name="wditlvdatapathattributes"></a>WDI\_TLV\_数据路径\_属性


WDI\_TLV\_数据路径\_属性是包含数据路径属性 TLV。

## <a name="tlv-type"></a>TLV 类型


0xB8

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                      | 允许多个 TLV 实例 | 可选 | 描述                |
|---------------------------------------------------------------------------|--------------------------------|----------|----------------------------|
| [**WDI\_TLV\_数据路径\_功能**](wdi-tlv-datapath-capabilities.md) |                                | X        | 数据路径的功能。 |

 

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

 

 




