---
title: WDI_TLV_BEACON_FRAME
description: WDI_TLV_BEACON_FRAME 是包含信号帧 TLV。
ms.assetid: 4022B721-B56E-482C-8F97-C4F7820CF6D1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BEACON_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b0bccb86ff061a53a4b7389d73a533919c2c16ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361778"
---
# <a name="wditlvbeaconframe"></a>WDI\_TLV\_BEACON\_FRAME


WDI\_TLV\_发信号的\_帧是包含信号帧 TLV。

## <a name="tlv-type"></a>TLV 类型


0xA

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                 |
|-----------|-------------------------------------------------------------|
| UINT8\[\] | 指定的信号框架 UINT8 元素的数组。 |

 

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

 

 




