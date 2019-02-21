---
title: WDI_TLV_INDICATION_WAKE_PACKET_PATTERN_ID
description: WDI_TLV_INDICATION_WAKE_PACKET_PATTERN_ID 是模式的 TLV 包含 ID 的唤醒数据包匹配。
ms.assetid: 3E1D4CC4-0369-4C1F-94C6-AFC34C861E0D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_WAKE_PACKET_PATTERN_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 35d662515dd2449077a176e92919b00104386a49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540515"
---
# <a name="wditlvindicationwakepacketpatternid"></a>WDI\_TLV\_指示\_唤醒\_数据包\_模式\_ID


WDI\_TLV\_指示\_唤醒\_数据包\_模式\_ID 是 TLV 包含 ID 的唤醒数据包匹配的模式。

## <a name="tlv-type"></a>TLV 类型


0xB0

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                                    |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 唤醒数据包匹配的模式的 ID。 与添加模式时定义的 ID [OID\_WDI\_设置\_添加\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/dn925858)。 |

 

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

 

 




