---
title: WDI_TLV_PHY_TYPE_LIST
description: WDI_TLV_PHY_TYPE_LIST 是 TLV 包含 PHY 类型的数组。
ms.assetid: 4066E4CE-D63E-4499-AE27-11F6BD57795D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_TYPE_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ed175414be7b8d42f268e761aa3a016825ca2579
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540918"
---
# <a name="wditlvphytypelist"></a>WDI\_TLV\_PHY\_类型\_列表


WDI\_TLV\_PHY\_类型\_列表是包含一个物理类型数组 TLV。

## <a name="tlv-type"></a>TLV 类型


0x19

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_PHY\_类型**](https://msdn.microsoft.com/library/windows/hardware/dn926105)值。 该数组必须包含一个或多个值。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                            | 描述                  |
|-------------------------------------------------|------------------------------|
| [**WDI\_PHY\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/dn926105)\[\] | PHY 类型值的数组。 |

 

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

 

 




