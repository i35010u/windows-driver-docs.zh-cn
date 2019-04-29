---
title: WDI_TLV_BITMAP_PATTERN
description: WDI_TLV_BITMAP_PATTERN 是包含字节数组的一种模式 TLV。
ms.assetid: 44A18754-3D04-4B62-B8C2-861A47129F08
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BITMAP_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 065bc7c806ea6b5b5bfc0374d019fb134c8554b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327566"
---
# <a name="wditlvbitmappattern"></a>WDI\_TLV\_BITMAP\_PATTERN


WDI\_TLV\_位图\_模式是包含字节数组的一种模式 TLV。

## <a name="tlv-type"></a>TLV 类型


0x68

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素数组，其中包含该模式的字节数组。 长度 = （模式长度 + 7） / 8。 |

 

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

 

 




