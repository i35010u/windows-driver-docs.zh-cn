---
title: WDI_TLV_CHANNEL_WIDTH_LIST
description: WDI_TLV_CHANNEL_WIDTH_LIST 是包含一系列通道宽度 TLV。
ms.assetid: 9869157D-2E71-4F08-92D0-A4FFA085ACE7
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHANNEL_WIDTH_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ce0aed396336af11a382a2673fbe7fb80d6389e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525800"
---
# <a name="wditlvchannelwidthlist"></a>WDI\_TLV\_通道\_宽度\_列表


WDI\_TLV\_通道\_宽度\_列表是包含一系列通道宽度 TLV。

## <a name="tlv-type"></a>TLV 类型


0xF5

## <a name="length"></a>长度


UINT32 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入       | 描述                                 |
|------------|---------------------------------------------|
| UINT32\[\] | 通道宽度，以 mhz 为单位指定的列表。 |

 

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

 

 




