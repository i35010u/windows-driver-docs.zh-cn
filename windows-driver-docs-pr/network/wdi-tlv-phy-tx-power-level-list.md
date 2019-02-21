---
title: WDI_TLV_PHY_TX_POWER_LEVEL_LIST
description: WDI_TLV_PHY_TX_POWER_LEVEL_LIST 是包含一系列 power 级别 TLV。
ms.assetid: DDBF9BBA-9700-4FD2-9521-6D0970E99893
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_TX_POWER_LEVEL_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8fedee8a5cea5c5ae2fc0473516e9d658784744f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533091"
---
# <a name="wditlvphytxpowerlevellist"></a>WDI\_TLV\_PHY\_TX\_POWER\_LEVEL\_LIST


WDI\_TLV\_PHY\_TX\_POWER\_级别\_列表是包含一系列 power 级别 TLV。

## <a name="tlv-type"></a>TLV 类型


0x1C

## <a name="length"></a>长度


UINT32 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入       | 描述                                              |
|------------|----------------------------------------------------------|
| UINT32\[\] | 指定电源级别 UINT32 元素的数组。 |

 

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

 

 




