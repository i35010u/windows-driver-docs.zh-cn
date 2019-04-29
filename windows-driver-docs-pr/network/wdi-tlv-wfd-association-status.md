---
title: WDI_TLV_WFD_ASSOCIATION_STATUS
description: WDI_TLV_WFD_ASSOCIATION_STATUS 是 TLV，其中包含要关联请求被拒绝时设置的状态代码。
ms.assetid: E97868FA-3F18-4EEF-B5EF-E2009381A16E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WFD_ASSOCIATION_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 658ded9e9d7d508fc23c6b0b8c1398f5d85e765d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381293"
---
# <a name="wditlvwfdassociationstatus"></a>WDI\_TLV\_WFD\_关联\_状态


WDI\_TLV\_WFD\_关联\_状态是 TLV，其中包含要关联请求被拒绝时设置的状态代码。

## <a name="tlv-type"></a>TLV 类型


0x126

## <a name="length"></a>长度


超出 UINT8 的大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                   |
|-------|-------------------------------------------------------------------------------|
| UINT8 | DOT11\_WFD\_状态\_关联请求被拒绝时要设置的代码。 |

 

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

 

 




