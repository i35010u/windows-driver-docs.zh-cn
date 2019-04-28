---
title: WDI_TLV_FT_FTE
description: WDI_TLV_FT_FTE 是包含一个快速转换元素 TLV。
ms.assetid: E502508A-FB01-4F1E-9A68-40AA88894C61
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FT_FTE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c7fae0d2513243cb04316b9083f816f74ff32858
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353134"
---
# <a name="wditlvftfte"></a>WDI\_TLV\_FT\_FTE


WDI\_TLV\_FT\_FTE 是包含一个快速转换元素 TLV。

## <a name="tlv-type"></a>TLV 类型


0x10B

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                    |
|-----------|----------------------------------------------------------------|
| UINT8\[\] | 快速转换包含的元素的 R0KHID 和 SNonce。 |

 

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

 

 




