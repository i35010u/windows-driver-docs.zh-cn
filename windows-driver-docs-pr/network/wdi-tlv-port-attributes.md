---
title: WDI_TLV_PORT_ATTRIBUTES
description: WDI_TLV_PORT_ATTRIBUTES 是 TLV 包含端口的属性。
ms.assetid: F5A0BC8D-1B86-41C2-A530-860E15775695
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PORT_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 61552853ad51a798386a55e68f5b1ad087081e53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329879"
---
# <a name="wditlvportattributes"></a>WDI\_TLV\_端口\_属性


WDI\_TLV\_端口\_属性是 TLV 包含端口的属性。

## <a name="tlv-type"></a>TLV 类型


0x29

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                         |
|---------------------------------------------------|-----------------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 指定与端口相关联的 MAC 地址。 |
| UINT16                                            | 指定的端口号。                          |

 

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

 

 




