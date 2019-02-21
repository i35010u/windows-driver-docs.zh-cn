---
title: WDI_TLV_IHV_DATA
description: WDI_TLV_IHV_DATA 是 TLV，其中包含由 IHV 扩展性模块的 IHV 特定信息。
ms.assetid: 50D80D9E-C3FF-41E5-A054-A5A28ED499FD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IHV_DATA 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b9a334edcc0ad4497b419e15057d6bd8769d8575
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521797"
---
# <a name="wditlvihvdata"></a>WDI\_TLV\_IHV\_DATA


WDI\_TLV\_IHV\_数据是 TLV，其中包含由 IHV 扩展性模块的 IHV 特定信息。

## <a name="tlv-type"></a>TLV 类型


0xBD

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                            |
|-----------|------------------------------------------------------------------------|
| UINT8\[\] | IHV IHV 扩展性模块使用的特定信息。 |

 

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

 

 




