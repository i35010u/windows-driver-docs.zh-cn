---
title: WDI_TLV_SSID
description: WDI_TLV_SSID 是包含 SSID TLV。
ms.assetid: 31391E25-B507-4652-9D70-9DA0D6245CA8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SSID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 12ea12a875c7ffa359dd0da4a21ea88128caad89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556061"
---
# <a name="wditlvssid"></a>WDI\_TLV\_SSID


WDI\_TLV\_SSID 是包含 SSID TLV。

## <a name="tlv-type"></a>TLV 类型


0x3B

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 允许数组长度为 0。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                        |
|-----------|----------------------------------------------------|
| UINT8\[\] | 指定 SSID UINT8 元素的数组。 |

 

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

 

 




